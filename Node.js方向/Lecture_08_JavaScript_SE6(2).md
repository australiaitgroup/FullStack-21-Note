# lecture 8 JS SE6(2)
## Description
这篇笔记是 Mason 老师 Lecture 08 JS ES6 课程的随堂笔记，请结合老师 [github的note](https://github.com/LazeBear/jr-fullstack-notes-21/blob/master/ES6/note.md) 一起看：
## Table of Content
  - [异步函数](#异步函数)
  - [Symbol](#symbol)
  - [模块化](#模块化)
## 异步函数
- 重要概念
  - `Promise`
  - `then` 和 `catch`
  - `async`/`await`
  - `try` 和 `catch`
  - `Promise.race() `
  - `Promise.all()`
- `Promise` 是一种用于处理异步操作的对象。
  - 它有三个状态：`pending`（进行中）、`fulfilled`（已成功）、`rejected`（已失败）。
  - 一个 `Promise` 对象表示一个异步操作的最终完成（或失败）及其结果值。
  - `Promise` 可以帮助解决回调地狱（Callback Hell）的问题。
   ```javascript
   let myPromise = new Promise((resolve, reject) => {
     // 使用setTimeout模拟异步操作
     setTimeout(() => {
         resolve("success");
        // 或者 reject("fail");
     }, 1000);
   });

   myPromise //可以使用then catch 或 async await 处理 Promise 对象的解决（成功）和拒绝（失败）的结果
     .then((result) => {
       console.log(result);
     })
     .catch((error) => {
       console.error(error);
     });
   ```

- `async`/`await`（只是语法糖）
  - `async` 函数返回一个`Promise`对象，可以使用`await`等待`Promise`的解决或拒绝。`async`函数使得异步代码看起来更像同步代码。

   ```javascript
   async function myAsyncFunction() {
  // 使用 async处理 Promise 对象的解决（成功）和拒绝（失败）的结果
  // 使用 try catch 处理可能的错误
     try {
       let result = await myPromise;
       console.log(result);
     } catch (error) {
       console.error(error);
     }
   }

   myAsyncFunction();
   ```
`then` 和 `catch` 是 `Promise` 对象提供的两个方法，用于处理异步操作的结果（解决或拒绝）。

- `then` 和 `catch` 方法
  - `then` 方法用于注册在 `Promise` 对象解决时（状态变为 `fulfilled`）执行的回调函数。它接受两个参数：第一个参数是解决时的回调函数，第二个参数是拒绝时的回调函数（可选）。
  - `catch` 方法用于注册在 `Promise` 对象被拒绝时（状态变为 `rejected`）执行的回调函数。
  - `catch`可以抓住前面任意一个`then`发生错误或`rejected`
  - 两个`catch`叠加在一起大多数情况下是没什么用的，但也不排除前面这个`catch`发生错误的情况
  ```javascript
  let myPromise = new Promise((resolve, reject) => {
    // 异步操作
    setTimeout(() => {
      let success = true; // 或者 false
      if (success) {
        resolve("操作成功");
      } else {
        reject("操作失败");
      }
    }, 1000);
  });

  myPromise.then(
    (result) => {
      console.log("成功:", result);
    },
    (error) => {
      console.error("失败:", error);
    }
  );
  ```

  - 在链式调用中，`then` 方法还可以返回一个新的 `Promise` 对象，以实现链式调用的异步操作。

   ```javascript
   myPromise
     .then((result) => {
       console.log("成功:", result);
       return "新的解决值";
     })
     .then((newResult) => {
       console.log("新的成功:", newResult);
     })
     .catch((error) => {
       console.error("失败:", error);
     });
   ```
- `Promise.race()`
  - `Promise.race()` 方法用于在多个`Promise`对象中，只要有一个`Promise`对象的状态变更，就返回该`Promise`的结果或错误。即，只要有一个`Promise`解决或拒绝，race就会立即返回。
  - `promise race()` 不太会用到，了解就行了
    ```javascript
    let promise1 = new Promise((resolve) => setTimeout(() => resolve('Promise 1'), 2000));
    let promise2 = new Promise((resolve, reject) => setTimeout(() => reject('Promise 2'), 1000));

    Promise.race([promise1, promise2])
      .then((result) => console.log(result))
      .catch((error) => console.error(error));
    ```

- `Promise.all()`
  - `Promise.all()` 方法用于等待所有`Promise`对象解决后，返回一个包含所有解决值的数组。如果任何一个`Promise`对象被拒绝，则整个`Promise.all`被拒绝。
  - `promise all()` 要知道，工作中可能会用到，

    ```javascript
    let promise3 = new Promise((resolve) => setTimeout(() => resolve('Promise 3'), 1500));
    let promise4 = new Promise((resolve) => setTimeout(() => resolve('Promise 4'), 2000));

    Promise.all([promise3, promise4])
      .then((results) => console.log(results))
      .catch((error) => console.error(error));
    ```
## Symbol
- 什么是 `Symbol`
  - ES6 新的数据类型
  - 唯一标识符
    ```js
    // 可以使用 Symbol 构造函数来创建 Symbol 实例。如果你想要创建两个具有相同描述的不同 Symbol，可以使用相同的描述字符串作为参数来调用 Symbol 构造函数。尽管描述相同，但每个 Symbol 实例都是唯一的，因此它们不相等。
    const symbol1 = Symbol('mySymbol');
    const symbol2 = Symbol('mySymbol');

    console.log(symbol1 === symbol2); // 输出 false
    ```
  - 私有性： Symbol 的描述（参数）仅用于调试和标识，不影响 Symbol 的唯一性。因此，Symbol 可以用作对象的属性，用来创建私有成员，因为其他代码很难获取到相同描述的 Symbol。
  - 应用场景少，主要用于创建对象的私有属性，以防止属性被不同模块或代码直接访问修改。一般在写library或framework时才会使用到
## 模块化
- 独立的模块提高了可复用性和可维护性
- 使用模块需要在 html的`<script>  </script>`标签中添加 `type='module'`
  ```js
  <script type="module" src="./index.js"></>
  // 现代浏览器支持
  // 但旧的浏览器可能有兼容性问题
  ```
- 导出方式：
  - 命名导出
  - 默认导出 `export default` ，每一个模块只能有一个默认导出

