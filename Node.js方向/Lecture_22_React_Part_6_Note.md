# Lecture 22 React Part 6
## Description
本篇笔记为 Zhao Long 老师的 Lecture 22 React (Part 6) 随堂笔记

## 学习方法
> Get hands dirty
> Do not wait for everything to be ready

### Writing a React App
Prerequisites：knowing `HTML`, `CSS`, `JavaScript`(`jQuery`), but unfamiliar with `React`, ow to write a React App with existing knowledge:
- Existing Assets：
  - `index.html`
    - `index.js`
    - `styles.css`
    - Importing `jQuery`
      ```html
      <head>
        <script src="https://unpkg.com/browse/jquery@3.7.1/"></script>
      </head>
      ```
> Extend knowledge from what we already know.
- Import `react` and `react-dom` in the same way as importing `jQuery`
  ```html
  <head>
    <script src="https://unpkg.com/browse/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/browse/react-dom@18/umd/react-dom.development.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script>
      const root = reactDom.createRoot(document.getElementById("root"));
      root.render(React.createElement("h1", null, "HelloWorld"));
    </script>
  </body>
  ```

  > `production.min.js` -> `development.js`

  > debug error in console from top to bottom.
  
  > The order of `<script>` tags.
- to use JSX, import babel
  > Three trustworthy google result: stackoverflow, doc, github
  ```html
  <head>
    <script src="https://unpkg.com/browse/react@18/umd/react.development.js"></script>
    <script src="https://unpkg.com/browse/react-dom@18/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/browse/babel-standalone@6.26.0/"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">
      const root = reactDom.createRoot(document.getElementById("root"));
      root.render(React.createElement("h1", null, "HelloWorld"));
    </script>
  </body>
  ```
- Learn `cli`, `npm`, `install`
  - 我们为什么使用 `npm` 管理 `package`
    - different version for different project
    - install dependency in project to make project portable
  - when to use `global`
    - When you install a tool into the system, such as `create-react-app`.
> Only read the documentation thoroughly when you need to refer to it.
- `webpack` / `rollup`
  - [https://webpack.js.org/](https://webpack.js.org/)
- boilerplate
> Knowledge is driven by code; learn when needed.
### webpack
- Concept
  - **Entry Points**: 
    - Specify one or more entry points where Webpack starts building the dependency graph of the application.

  - **Output**: 
    -Define where Webpack should emit the bundled files and how they should be named.
    
  - **Loaders**:
    - Loaders allow Webpack to process non-JavaScript files and transform them into modules that can be used by the application. For example, using a Babel loader can transform JavaScript files with ES6+ syntax into backward-compatible ES5 syntax.

  - **Plugins**:
    - Plugins can perform various tasks such as optimization, asset management, environment variable injection, etc. Webpack plugins extend the functionality of Webpack to meet specific requirements.

  - **Mode**:
    - Mode specifies the build mode of Webpack, which can be development, production, or none. Different modes trigger different built-in optimization strategies to meet the needs of either the development or production environment.

- `webpack.config.js`
  -   Configuration in Webpack refers to the setup and customization of the build process through a configuration file. This file, usually named `webpack.config.js`, contains various options and settings that define how Webpack should bundle the project's assets.


