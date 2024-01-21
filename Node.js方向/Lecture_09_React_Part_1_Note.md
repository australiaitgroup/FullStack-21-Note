# Lecture 09 React (1)

## Description
本篇笔记以 Zhao Long 老师的 Lecture 09 React (Part 1) 随堂笔记
## Table of Content
- [ES6 回顾](#es6-回顾)  
- [高质量的代码](#高质量的代码)  
- [前端工程化](#前端工程化)  
- [React 的特性](#react-的特性)  
- [前端的大规模发展](#前端的大规模发展)
## ES6 回顾
### 数据类型
  1. 一般类型/基础类型: String, Number, Boolean, Null, Undefined
  2. 其他类型都是Object，包括：Object，如 Array, Function 
    - 使用 typeof 检查数据类型
  - 注意： 
    - `typeof function` 返回 `function` 而不是 `Object`
    - `console.log(myFunction instanceof Object)` 会返回 `true`
    - `typeof null` 返回 `Object`
### 变量提升
js会将变量和函数提升到顶部
- 提升内容
  - 使用var声明的变量会被提升，但只有声明部分被提升，初始化（赋值）不会被提升
  - 函数声明也会被提升，包括函数体。
- 不被提升的内容：函数表达式不会被提升
### this 
- 在JS中，this是一个特殊的关键字，他在函数被调用时自动定义，提供一个额外的方式来访问函数执行上下文(context)。
  - 是被调用时自动定义的
  - 谁调用就指向谁
- 基本使用场景
  - 全局上下文: 在非函数代码中，this只想全局对象（在浏览器中是window,在Node.js中是global，在严格模式下是undefined）
  - 函数上下文:在普通函数调用中，this 通常指向全局对象（非严格模式）或undefined（严格模式）
  - 对象方法：当函数作为对象的一个属性（即方法）被调用时，this指向这个对象
  - 构造函数：使用new调用函数时，this指向一个新创建的对象
  - 事件处理：在DOM事件处理中，this 通常指向触发事件的元素
  - 对象中里立即调用函数this指向window或global  
## 高质量的代码
> 雷军：我的代码写的想诗一样优雅
- 高质量代码：
  - 可读性 Readable，
  - 可维护性 Maintainable，
  - 可复用性 Reusable
  - 写符合人类思考方式的代码
    - 在写代码之前充分了解问题
    - 变量命名需要具有描述性
    - Don't repeat yourself
    - keep it simple, stupid
    - 不要为未来设计代码，不要添加当前不需要的功能
    - 即使代码已经工作，也应该回顾和改进
> 不要 Copy and Paste
- SOLID 原则
  - 单一职责原则 single responsiblity principle
    - 一个代码块只负责一项任务
  - 开放封闭原则 open/ clode principle
    - 对拓展开放，对修改封闭
  - 依赖注入原则 dependency injection principle
    - 一个代码块的依赖应该由外部注入，而不是耦合在实现逻辑里
## 前端工程化
- JavaScript(Vanilla JS | Node.js) 
  - Vanilla JS 是指原生 JS，不依赖任何外部库
- DOM：是前端向前发展的基石，没事的时候可以了解以下
- JQuery
  - 跨浏览器的兼容性
  - 简化的语法
  - 易用的AJAX语法
  - 强大的选择器引擎

## React 的特性
- Declarative 声明式
- Component-Based 组件化

### 命令式 与 声明式 Declarative 代码
- 命令式代码不符合 可读 可维护 可复用 的原则
- React是声明式代码
- 声明式是前端的根基

### 组件化 - 就像乐高积木
- 避免了 copy and paste
- 增加了代码复用

## 前端的大规模发展
### 前端的三驾马车
- React, Angular, VUE: 本质上都是基于声明式和组件化的实现
  - Angular是最复杂的
  - React 和 VUE 都提供了灵活性
  - React 因为社区发展的较早，拥有良好的生态


> next.js + tailwind css 是现在市场上的主流搭配 面试也需要会

