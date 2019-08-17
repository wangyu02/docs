# SpringBoot 跨域请求的解决方案#

---

- 跨域请求的基本概念：

  CORS(Cross Origin Resource Sharing) 跨域资源请求：表示javaScript 代码所在的及其和后端api 所在机器不是同一台的情况下实现资源访问。

  **在当前前后端分离的项目中，前端一般是SPA(Single Page Application)类型的应用，所有的JavaScript代码都会下载到用户机器的浏览器上，后端api 服务器端以单个机器或者集群的形式存在**

- 同源策略的概念

  同源策略限制了一个从同一个源加载文档或脚本如何与来自一个源的资源进行交互。这是一个用于隔离潜在恶意文件的重要安全机制。

  由于浏览器的同源策略限制，在前后端分离的项目中必须要考虑这个问题，否则就会出现以下的报错：

  ```sh
  Access to XMLHttpRequest at 'http://localhost:8081/api' from origin 'http://localhost:3000' has been blocked by CORS policy: Response to preflight request doesn't pass access control check: No 'Access-Control-Allow-Origin' header is present on the requested resource.
  ```

  

