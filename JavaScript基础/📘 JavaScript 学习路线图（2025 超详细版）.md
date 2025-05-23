# 📘 JavaScript 学习路线图（2025 超详细版）

> 本路线图结合当前主流开发风格，标注了 ✅必须掌握、⚠️了解即可、💡建议重点实践 的内容。

---

## 一、基础语法入门（零基础）

### ✅ 必学语法
- `let` / `const`（推荐） ⚠️ `var`（了解）
- 原始类型：`string` / `number` / `boolean` / `null` / `undefined` / `symbol` / `bigint`
- 引用类型：`Object` / `Array` / `Function`
- 运算符：算术、逻辑、比较、赋值、位运算
- 流程控制：`if` / `switch` / `for` / `while` / `for...of` / `for...in`
- **函数声明、表达式、箭头函数 `=>`**
- 参数默认值 / 剩余参数 `...args`
- **作用域、闭包（必学核心）**
- **`try...catch...finally`**
- **模块化：`script type="module"`**

---

## 二、核心机制理解（中级）

### ✅ 必学机制
- 执行上下文 & 作用域链
- 变量提升 / 函数提升（⚠️var 的副作用）
- `this` 绑定规则（默认 / 隐式 / 显式 / new）
- 原型与原型链（JS面向对象灵魂）
- 继承方式：组合继承、class继承
- **`call()` / `apply()` / `bind()`（常考）**
- 闭包作用与内存释放
- 垃圾回收机制（了解）

---

## 三、现代 ES6+ 语法（现代开发基础）

### ✅ 必学 ES6+ 特性
- 解构赋值（数组、对象）
- 模板字符串 `` `Hi ${name}` ``
- `let`、`const` 替代 `var`
- 箭头函数 `()=>`（注意 `this`）
- 对象字面量增强
- 展开运算符 `...` 和 `rest 参数`
- `Set` / `Map`（替代复杂对象处理）
- `class` / `extends` / `super`
- 模块化：`export` / `import`
- Promise（异步基础）
- async / await（异步主流）

### 💡 ES7 ~ ES13 常用语法（建议掌握）
- ES7：`includes()`、`**`（指数）
- ES8：`Object.entries`、`async/await`
- ES9：`Rest/Spread`、异步迭代器
- ES10+：`flat()`、`trimStart()`、可选链 `?.`、空值合并 `??`
- ES2024+：Temporal（新时间 API）

---

## 四、DOM 与事件操作（浏览器编程）

### ✅ 必学操作
- `document.querySelector()` / `getElementById()`
- DOM 修改：`innerHTML`、`style`、`classList`
- 节点操作：创建、添加、删除
- `addEventListener` 事件绑定
- 事件对象 `event`
- 冒泡 / 捕获机制
- 事件委托（高效事件绑定）

### ⚠️ 过时写法
- HTML 内联事件如 `onclick="..."`（不推荐）
- `document.write()`（淘汰）

---

## 五、BOM 与浏览器 API

### 💡 了解即可
- `window`、`location`、`navigator`
- 存储 API：
  - `localStorage` / `sessionStorage` ✅
  - `cookie`（了解）
- `setTimeout` / `setInterval`
- 页面跳转与刷新

---

## 六、异步编程与网络通信

### ✅ 异步基础
- 回调函数（callback）
- Promise（必须掌握）
- async / await（现代主流写法）
- 错误处理：try/catch + await

### ✅ 网络请求
- `fetch()` ✅（现代替代方案）
- `axios`（常用第三方库）
- HTTP 请求方法、状态码
- 跨域 / CORS 原理

---

## 七、模块化与工程化

### ✅ 模块体系
- ES Modules：`import` / `export` ✅
- CommonJS：`require` / `module.exports`（用于 Node）
- IIFE：立即执行函数（⚠️早期方案）

### ✅ 工程化工具
- 包管理：`npm` / `yarn` / `pnpm`
- 构建工具：`webpack`（传统） / `Vite`（现代推荐）
- 代码转译：`Babel`

---

## 八、面向对象与函数式编程

### ✅ OOP 基础
- `class` / `extends` / `super`
- 构造函数、静态方法、私有字段（`#`）
- 封装 / 继承 / 多态 模拟
- 设计模式（了解：工厂、单例、观察者）

### 💡 函数式思维
- 高阶函数
- 纯函数、不可变数据
- 柯里化、组合
- `map()` / `filter()` / `reduce()` ✅

---

## 九、框架中 JS 的实战运用

### 💡 框架相关
- Vue：
  - 响应式原理
  - 生命周期
  - `ref` / `reactive` / `computed`
- React：
  - 虚拟 DOM、JSX
  - hooks：`useState` / `useEffect` 等
- 状态管理：
  - Vuex / Pinia（Vue）
  - Redux / Zustand（React）

---

## 十、进阶技巧 & 面试手写题

### ✅ 必会实现
- `bind` / `call` / `apply` 实现
- `new` 运算符模拟
- `instanceof` 实现
- 深浅拷贝
- 节流 / 防抖
- 手写 Promise
- 发布订阅模式、EventEmitter
- 模拟实现 localStorage、JSON.stringify

### 💡 延伸学习
- AST 原理
- 浏览器渲染流程
- 性能优化

---

## ✅ 推荐学习资源

- 📖 文档类：
  - [MDN JavaScript](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
  - [JavaScript.info](https://javascript.info/)
- 📺 视频教程：
  - Bilibili: 网友整理的《现代 JavaScript 核心教程》
- 💻 在线练习：
  - [JSRun](https://jsrun.net)
  - [LeetCode](https://leetcode.cn/)
  - [牛客网](https://www.nowcoder.com/)

---

> ✨ 建议学习顺序：**基础语法 → 核心机制 → ES6+ → DOM & 异步 → 框架结合 → 手写实现 → 框架源码分析**