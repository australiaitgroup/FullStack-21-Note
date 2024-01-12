# Lecture 06 JavaScript ES6 

## Desciption
- 本篇笔记是 Mason 老师 Lecture 06 JS ES6 的随堂笔记
- 老师 [github 的 note 链接](https://github.com/LazeBear/jr-fullstack-notes-21/blob/master/ES6/note.md)：
## Table of Content
- [什么是ES6](#什么是es6)  
- [ES6 新语法 和一些补充知识点](#es6-新语法-和一些补充知识点)  
  - [`var` vs `let` and `const`](#var-vs-let-and-const)
  - [Template String](#template-string)
  - [Spread operator](#spread-operator)
  - [Destructuring](#destructuring)
  - [增强的对象字面量](#增强的对象字面量)
  - [this和词法作用域](#this和词法作用域)
  - [Function](#function)
  - [原型](#原型)
  - [Promise](#promise)
  - [iterators and generators](#iterators-and-generators)
## 什么是ES6
- ECMAScript 6（ES6）于2015年发布。它引入了许多新的语法特性、标准库和改进，以提高开发人员的生产力和代码的可维护性。ES6引入的一些重要特性包括箭头函数、模板字符串、解构赋值、类、let 和 const 等变量声明方式、以及Promise等异步编程的改进。

- ES6的新特性在旧版本的浏览器中并不一定被完全支持。为了确保向后兼容性，开发者通常使用工具如Babel来将使用ES6语法编写的代码转换为更早版本的JavaScript。

## ES6 新语法 和一些补充知识点

### `var` vs `let` and `const`
- var, let, const
    - var 和 let 在 for 循环中有不同的行为。var 声明的变量在整个函数作用域内都是可见的，而 let 在每次迭代中都会创建一个新的块级作用域。这在使用异步调用回调函数时可能会导致不同的结果，因为 var 的作用域是函数作用域，而 let 的作用域是块级的。
    
      ```js
      // Example
      var arr = [10, 12, 15, 21]
      for (var i = 0; i < arr.length; i++){
        setTimeout(function () {
          console.log('Index:' + i + ', element: ' + arr[i]);
        }, 1000);
      }
      /*
      Index:4, element: undefined
      Index:4, element: undefined
      Index:4, element: undefined
      Index:4, element: undefined
      */ 
      ```
      ```js
      var arr = [10, 12, 15, 21]

      for (let i = 0; i < arr.length; i++){
        setTimeout(function () {
          console.log('Index:' + i + ', element: ' + arr[i]);
        }, 1000);
      }
      // 会按照预期的方式输出每个元素的值
      ```
    - const 可以使用给基本数据类型并使用全大写变量名 
    - 初学者如果分不清何时使用const，学习过程中可以尽量用const 直到报错再改成 let
- 块级作用域 和 函数级作用域
  - 块级作用域：使用 let 和 const 声明的变量具有块级作用域。块级作用域是指变量仅在声明它的块或语句中可见，并在块外部不可访问。块级作用域常见于花括号 {} 包围的代码块，例如 if 语句、for 循环等。
  - 使用 var 声明的变量具有函数级作用域。函数级作用域是指变量在整个函数中可见，而在函数外部不可访问。但if语句和for循环的{}对var不起作用。
- Re-declare and update
  - var：使用 var 声明的变量可以在同一作用域内被多次声明，而不会引发错误。这种情况下，后续的声明会覆盖之前的声明。
  - let ：使用 let 声明的变量在同一作用域内不能被多次声明。尝试重新声明会导致错误。
    ```js
    let fruit = 'apple';
    // let fruit = "pear"; // Uncaught SyntaxError: Identifier 'fruit' has already been declared
    fruit = 'grape';
    console.log(fruit); // grape
    ```

### Template String
- 模板字符串
  - 模板字符串是JavaScript中一种字符串的创建方式，通过反引号``包裹，允许使用${}嵌入变量或表达式。
    ```js
      console.log(`The price is ${price}`)
    ```

  - 语法：在形参后面加一个 `=`
    ```js
    function greet(name = "Guest") {
    console.log(`Hello, ${name}!`);
    }
    ```
  - 如果传入参数过多，我们可以把他变成一个对象，实际开发中更常见
### Spread operator
- Spread Operator
  - 传参时 spread operator `...` 尽量放在前面，不然有可能覆盖前面的
  - 也可以用于捕获多余参数
### Destructuring
- 对象解构赋值：
  ```js
  const person = { name: 'John', age: 30, city: 'New York' };

  // 从对象中提取值并赋值给变量
  const { name, age, city } = person;

  console.log(name); // 输出: John
  console.log(age);  // 输出: 30
  console.log(city); // 输出: New York
  ```
- 数组解构赋值：
  ```js
  const numbers = [1, 2, 3, 4, 5];

  // 从数组中提取值并赋值给变量
  const [first, second, , fourth] = numbers;

  console.log(first);  // 输出: 1
  console.log(second); // 输出: 2
  console.log(fourth); // 输出: 4
  ```
- 解构赋值语法使用了花括号 {} 来对对象进行解构，使用方括号 [] 对数组进行解构。被提取的变量名要与对象或数组中的属性名或索引相匹配。
- 可以解构多层object和array

### 增强的对象字面量
- 增强的对象字面量
  - 属性的简写 - 非常常见
    ```js
    // 传统方式
    const x = 10;
    const y = 20;
    const point = { x: x, y: y };

    // 增强的对象字面量，属性的简写
    const point = { x, y };
      ```
  - 方法的简写 - 非常常见
    ```js
    // 增强的对象字面量，方法的简写
    const obj = {
      sayHello() {
        console.log("Hello!");
      }
    };
    ```
  - 动态属性，少见，但也会有 - 比如大量重复的数据
    ```js
    const data = ["name", "age", "city"];

    // 使用动态属性
    const person = {};
    for (let key of data) {
      person[key] = "Unknown";
    }
    ```
### this和词法作用域
- `this`的词法作用域，静态作用域，在代码还没有运行之前就确定下来了，让我们的行为变得可以追溯
- `call()`, `apply()`, `bind()`可以更改`this`指向。但现在很少用，只有在做library开发和ES6之前，人为改动`this`指向的时候才会用
### Function
- 高阶函数
  - 高阶函数是指能够接受一个或多个函数作为参数，并且/或者返回一个新函数的函数。它们提供了一种抽象层次，使得能够更灵活、可复用地操作函数行为。
- 箭头函数
  - 箭头函数对 `this` 的行为有影响，他们有自己的`this`指向，他的`this`是包裹他的函数的`this`
  - 工作中使用函数的时候，默认使用箭头函数。因为他避免动态`this`带来的一些问题。但也有特殊情况，比如说绑定事件的时候。 
### 原型
- 原型 `prototype` 工作的时候不会用，但面试的时候会问
- Set 和 Map 
  - Set 
    - Uniqueness:Set 是一种集合数据结构，它主要用于存储唯一的值，确保集合中的每个元素都是唯一的。
  - Map 
    - Key value pair: Map 是 JavaScript 中的一种集合数据结构，它以键值对（key-value pairs）的形式存储数据。在 Map 中，每个键对应一个值，且键可以是任意数据类型，包括基本数据类型和对象引用。
### Promise
- 什么是 Promise
  - promise  是 JavaScript 中一种用于处理异步操作的对象，它表示一个在未来某个时间点会产生结果的操作，解决回调函数的回调地狱。
- Promise 有三种状态，它们分别是
  - Pending（进行中）:
      - 初始状态，表示异步操作尚未完成，Promise 处于等待状态。
  - Fulfilled（已完成）:
      - 表示异步操作成功完成，Promise 被解决，且有一个结果值。
  - Rejected（已拒绝）:
      - 表示异步操作失败或出错，Promise 被拒绝，且有一个拒绝原因（错误信息）。
  - 一个 Promise 可以从 Pending 状态转变为 Fulfilled 状态，也可以从 Pending 状态转变为 Rejected 状态。一旦状态转变，就不会再改变。一个已经 Fulfilled 或 Rejected 的 Promise 称为 settled（已定型）。
- Promise Example
  ```js
  // 使用 Promise 处理异步操作
  const promiseExample = new Promise((resolve, reject) => {
    // 异步操作
    const isOperationSuccessful = true;

    if (isOperationSuccessful) {
      resolve("Operation succeeded!");
    } else {
      reject(new Error("Operation failed!"));
    }
  });

  promiseExample
    .then(result => {
      console.log("Fulfilled:", result);
    })
    .catch(error => {
      console.error("Rejected:", error.message);
    });
    
    // catch 只抓取这条链上他之前的错误

    // 也可以使用 async await 方法
  async function handlePromiseExample() {
    try {
      const result = await promiseExample;
      console.log("Fulfilled:", result);
    } catch (error) {
      console.error("Rejected:", error.message);
    }
  }

  handlePromiseExample();
  ```
### iterators and generators
- 开发中并不用
  - 可以使用旧的方法，更容易理解，更容易维护
  - 公司的大部分人可能也不会用这个东西，他们会很难做code review
- 一般认为写 while loop 是不太好的，因为一般避免写这种没有ending的loop，一定要写的话要写一个可以跳出循环的条件判断
execute context
