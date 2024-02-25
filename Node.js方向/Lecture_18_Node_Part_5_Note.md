# Lecture 18 Node Part 5

## Description
本篇笔记为 Lily 老师的 Lecture 18 Node.js (Part 5) 随堂笔记

## Table of Content
- [1. Build A Simple Server.js(No Databse connected)](#1-build-a-simple-serverjsno-databse-connected)
- [2. Node.js and Express.js for Project](#2-nodejs-and-expressjs-for-project)
## Introduction
> To text and debug backend, you need:
- learn how to use postman
- learn how to debug and use breakpoint
## 1. Build A Simple Server.js(No Databse connected)
1. **Installing Dependencies**: 
    - First, initialize a Node project by running `npm i -y` or `npm install -y` in terminal, which will generate the `package.json` and `package-lock.json` files. These files manage project dependencies and configurations.

    - You can customize scripts in the package.json file.

2. **Installing Express**: 
    - Install Express by executing `npm i express` in terminal.

3. **Installing Nodemon**: To install Nodemon and update the script in the package.json file:
    - `npm install nodemon -D`
    ``` js
    "scripts": {
        "start": "nodemon app.js"
    }
    ```

4. **Creating a Server**: Now, let's create a basic server in `app.js`:

    ```js
    const express = require('express')
    const app = express()

    app.listen(3000, ()=>{
      console.log('server running on 3000')
    })
    ```
    - With this code, we've set up a server that listens on port 3000.

    - Afterward, use npm start in the terminal to start the server and test it.

5. **Building Routes**: Next, we'll build routes to handle HTTPS requests. This involves defining endpoints for various functionalities our API will support.
    ```js
    app.get('/users', ()=>{
      // 业务逻辑
    })
    
    app.post('/users', ()=>{
      // 业务逻辑
    })
    
    app.update('/users/:id', ()=>{
      // 业务逻辑
    })
    
    app.delete('/users/:id', ()=>{
      // 业务逻辑
    })
    
    ```
    
6. **error handling middleware**: add error handling middleware and place it at the end of all the route, just before `app.listen()`
    ```js
    app.use((err, req, res, next)=>{
      res.status(err.status || 500).json({
        message: err.message,
        ...(process.env.NODE_ENV) == 'development' && (stack: err.stack)
      }); // dont forget to configure the .env file development mode first
    })

    app.listen(3000, ()=>{
      ...
    })
    ```

Now you have set up a simple backend! 

However, building a backend for a real project is more complex than this. Let's take a look at the file structure of the backend using Node.js and Express.js.

## 2. Node.js and Express.js for Project
### 2.1 file structure
``` js
Common
  // 配置
Controllers
Logs
Models
Servies
  // 业务处理
Routes 
  // 所有的路由，
  // 按照功能不同放在不同的文件里
  // 每一个路由都绑定到控制器上
Middleware
Config
Public/Static
Views
```
### 2.2 log
controller和services里一般会写日志
- Winston：`npm install winston`
  - winston 可以定义不同级别的日志消息，如 error、warn、info、verbose、debug
- Morgan：`npm install morgan`
  - 记录请求的中间件
  - morgan 提供了多种预定义的日志格式，如 combined、common、dev、short、tiny 等，每种
格式都有不同的日志详情。你也可以定义自己的格式
- log4js
### 2.3 API Security
#### Helmet
`npm i helmet`
```js
import express from "express";
import helmet from "helmet";

const app = express();

// Use Helmet!
app.use(helmet());

app.get("/", (req, res) => {
  res.send("Hello world!");
});

app.listen(8000);
```
- By default, Helmet sets the following headers:
  - `Content-Security-Policy`: A powerful allow-list of what can happen on your page which mitigates many attacks
  - `Cross-Origin-Opener-Policy`: Helps process-isolate your page
  - `Cross-Origin-Resource-Policy`: Blocks others from loading your resources cross-origin
  - `Origin-Agent-Cluster`: Changes process isolation to be origin-based
  - `Referrer-Policy`: Controls the Referer header
  - `Strict-Transport-Security`: Tells browsers to prefer HTTPS
  - `X-Content-Type-Options`: Avoids MIME sniffing
  - `X-DNS-Prefetch-Control`: Controls DNS prefetching
  - `X-Download-Options`: Forces downloads to be saved (Internet Explorer only)
  - `X-Frame-Options`: Legacy header that mitigates clickjacking attacks
  - `X-Permitted-Cross-Domain-Policies`: Controls cross-domain behavior for Adobe products, like Acrobat
  - `X-Powered-By`: Info about the web server. Removed because it could be used in simple attacks
  - `X-XSS-Protection`: Legacy header that tries to mitigate XSS attacks, but makes things worse, so Helmet disables it
#### rate limiting
- 防止过渡访问API
- `npm install express-rate-limit`
### 2.4 CORS
#### What is CORS? 

CORS (Cross-Origin Resource Sharing) consists of a set of HTTP response headers that determine whether the browser will prevent front-end JS code from accessing resources across domains.

By default, the browser's same-origin security policy prevents web pages from accessing resources "across the domain". However, if the interface server is configured with CORS-related HTTP response headers, the crossdomain access restrictions on the browser side can be lifted.

Tips:
- CORS is primarily configured on the server side. The client browser does not need to do any additional configuration to request a CORS-enabled interface
  - configure at the backend
  - Jsonp  
- CORS has browser compatibility. Only browsers that support XMLHttpRequest Level 2 can properly access the server-side interface with CORS enabled (e.g. IE10+, Chrome4+, FireFox3.5+).
- cors is a third party middleware for Express. Cross-domain issues can be easily resolved by installing and configuring the cors middleware.It can be used in 3 steps as follows. 
  -  Run `npm install cors` to install the middleware 
  -  import the middleware using const cors = require('cors')
  -  Call app.use(cors()) to configure the middleware before routing
### 2.5 API Document and Versioning
#### Swagger
- install `install swagger-jsdoc swagger-ui-express --save`
- configure
#### Document and Versioning Best Practice
- url 路径版本控制
`api/v1/resource`
- 查询参数指定版本
`/api/resource?version=1`
- 通过 http 请求头控制版本
- 提供清晰文档
  - 过渡期
  - 迁移指南
- 测试
