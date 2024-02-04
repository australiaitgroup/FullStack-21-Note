# Lecture 12 React（4）

## Description
本篇笔记以 Zhao Long 老师的 Lecture 12 React (Part 4) 随堂笔记
## Table of Content
- Table of Content
  - [复习](#复习)
  - [Children](#children)
  - [传递所有 Props (Spread Attributes)](#传递所有-props-spread-attributes)
  - [如何在 React 中应用 style](#如何在-react-中应用-style)

## 复习
- `Props` 是只读的，自顶向下流动的数据结构在 `tree view` 里非常方便 debug 和 维护。所有传递的东西是不能改变的，代码的维护性强。
- `props` 是 key value 的形式
- 子组件对于父组件应该是一个黑盒，符合 open/close 原则里的 close 部分，因为子组件的实现是对父组件隐藏的，封装了一个黑盒。技术实现细节和内容对外是不可见的。
- 反向数据流：子传父通过回调函数。符合 open/close 原则的 open 部分，open 出来接口和数据。
## Children
- `Children` 是一个特殊的 `prop`,他允许你在组建的开标前和闭标签之间插入内容，然后在组件内部通过 `props.children` 来访问
  ```jsx
  function MyComponent(props) {
    return <div>{props.children}</div>
  }
  ```
- 百度面试题
  ```jsx
  function Calculator(props){
    return (
      <div>
        <p>Input is <strong>{props.a}</strong>,<strong>{props.b}</strong></p>
        <p>result is <strong>{props.calculate(props.a, props.b)}</strong></p>
      </div>
    );
  }

  <Calculate a={a} b={b} calculate={(a, b) => a + b} />
  ```
- `children` 应该怎么用
  - `children` 可以传组件
    ```jsx
    <ChildComponent>
      <h1>Hello World</h1>
    </ChildComponent>
    ```
  - 使用 `props.children` 可以获取 Button 组件中间的文本
## 传递所有 Props (Spread Attributes)
- 你可以使用扩展运算符 `...` 来传递所有的 `props`
  ```jsx
  function MyComponent(props) {

    return <OtherComponent {...props} />
  }
  ```
## 如何在 React 中应用 style
#### 命名
- BEM
- 我们为什么写BEM:因为我们没办法快速实现一个可读的唯一 `className` 生成器
#### 应用 style
> 就近维护原则
  - 内联样式：不好读
  - 为了避免使用内联样式或者BEM，可以使用：CSS module, Styled Component, Tailwind CSS 三分天下
> 我们可以在 js 中写 css，是因为 bundler，而不是 compiler
#### 打包器 和 编译器
- 打包器 (比如 webpack)：将相应的内容打包到正确的地址
- 编译器（比如 babel）: 把不合法的JS通过一些列的方法，比如JSX编译成合法的JS
#### CSS Modules
- 使用CSS Modules是一种常见的方法，它允许你将CSS样式模块化，确保每个组件的样式在其作用域内。在使用CSS Modules时，你不太容易发生样式冲突，因为每个模块的样式都被封装在自己的作用域内。
- 如果使用了 CRA, 不需要自己配置 CSS Modules， 否则需要自己配置 CSS Modules
- 配置 Example：
  ```javascript
  // webpack.config.js

  module.exports = {
    // ...其他配置
    module: {
      rules: [
        {
          test: /\.module\.css$/,
          use: [
            'style-loader',
            {
              loader: 'css-loader',
              options: {
                modules: true,
              },
            },
          ],
        },
        // ...其他规则
      ],
    },
  };
  ```
- 原理：webpack 将 css 变成一个 object
  ```jsx
  if(/* 文件名end with .module.css */){
  // 进入这个 css，将这个 css 做成一个 object
  const styles = {
    '.container': `
      padding: 20px;
      background-color: #f0f0f0;
    `,
    '.button': `
      border: 0;
    `,
  }

  export styles
  }

  ```
  ```jsx
  // styles.module.css
  .button {
    // styles for the button
  }

  // ButtonComponent.jsx
  import React from 'react';
  import styles from './styles.module.css';

  const ButtonComponent = () => {
    return <button className={styles.button}>Click me</button>;
  };
  ```
#### styled component：用 JS 解决问题
- 初始安装
  ```
  # with npm
  npm install styled-components

  # with yarn
  yarn add styled-components
  ```
- Code Example
  ```jsx
  // Button.js
  import styled from 'styled-components';

  // Define a styled component
  const Button = styled.button`
    color: #fff;
    padding: 10px 15px;
    border: none;
    border-radius: 3px;
    background-color: ${(props) => props.color /* 传 props */}; 
    cursor: pointer;

    &:hover {
      background-color: #217dbb;
    }
  `;

  // Use the styled component in your React component
  export default Button;


  // App.js
  import React from 'react';
  import Button from './Button';

  const App = () => {
    return (
      <div>
        <h1>Hello Styled Components!</h1>
        <Button color="green" >Click Me!</Button>
      </div>
    );
  };

  export default App;
  ```
#### Tailwind CSS
> Tailwind CSS 也有学习成本，所以无法占据垄断地位

> 但是再也不用写很长的 CSS 了
- 初始安装
  ```
  npm install -D tailwindcss
  npx tailwindcss init
  ```
- 配置 `tailwind.config.js`
- Code Example
  ```jsx
  import React from 'react';

  const MyComponent = () => {
    return (
      <div className="bg-blue-500 text-white p-4">
        This is a component styled with Tailwind CSS.
      </div>
    );
  };

  export default MyComponent;
  ```
> CSS module, Styled Component, Tailwind CSS 三分天下
> 不要用 Material UI
