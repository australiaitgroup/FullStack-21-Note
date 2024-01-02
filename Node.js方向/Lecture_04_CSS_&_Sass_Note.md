# Lecture04 CSS & Sass
## Description
本篇笔记以Ally老师的 Lecture 04 CSS & Sass 为框架，根据W3School和MDN进行补充，旨在辅助21期全栈视频，帮助同学建立起基本的学习框架。

欲了解更多实际操作和详细内容，请参考文档。
## 目录
1. [1. CSS](#1-css)
    - [1.1 CSS中的长度单位](#11-css中的长度单位)
    - [1.2 Naming Convention in CSS](#12-naming-convention-in-css)
    - [1.3 用 Media Query 做响应式布局](#13-用-media-query-做响应式布局)
    - [1.4 Position](#14-position)
    - [1.5 Transition](#15-transition)
    - [1.6 z-index](#16-z-index)
    - [1.7 Grid](#17-grid)
2. [Sass](#2-sass)
    - [2.1 Sass Introduction](#21-sass-introduction)
    - [2.2 Sass Variables](#22-sass-variables)
    - [2.3 Nesting](#23-nesting)
    - [2.4 Mixin and Include](#24-mixin-and-include)
    - [2.5 Import and Partials](#25-import-and-partials)
    - [2.6 Extend and Inheritance](#26-extend-and-inheritance)
    - [2.7 Function](#27-function)
## 1. CSS
### 1.1 CSS中的长度单位
`rem`, `em`, `px`, `vh`, `vw`, `%`
- em 是相对于父元素的单位，用于设置元素的尺寸，例如 width、height、padding、margin。当应用于 font-size 时，em 是相对于该元素的父元素的 font-size。
- rem (用的最多)是一种广泛使用的相对单位，它始终相对于根元素（html）的 font-size。因此，rem 在整个文档中保持一致。
- px 通常用于设置边框（border）等较小的尺寸，或者在特定情况下用于定位元素。
- vh 和 vw 分别表示视窗的高度和宽度的百分比单位。
- 百分比（%）单位是相对于父元素的，可以用于设置宽度、高度等属性，使其相对于父元素的相应属性的百分比。

### 1.2 Naming Convention in CSS
BEM (块、元素、修饰符)：
- BEM 是一种命名约定，用于创建清晰且模块化的 CSS。
- 命名模式为块__元素--修饰符。
例如：
![css bem](./assets/images/css_bem.jpg)
> BEM只是所有命名方式其中一种流行命名方式  
> 工作中也有其他命名方式，具体看公司规定  
> 比如说在styled-components中 (一个用于构建 React 应用的流行的 CSS-in-JS库)
会使用驼峰命名法。

### 1.3 用 Media Query 做响应式布局
在实现响应式布局时，@media 查询是一种有用的CSS功能，允许根据设备的屏幕宽度或其他特征应用不同的样式。以适应手机，平板和pc。

```css
body {
    background-color: green;
}

/* 在最大宽度为 1200px 以下时应用的样式 */
@media (max-width: 1200px) {
    body {
        background-color: purple;
    }
}

/* 在最大宽度为 600px 以下时应用的样式 */
@media (max-width: 600px) {
    body {
        background-color: yellow;
    }
}
```

顺序的重要性： CSS是按照代码的顺序执行的，因此在编写@media查询时，顺序非常重要。确保更具体的查询在更一般的查询之前，这样样式表就能正确地覆盖。

### 1.4 Position
position 属性用于控制元素的定位方式：
- static： 默认值，元素按照标准流布局展示，即元素出现在文档流中的位置。
- relative： 相对于元素在标准流中的位置进行移动，但原来的标准流位置仍然占用。
    ```css
    div {
    width: 100px;
    height: 100px;
    position: relative;/*开启相对定位*/
    top: 100px;
    left: 100px;
    }
    /*上述例子表示元素向下和向右移动了100px。*/
    ```
  属性：用于在相对定位的元素中进行位置微调，使元素相对于其在标准文档流中的位置进行移动。
  - `top: 100px;` 向下移动 100px
  - `top: -100px;` 向上移动 100px
  - `right: 100px;` 向左移动 100px
  - `right: -100px;` 向右移动 100px
  - `bottom: 100px;` 向上移动 100px
  - `bottom: -100px;` 向下移动 100px
  - `left: 100px;` 向右移动 100px
  - `left: -100px;` 向左移动 100px

- absolute： 
  - 相对于最近的已定位（非 static 定位）祖先元素（absolute并不是相对自己定位），如果没有已定位的祖先元素，则相对于文档根元素（root element）进行定位。
  - 至少设置 left、top、right、bottom 中的一个，否则 absolute 不会生效。
- fixed： 相对于浏览器窗口进行定位，不占用原来的位置。常用于创建悬浮窗。
  ```css
  position: fixed;
  top: 0;
  left: 0;
  /*上述例子表示元素在向下滚动时，在距离父容器顶部20px的位置固定。*/
  ```

- sticky  

  当元素在视口中满足给定的偏移位置——然后它“粘”在视口中。
  ```css
  position: sticky;
  top: 20px;
  /*上述例子表示元素在向下滚动时，在距离父容器顶部20px的位置固定。*/
  ```
  必须设置top left right bottom 的其中一个， sticky 才生效。

### 1.5 Transition:

在CSS中，transition 是一种用来控制属性值在一定时间范围内平滑过渡的属性。它允许你在元素属性值发生变化时，使变化过程变得更加平滑和渐进，而不是突然改变。
语法：
```css
selector {
  transition: property duration timing-function delay;
}
```
Example
```css
.box {
  background-color: blue;
  transition: background-color 0.5s ease;
}

.box:hover {
  background-color: red;
}
```

- property：要过渡的CSS属性的名称，比如 color、opacity、transform 等。
- duration：过渡的持续时间，可以是秒(s)或毫秒(ms)。例如，1s 表示过渡时长为1秒。
- timing-function：过渡效果的时间函数，控制过渡过程中属性值的变化速度。常见的有 ease、linear、ease-in、ease-out 等。
- delay：延迟开始过渡的时间，同样可以是秒(s)或毫秒(ms)。


transition: 除了使用伪类，也可以通过使用js添加和删除 class 来控制transition何时生效

### 1.6 z-index 
z-index 是一个 CSS 属性，用于控制页面上元素的堆叠顺序（叠放顺序）。在 HTML 文档中，元素可以通过 z-index 属性来确定它们在堆叠上下文中的顺序，即哪个元素位于哪个元素的上方或下方。

注意事项：
- 只对定位元素有效： z-index 只对设置了定位属性（position 值为 relative、absolute 或 fixed）的元素有效。这是因为只有定位元素才会创建堆叠上下文。
- 同一堆叠上下文中比较： z-index 只有在同一堆叠上下文（stacking context）中才有意义。如果两个元素不在同一堆叠上下文中，它们的 z-index 值比较没有意义。
- 父子关系： 子元素的 z-index 值不会影响到父元素或其他同级元素的堆叠顺序。子元素的堆叠顺序是相对于父元素而言的。
- 层叠上下文： 某些属性和元素会触发新的层叠上下文，影响 z-index 的表现。例如，设置 transform、opacity、filter、will-change 等属性，或者使用一些 CSS 属性（如 flex、grid 等）的容器都可能创建新的层叠上下文。
- 工作中，如果一个z-index优先级最高，最大常设 999

### 1.7 Grid

css grid很强大  
工作中flex用的比grid多

flex是一维布局  
grid是二维布局

- 容器和项目

  ```html
  <div class="container">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
  ```
  - 对一个容器开启grid布局使用：`display: grid;`  

- 行和列
  - 容器里分为 row （水平） 和 column （垂直）
  - 使用 `grid-template-columns` 属性 `grid-template-rows` 来定义每一列的列宽
    Example
    ```css
    .container {
      display: grid;
      grid-template-columns: 100px 100px 100px;
      grid-template-rows: 100px 100px 100px;
    }
    ```
    - repeat() 函数用于重复网格行或列的模式。它接受两个参数：重复的次数和模板，如`grid-template-columns: repeat(3, 1fr);`
    - 属性值`auto-fill`，可以与 repeat() 结合使用，使网格容器自动填充网格项，以适应容器的宽度。这在响应式设计中非常有用。
    - 属性值 `fr`, 用于指定网格容器中剩余空间的等份分配。例如：`grid-template-columns: 1fr 2fr 1fr;`
    - 属性值`minmax()`，定义网格项的最小和最大尺寸。  
    
    Exapmle
    ```css
    grid-template-columns: repeat(auto-fill, 200px);
    grid-template-columns: 200px 1fr 2fr;
    grid-template-columns: 1fr 1fr minmax(300px, 2fr);

    grid-gap: 20px;
    grid-row-gap: 20px;
    grid-column-gap: 20px;

    grid-template-rows: 100px 200px; /*行高*/
    ```
  - 使用属性：`grid-row-gap` ，`grid-column-gap`，`grid-gap` 设置gap
  - 了解 justify-items、align-items、justify-self、align-self 等属性，它们可以用于控制网格容器和网格项的对齐方式。


    
一些flex的属性也可以用于CSS Grid，如 justify-content

## 2. Sass

### 2.1 Sass Introduction
Sass 是一个 CSS 预处理器。
其他预处理语言 less, SCSS(Sass和SCSS都是同一项目的两种语法变体，)

为什么使用Sass
- 可以减少 CSS 的重复书写，从而节省时间。
- 提供简单的逻辑计算方程
- 开启了模块化的可能性

HTML无法处理Scss，所以只在开发阶段使用，并使用VS code插件或包将Scss文件编译成CSS文件  
推荐使用的插件: Live Sass Compoiler

### 2.2 Sass Variables
设置变量以复用和方便修改
Syntax:
```SCSS
$myFont: Helvetica, sans-serif;
$myColor: red;
$myFontSize: 18px;
$myWidth: 680px;

p {
    color: $myColor;
    font-size: $myFontSize;
}
```
作用域: Sass 变量仅在定义它们的嵌套级别可用。

### 2.3 Nesting
Sass lets you nest CSS selectors in the same way as HTML.

Example
将以下CSS代码改写为Sass
```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```
改写的Sass代码
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

### 2.4 Mixin and Include
使用 @mixin 指令，可以创建可复用代码（块）。  
使用 @include 指令插入已创建的可复用代码（块）。

Example  

```scss
@mixin customised-mixin-name {
  property: value;
  property: value;
}

div {
  @include customised-mixin-name;
}
```

### 2.5 Import and Partials
@import  
The @import directive allows you to include the content of one file in another.
```scss
@import reset;
@import colors;
```
Partials  
默认情况下，Sass 直接转译所有 .scss 文件。然而，当你想要 导入文件时，不需要直接转译该文件。  
如果你的文件名以下划线开头，Sass 将不会转译它。

### 2.6 Extend and Inheritance

使用 @extend 将一组代码从一个选择器共享到另一个选择器  
Example
```scss
.button-basic  {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  @extend .button-basic;
  background-color: red;
}
```
> The @extend directive helps keep your Sass code very DRY.(Don't Repeat Yourself)

### 2.7 Function

Sass和SCSS中的函数（Functions）允许你在样式表中执行计算、操作数据以及生成动态的样式。Sass的函数可以用于生成值，例如颜色、数字、字符串等。：
1. 内置函数: SCSS内置了许多函数，用于处理颜色、数学运算、字符串等。
    Example: SCSS内置darken，和 round函数
    ```scss
    $color: darken(#3498db, 10%);
    $result: round(5.7);
    ```
2. 自定义函数： 使用@function关键字创建自定义函数。  
    Example
    ```scss
    // 定义自定义函数
    @function add-margin($value) {
    @return $value + 10px;
    }

    // 使用自定义函数
    .box {
    margin: add-margin(20px);
    }

    //margin 为 30px
    ```
