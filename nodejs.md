# Node.js

Node.js 是一个基于 Chrome V8 引擎 (Google Chrome 的内核) 的 JavaScript 运行时环境，它使得 JavaScript 不仅可以在浏览器中运行，还可以在服务器端运行。

Node.js 的主要特点包括：

1. **非阻塞 I/O**：Node.js 使用事件驱动和异步 I/O 模型，这使得它能够处理大量并发连接，并且性能高效。

    > **同步 I/O（阻塞模型）的情况：**
    >
    > 在传统的同步 I/O 模型中，当服务器接收到一个请求时，它会进行一些 I/O 操作，比如读取文件、访问数据库等。这些操作是**阻塞的**，即服务器在等待操作完成时无法处理其他请求。这样，**如果有大量请求到达**，服务器可能会被阻塞，导致延迟增加，吞吐量下降。

2. **单线程**：Node.js 采用单线程模型来处理所有的并发请求。通过事件循环（Event Loop）和回调函数，Node.js 能够在同一个线程上高效地管理多个任务。

3. **高性能**：Node.js 基于 Google 的 V8 引擎，这使得它能够执行 JavaScript 代码非常快速。

4. **模块化**：Node.js 提供了丰富的内置模块和包管理器 npm（Node Package Manager），开发者可以很容易地安装、共享和使用各种开源模块。

5. **广泛的应用场景**：Node.js 被广泛应用于构建高性能的 Web 应用程序、API 服务、实时聊天系统等。

