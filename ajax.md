# Ajax（Asynchronous JavaScript and XML）

[TOC]

AJAX（Asynchronous JavaScript and XML）是一种在网页上与服务器进行异步交互的技术，使得网页可以在不重新加载整个页面的情况下与服务器交换数据并更新部分网页内容。AJAX 是基于 JavaScript、XML（或 JSON）以及一些额外的浏览器功能（如 `XMLHttpRequest` 或 `Fetch API`）实现的。

# 原生AJAX

原生AJAX 允许你向服务器发送请求（如 GET、POST 请求），然后异步接收响应并处理结果，常用于实现动态网页加载和用户交互。



## GET请求

```js
// 1. 创建 XMLHttpRequest 对象
const xhr = new XMLHttpRequest();

// 2. 配置请求（例如 GET 请求，异步）
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts', true);

// 3. 设置请求完成后的回调函数
xhr.onreadystatechange = function () {
    // 请求完成
    if (xhr.readyState === 4 && xhr.status === 200) {
        // 4. 处理响应结果（此例是 JSON 格式）
        let data = JSON.parse(xhr.responseText);
        console.log(data); // 打印返回的 JSON 数据
    }
};

// 4. 发送请求
xhr.send();

```



## POST请求

```js
const xhr = new XMLHttpRequest();
xhr.open('POST', 'https://jsonplaceholder.typicode.com/posts', true);
xhr.setRequestHeader('Content-Type', 'application/json'); // 设置请求头，告知服务器请求体的格式

xhr.onreadystatechange = function () {
    if (xhr.readyState === 4 && xhr.status === 201) {
        let response = JSON.parse(xhr.responseText);
        console.log(response);
    }
};

const data = {
    title: 'foo',
    body: 'bar',
    userId: 1
};

// 将 JavaScript 对象转换为 JSON 字符串并发送
xhr.send(JSON.stringify(data));

```



## 常用的 `readyState` 状态值

- `0` - 请求未初始化
- `1` - 服务器连接已建立
- `2` - 请求已接收
- `3` - 请求处理中
- `4` - 请求已完成，且响应已就绪

## 常用的 `status` 状态码

- `200` - 请求成功
- `400` - 错误请求
- `404` - 请求的资源未找到
- `500` - 服务器内部错误

## 如何在 JavaScript 中使用 JSON 对象

1. **解析 JSON 字符串**：使用 `JSON.parse()` 将 JSON 字符串转换为 JavaScript 对象。

   ```javascript
   var jsonString = '{"name": "Alice", "age": 30}';
   var jsonObj = JSON.parse(jsonString);
   console.log(jsonObj.name); // 输出: Alice
   ```

2. **将 JavaScript 对象转为 JSON 字符串**：使用 `JSON.stringify()` 将 JavaScript 对象转换为 JSON 字符串。

   ```javascript
   var obj = { name: "Bob", age: 25 };
   var jsonString = JSON.stringify(obj);
   console.log(jsonString); // 输出: {"name":"Bob","age":25}
   ```



# Axios

https://www.axios-http.cn/docs/instance

## 导入 `axios`

使用 npm:

```bash
$ npm install axios
```

使用 bower:

```bash
$ bower install axios
```

使用 yarn:

```bash
$ yarn add axios
```

使用CDN:

```html
<!-- 使用 jsDelivr CDN: -->
<script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
<!-- 使用 unpkg CDN: -->
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
```

然后你就可以直接使用 `axios`，不需要 `import` 或 `require`。

CommonJS 引入方式（适用于 Node.js）

```js
const axios = require('axios');
```

ES6 模块引入方式（适用于前端或使用 ES6 模块的项目）

```js
import axios from 'axios';
```

## GET请求

```js
// 发起一个 GET 请求
const axios = require('axios');

// 向给定ID的用户发起请求
axios.get('/user?ID=12345')
  .then(function (response) {
    // 处理成功情况
    console.log(response);
  })
  .catch(function (error) {
    // 处理错误情况
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });

// 上述请求也可以按以下方式完成（可选）
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // 总是会执行
  });  

// 支持async/await用法
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

>**注意:** 由于`async/await` 是ECMAScript 2017中的一部分，而且在IE和一些旧的浏览器中不支持，所以使用时务必要小心。

## POST请求

```js
// 发起一个 POST 请求
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });

// 发起多个并发请求
function getUserAccount() {
  return axios.get('/user/12345');
}

function getUserPermissions() {
  return axios.get('/user/12345/permissions');
}

const [acct, perm] = await Promise.all([getUserAccount(), getUserPermissions()]);

// OR

Promise.all([getUserAccount(), getUserPermissions()])
  .then(function ([acct, perm]) {
    // ...
  });

// 将 HTML Form 转换成 JSON 进行请求
const {data} = await axios.post('/user', document.querySelector('#my-form'), {
  headers: {
    'Content-Type': 'application/json'
  }
})
```

## Axios API

可以向 `axios` 传递相关配置来创建请求

**axios(config)**

```js
// 发起一个post请求
axios({
  method: 'post',
  url: '/user/12345',
  data: {
    firstName: 'Fred',
    lastName: 'Flintstone'
  }
});
```

```js
// 在 node.js 用GET请求获取远程图片
axios({
  method: 'get',
  url: 'http://bit.ly/2mTM3nY',
  responseType: 'stream'
})
  .then(function (response) {
    response.data.pipe(fs.createWriteStream('ada_lovelace.jpg'))
  });
```

**axios(url[, config])**

```js
// 发起一个 GET 请求 (默认请求方式)
axios('/user/12345');
```

### 请求方式别名

为了方便起见，已经为所有支持的请求方法提供了别名。

**axios.request(config)**

**axios.get(url[, config])**

**axios.delete(url[, config])**

**axios.head(url[, config])**

**axios.options(url[, config])**

**axios.post(url[, data[, config]])**

**axios.put(url[, data[, config]])**

**axios.patch(url[, data[, config]])**

**axios.postForm(url[, data[, config]])**

**axios.putForm(url[, data[, config]])**

**axios.patchForm(url[, data[, config]])**

> 注意：在使用别名方法时， `url`、`method`、`data` 这些属性都不必在配置中指定。

## Axios 实例

### 创建一个实例

您可以使用自定义配置新建一个实例。

**axios.create([config])**

```js
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

### 实例方法

以下是可用的实例方法。指定的配置将与实例的配置合并。

**axios#request(config)**

**axios#get(url[, config])**

**axios#delete(url[, config])**

**axios#head(url[, config])**

**axios#options(url[, config])**

**axios#post(url[, data[, config]])**

**axios#put(url[, data[, config]])**

**axios#patch(url[, data[, config]])**

**axios#getUri([config])**

## 请求配置

这些是创建请求时可以用的配置选项。只有 `url` 是必需的。如果没有指定 `method`，请求将默认使用 `GET` 方法。

```js
{
  // `url` 是用于请求的服务器 URL
  url: '/user',

  // `method` 是创建请求时使用的方法
  method: 'get', // 默认值

  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',

  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 它只能用于 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 数组中最后一个函数必须返回一个字符串， 一个Buffer实例，ArrayBuffer，FormData，或 Stream
  // 你可以修改请求头。
  transformRequest: [function (data, headers) {
    // 对发送的 data 进行任意转换处理

    return data;
  }],

  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对接收的 data 进行任意转换处理

    return data;
  }],

  // 自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},

  // `params` 是与请求一起发送的 URL 参数
  // 必须是一个简单对象或 URLSearchParams 对象
  params: {
    ID: 12345
  },

  // `paramsSerializer`是可选方法，主要用于序列化`params`
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function (params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },

  // `data` 是作为请求体被发送的数据
  // 仅适用 'PUT', 'POST', 'DELETE 和 'PATCH' 请求方法
  // 在没有设置 `transformRequest` 时，则必须是以下类型之一:
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属: FormData, File, Blob
  // - Node 专属: Stream, Buffer
  data: {
    firstName: 'Fred'
  },
  
  // 发送请求体数据的可选语法
  // 请求方式 post
  // 只有 value 会被发送，key 则不会
  data: 'Country=Brasil&City=Belo Horizonte',

  // `timeout` 指定请求超时的毫秒数。
  // 如果请求时间超过 `timeout` 的值，则请求会被中断
  timeout: 1000, // 默认值是 `0` (永不超时)

  // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default

  // `adapter` 允许自定义处理请求，这使测试更加容易。
  // 返回一个 promise 并提供一个有效的响应 （参见 lib/adapters/README.md）。
  adapter: function (config) {
    /* ... */
  },

  // `auth` HTTP Basic Auth
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },

  // `responseType` 表示浏览器将要响应的数据类型
  // 选项包括: 'arraybuffer', 'document', 'json', 'text', 'stream'
  // 浏览器专属：'blob'
  responseType: 'json', // 默认值

  // `responseEncoding` 表示用于解码响应的编码 (Node.js 专属)
  // 注意：忽略 `responseType` 的值为 'stream'，或者是客户端请求
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // 默认值

  // `xsrfCookieName` 是 xsrf token 的值，被用作 cookie 的名称
  xsrfCookieName: 'XSRF-TOKEN', // 默认值

  // `xsrfHeaderName` 是带有 xsrf token 值的http 请求头名称
  xsrfHeaderName: 'X-XSRF-TOKEN', // 默认值

  // `onUploadProgress` 允许为上传处理进度事件
  // 浏览器专属
  onUploadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `onDownloadProgress` 允许为下载处理进度事件
  // 浏览器专属
  onDownloadProgress: function (progressEvent) {
    // 处理原生进度事件
  },

  // `maxContentLength` 定义了node.js中允许的HTTP响应内容的最大字节数
  maxContentLength: 2000,

  // `maxBodyLength`（仅Node）定义允许的http请求内容的最大字节数
  maxBodyLength: 2000,

  // `validateStatus` 定义了对于给定的 HTTP状态码是 resolve 还是 reject promise。
  // 如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，
  // 则promise 将会 resolved，否则是 rejected。
  validateStatus: function (status) {
    return status >= 200 && status < 300; // 默认值
  },

  // `maxRedirects` 定义了在node.js中要遵循的最大重定向数。
  // 如果设置为0，则不会进行重定向
  maxRedirects: 5, // 默认值

  // `socketPath` 定义了在node.js中使用的UNIX套接字。
  // e.g. '/var/run/docker.sock' 发送请求到 docker 守护进程。
  // 只能指定 `socketPath` 或 `proxy` 。
  // 若都指定，这使用 `socketPath` 。
  socketPath: null, // default

  // `httpAgent` and `httpsAgent` define a custom agent to be used when performing http
  // and https requests, respectively, in node.js. This allows options to be added like
  // `keepAlive` that are not enabled by default.
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),

  // `proxy` 定义了代理服务器的主机名，端口和协议。
  // 您可以使用常规的`http_proxy` 和 `https_proxy` 环境变量。
  // 使用 `false` 可以禁用代理功能，同时环境变量也会被忽略。
  // `auth`表示应使用HTTP Basic auth连接到代理，并且提供凭据。
  // 这将设置一个 `Proxy-Authorization` 请求头，它会覆盖 `headers` 中已存在的自定义 `Proxy-Authorization` 请求头。
  // 如果代理服务器使用 HTTPS，则必须设置 protocol 为`https`
  proxy: {
    protocol: 'https',
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },

  // see https://axios-http.com/zh/docs/cancellation
  cancelToken: new CancelToken(function (cancel) {
  }),

  // `decompress` indicates whether or not the response body should be decompressed 
  // automatically. If set to `true` will also remove the 'content-encoding' header 
  // from the responses objects of all decompressed responses
  // - Node only (XHR cannot turn off decompression)
  decompress: true // 默认值

}
```

## 响应结构

一个请求的响应包含以下信息。

```js
{
  // `data` 由服务器提供的响应
  data: {},

  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,

  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',

  // `headers` 是服务器响应头
  // 所有的 header 名称都是小写，而且可以使用方括号语法访问
  // 例如: `response.headers['content-type']`
  headers: {},

  // `config` 是 `axios` 请求的配置信息
  config: {},

  // `request` 是生成此响应的请求
  // 在node.js中它是最后一个ClientRequest实例 (in redirects)，
  // 在浏览器中则是 XMLHttpRequest 实例
  request: {}
}
```

当使用 `then` 时，您将接收如下响应:

```js
axios.get('/user/12345')
  .then(function (response) {
    console.log(response.data);
    console.log(response.status);
    console.log(response.statusText);
    console.log(response.headers);
    console.log(response.config);
  });
```

当使用 `catch`，或者传递一个[rejection callback](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then)作为 `then` 的第二个参数时，响应可以通过 `error` 对象被使用，正如在[错误处理](https://www.axios-http.cn/docs/handling_errors)部分解释的那样。

## 拦截器

在请求或响应被 then 或 catch 处理前拦截它们。

```js
// 添加请求拦截器
axios.interceptors.request.use(function (config) {
    // 在发送请求之前做些什么
    return config;
  }, function (error) {
    // 对请求错误做些什么
    return Promise.reject(error);
  });

// 添加响应拦截器
axios.interceptors.response.use(function (response) {
    // 2xx 范围内的状态码都会触发该函数。
    // 对响应数据做点什么
    return response;
  }, function (error) {
    // 超出 2xx 范围的状态码都会触发该函数。
    // 对响应错误做点什么
    return Promise.reject(error);
  });
```

如果你稍后需要移除拦截器，可以这样：

```js
const myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```

可以给自定义的 axios 实例添加拦截器。

```js
const instance = axios.create();
instance.interceptors.request.use(function () {/*...*/});
```

## 错误处理

```js
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 请求成功发出且服务器也响应了状态码，但状态代码超出了 2xx 的范围
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // 请求已经成功发起，但没有收到响应
      // `error.request` 在浏览器中是 XMLHttpRequest 的实例，
      // 而在node.js中是 http.ClientRequest 的实例
      console.log(error.request);
    } else {
      // 发送请求时出了点问题
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```

使用 `validateStatus` 配置选项，可以自定义抛出错误的 HTTP code。

```js
axios.get('/user/12345', {
  validateStatus: function (status) {
    return status < 500; // 处理状态码小于500的情况
  }
})
```

使用 `toJSON` 可以获取更多关于HTTP错误的信息。

```js
axios.get('/user/12345')
  .catch(function (error) {
    console.log(error.toJSON());
  });
```



# Fetch API

Fetch API 是一种现代的、功能强大的网络请求工具，它允许你通过 JavaScript 异步地请求资源，而不需要使用传统的 XMLHttpRequest 对象。

Fetch API 可以简洁地发起 HTTP 请求，并处理服务器的响应。

Fetch API 基于 Promise 设计，使得异步操作更加简洁和易于理解。

**Fetch 优点：**

- 基于 **Promises**，代码更加简洁和易读。
- 更好的错误处理机制：只在网络错误（如无法连接服务器）时返回 `catch`，而非状态码错误。
- 支持多种数据格式（JSON、文本、二进制等）。
- 可以处理跨域请求，通过 `CORS` 机制配置。

## fetch 的基本用法

fetch 的语法相当简洁，最基本的形式是：

```js
fetch(url)
  .then(response => response.json()) // 解析 JSON 数据
  .then(data => console.log(data))   // 处理数据
  .catch(error => console.error('Error:', error)); // 错误处理
```

**参数：**

- **url**：要发送请求的目标 URL。
- **options**（可选）：可以指定请求方法（GET、POST 等）、请求头、请求体等内容。

**返回值：**

返回一个 Promise 对象，Promise 在请求成功时返回 Response 对象，在请求失败时被拒绝。

------

## 使用 Fetch

### GET 请求

```js
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在这个例子中，fetch 默认执行 GET 请求，返回的 response 是一个 Response 对象，通过调用 .json() 方法来解析 JSON 数据。

### POST 请求

```js
fetch('https://api.example.com/data', {
    method: 'POST', // 指定请求方法
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        key: 'value',
        name: 'Pete',
        age: 11
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

这里，我们通过设置 method 为 'POST' 来发送 POST 请求，并在请求体 body 中发送 JSON 格式的数据。

### 处理响应状态

```js
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok ' + response.statusText);
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在处理响应时，我们首先检查响应状态是否成功（response.ok），如果不成功则抛出错误。

### 发送带凭据的请求

```js
fetch('https://api.example.com/data', {
  credentials: 'include' // 包括 cookies 在请求中
});
```

使用 credentials: 'include' 可以在跨域请求中发送 cookies。

### 使用 Request 和 Response 对象

```js
const request = new Request('flowers.jpg');
fetch(request)
    .then(response => response.blob())
    .then(imageBlob => {
        const imageObjectUrl = URL.createObjectURL(imageBlob);
        img.src = imageObjectUrl;
    });
```

你可以创建 Request 对象来定制请求，fetch 会返回一个 Response 对象，你可以用它来获取不同类型的响应体，如 blob、text、json 等。

### 错误处理

```js
fetch('https://api.example.com/data')
    .then(response => {
        if (response.ok) {
            return response.json();
        }
        throw new Error('Something went wrong');
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在链式调用中，任何地方抛出的错误都会被 .catch() 捕获。

### 设置请求头

```js
fetch('https://example.com/api', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer your-token'
    },
    body: JSON.stringify({ name: 'John', age: 30 })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

可以通过 headers 属性为请求添加自定义的 HTTP 头信息，例如 Content-Type、Authorization 等。

### 处理非 200 的响应状态

```js
fetch('https://example.com/api')
  .then(response => {
    if (!response.ok) { // 检查响应状态
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));
```

fetch 不会自动将 HTTP 错误状态（如 404 或 500）作为拒绝的 Promise，仍然需要检查响应状态。

### 发送表单数据

```js
const formData = new FormData();
formData.append('username', 'John');
formData.append('email', 'john@example.com');

fetch('https://example.com/api/form', {
    method: 'POST',
    body: formData
})
.then(response => response.text())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

可以使用 FormData 对象将表单数据发送给服务器：

### 跨域请求

```js
fetch('https://example.com/api', {
    method: 'GET',
    credentials: 'include' // 允许跨域请求时携带 cookie
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

如果需要进行跨域请求，可以在服务器端设置 CORS（Cross-Origin Resource Sharing）。在前端，也可以通过 credentials 选项来指定是否发送 cookies 等凭据。



