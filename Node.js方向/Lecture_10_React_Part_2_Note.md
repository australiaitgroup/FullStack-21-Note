# Lecture 10 React (2)

## Description
本篇笔记以 Zhao Long 老师的 Lecture 09 React (Part 2) 随堂笔记
## Table of Content
- [React 是简单易用的框架](#1-react-是简单易用的框架)  
- [如何搭建 React 项目](#2-如何搭建-react-项目)  
- [React 的基本概念](#3-react-的基本概念)  
- [React 语法举例](#4-react-语法举例)  
- [补充](#5-补充)
## 1 React 是简单易用的框架
- JS 是命令式的，React是声明式的
- 不要神话 React！React是简单的，可读的，组件化的
- 在IT中一定是简单易用的技术才能存活下来
- 不要想复杂的东西
## 2 如何搭建 React 项目 
### 2.1 使用脚手架搭建
- 脚手架是一个工具，帮我们创建项目的基本功能，包括Babel的配置
  - vite 脚手架 `npm create vite my-project-name -- --template react`
    - 为什么使用 vite， vite 比 create react app 好在哪？
      - 因为简单 上手快 好学
      - Junior 不要谈 performance
    - [vite 的官方文档](https://vitejs.dev/)
### 2.2 什么是打包器？
  - webpack 是现在主流前端打包工具，但过于繁杂
  - Rollup 正逐渐代替 webpack
  - Turbo
### 2.3 React App 基本架构
  - `index.html` 是入口文件，所以要看一个 Web App 是怎么工作的，首先去看 `index.html`
  - 根节点 `root` 和 树状结构 `tree`
    - 在React中，根节点通常是应用的顶层组件，它是整个组件树的起点。在React的`虚拟DOM`中，根节点是`真实DOM树`的入口点。通过`ReactDOM库`中的`ReactDOM.render()方法`，你可以将`React元素`渲染到一个`真实的DOM节点`上，这个节点就是根节点。
    - 组件树是由多个组件嵌套而成的层级结构，它描述了整个应用的组织和关系。组件树的结构反映了应用的UI结构，每个节点都代表一个React组件。
    - 什么是 `ReactDom.createRoot()`?
      - `ReactDom.createRoot`在`index.html`上创建了一个根节点
    - 什么是 `react.render()`?
      - `react.render()`在根节点上渲染了`<APP />`
    - 什么是 `ReactDom`?
      - `ReactDom`是一个桥梁，用于连接React和HTML
  - `React.StrictMode`
## 3 React 的基本概念
### 3.1 概念区分：React，JSX，Babel，脚手架
- React
  - 是一个工具，让我们能够简单容易的去创建交互式的UI。React 是一个JavaScript 库，用于构建用户界面。它不是一个完整的框架，而是专注于视图层的构建。
- JSX
  - 是 React 的核心概念, React 通过引进JSX来实现简单容易的语法来创建交互式的UI，JSX是提高了代码的可读性和可维护性，而不是性能提升
- Babel
  - 是 JS 编译器，他将JSX编译成浏览器可以执行的标准JS，
- 脚手架: 
  - 是一个工具，帮我们创建项目的基本功能，包括Babel的配置
### 3.2 理解 JSX 的语法和作用
- JSX（JavaScript XML）是一种 JavaScript 的语法扩展，用于在 JavaScript 代码中声明 React 元素。它允许开发者在 JavaScript 中以类似于 XML 或 HTML 的方式书写 UI 组件的结构。
- 在 JavaScript 中写 HTML： JSX 允许在 JavaScript 代码中直接嵌入类似 HTML 的标记，这使得编写 React 组件时更加直观和方便。
  - 在 JSX 里面，所有以<开头 到>结尾的内容，都被认定为 HTML
    ```jsx
    <h1>Hello, World!</h1>;
    <div>1 + 1</div> => 1 + 1
    ```
  - 在 JSX 里面，所有以{开头 到}结尾的内容，都被认定为 JavaScript
    ```jsx
    <div>{1 + 1}</div> => 2
    <div>{js表达式}</div>
    <div>`${js表达式}`</div>
    ```
- JSX 的特点: 可读性和可维护性，不要提 reusable

- 浏览器不能理解jsx，所以要使用babel编译：JSX 本身是一种语法糖，浏览器无法直接理解。为了在浏览器中运行 React 应用，需要使用工具链中的 Babel 来将 JSX 编译为普通的 JavaScript。这个编译过程通常与其他工具和配置一起使用，以便将 JSX 转换为浏览器可执行的代码。
### 3.3 Babel
通过Babel，开发人员可以写出更现代，更易读，更易维护，同时不牺牲兼容性。通常通过`.babelrc` 或 `babel.config.js` 文件进行配置。
- 原始的 JSX 代码需要通过 Babel 来编译
  - JSX
    ```jsx
    const element = <h1>Hello, world!</h1>
    // JSX 语言
    ```
  - Bable 将 JSX 语言 编译成合法的 JS 语言
  - 通过 Babel 编译后的 JavaScript 代码
    ```js
    const element = React.createElement('h1', null, 'Hello, World!');
    // JS 语言
    ```
## 4 React 语法举例
数组映射
  ```jsx
  <ul>
    {fruits.map((item, item_id)=>(
      <li key={item_id}>item</li>
    ))}
  </ul>
  ```
  - 当最终渲染结果来自于数组，那这些渲染结果需要有独一无二的 `key`, 因为 React 需要 key 来正确的使用 virtual dom
  - 关于 `key`
    - 如果数据来自后端数据库的可以使用 `id` 或 `uuid`
    - 如果数据是自己声明的，就设计一个 `id`/`key` 可以手动设计一个
    - 使用索引作为 `key` 是不推荐的，因为 `index` 的顺序可能会改变（比如有一个 sort button 把列表进行了重新排序），这可能会导致性能问题
    - 即使面试官说以后不会使用 sort 功能，也回答不可以使用 index，因为不可读
    - key的作用域是局部的，只考虑他在数组内的作用域，不需要考虑全局唯一，但要在兄弟元素里是唯一的

  - 为什么使用 map 而不是 forEach
## 5 补充：
> 有时间可以了解以下virtual dom reconciliation https://legacy.reactjs.org/docs/faq-internals.html 

> 写代码不考虑未来，小组组员也无法同一个标准和时间点上考虑未来，所以写代码的时候只按照当前的标准和需求写

> Scalable 不是通过考虑未来来增加的，而是基于可读，可维护，可复用的高质量的代码
