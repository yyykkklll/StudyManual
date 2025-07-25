# 详细的 JavaScript 学习细化规划

------

## 🧱 一、JavaScript 基础语法（2~3天）

| 小节       | 要点                                                         | 说明                               |
| ---------- | ------------------------------------------------------------ | ---------------------------------- |
| 变量声明   | `let` / `const`                                              | `var` 跳过，强调块级作用域         |
| 数据类型   | 基本类型（string, number, boolean, null, undefined, symbol, bigint），引用类型（object, array, function） | Vue 中常处理对象与数组             |
| 字符串操作 | 模板字符串（`Hello ${name}`）、常用方法：`split()`、`includes()`、`trim()`、`toLowerCase()` 等 | 模板拼接用于 DOM 和 Vue            |
| 运算符     | `==` vs `===`，逻辑运算符 `&&                                |                                    |
| 流程控制   | `if`、`switch`、`for`、`while`、`do-while`、`break/continue` | Vue 的指令如 `v-if` 与这些逻辑相关 |

------

## 📦 二、数组与对象（重点，3~5天）

### ✅数组操作（Vue 中频繁用于列表渲染）

| 方法                          | 用法                         |
| ----------------------------- | ---------------------------- |
| `forEach()`                   | 遍历数组                     |
| `map()`                       | 生成新数组（常用于 UI 渲染） |
| `filter()`                    | 过滤数组元素                 |
| `reduce()`                    | 聚合计算（统计、求和）       |
| `find()`、`some()`、`every()` | 条件查找                     |

📌 **Vue 中用 map + key 渲染列表，用 filter 控制展示**

### ✅对象操作

| 特性                                       | 描述                                          |
| ------------------------------------------ | --------------------------------------------- |
| 解构赋值                                   | `const { name, age } = person`                |
| 简写                                       | `const person = { name, age }`                |
| 访问方式                                   | 点操作 `obj.key` 和中括号 `obj["key"]`        |
| `Object.keys()` / `values()` / `entries()` | 遍历对象键值对                                |
| 拷贝与合并                                 | `Object.assign({}, obj1, obj2)` / `...扩展符` |

📌 **Vue 的 props、data、computed 都涉及对象结构**

------

## 🔁 三、函数与作用域（3~4天）

### ✅核心知识：

| 特性                             | 用法与说明                                                   |
| -------------------------------- | ------------------------------------------------------------ |
| 函数声明 & 表达式                | 区别了解即可，推荐写法为 const + 箭头函数                    |
| 箭头函数 `=>`                    | 简洁、this 绑定不变，非常适合回调函数                        |
| 参数默认值 / rest 参数 `...args` | 提升函数的灵活性                                             |
| 回调函数                         | 用于事件处理、异步编程、数组方法                             |
| 作用域                           | 函数作用域 & 块级作用域，`let` 和 `const` 是块级             |
| 闭包                             | 了解闭包是如何“记住”函数作用域的变量                         |
| this                             | 浏览器/箭头函数/事件绑定中 this 的区别：Vue 会自动处理，大多数时候用箭头函数就对了 |

📌 可跳过：

- `arguments` 对象（用不到）
- 手动 `bind()` / `call()` / `apply()`（了解用途，不练）

------

## 🧩 四、DOM 操作与事件系统（3~4天）

Vue 其实封装了 DOM，但你必须理解其底层逻辑。

### ✅必须掌握：

| 类别     | 内容                                                    |
| -------- | ------------------------------------------------------- |
| 获取元素 | `document.querySelector()` / `getElementById()` 等      |
| 修改内容 | `innerText` / `innerHTML` / `textContent`               |
| 修改样式 | `element.style` / `classList.add/remove/toggle`         |
| 创建元素 | `createElement()` / `appendChild()` / `remove()`        |
| 事件绑定 | `addEventListener`（点击、输入、提交等）                |
| 事件对象 | `event.target`、`preventDefault()`、`stopPropagation()` |

📌 Vue 会简化事件绑定为 `@click` 等形式，但你必须知道原理！

📌 可跳过：

- `attachEvent`、IE 兼容方法
- `innerHTML` 安全性原理（了解即可）

------

## ⏳ 五、异步编程：Promise + async/await（3~4天）

这是 Vue 中处理 Ajax、组件生命周期的核心内容。

### ✅必须掌握：

| 概念                   | 内容                                       |
| ---------------------- | ------------------------------------------ |
| 回调地狱               | 多层回调嵌套，代码难维护（为引出 Promise） |
| Promise 概念           | `new Promise((resolve, reject) => {...})`  |
| `.then()` / `.catch()` | 链式调用异步流程                           |
| `async` / `await`      | 同步写法表达异步逻辑                       |
| 错误处理               | `try...catch` 中处理 `await` 错误          |
| fetch                  | 替代 XMLHttpRequest 的现代接口             |

📌 Vue 项目中大量使用 `async setup()`、接口获取、异步计算、加载控制。

📌 可跳过：

- XMLHttpRequest
- Generator 函数（高级内容）
- 手写 Promise 实现（非必要）

------

## 📦 六、模块化、ES6 语法增强（2~3天）

| 特性             | 内容                                                |
| ---------------- | --------------------------------------------------- |
| import/export    | `import` 模块、`export default` 或 `export const`   |
| 解构赋值         | 函数参数、数组、对象解构                            |
| 扩展运算符 `...` | 复制数组/对象，传参                                 |
| 模板字符串       | 多用于 Vue 模板拼接                                 |
| Set / Map        | Vue 组件状态管理或缓存机制时可用，了解常用 API 即可 |

------

## 💡 七、工具函数与开发习惯（可穿插）

| 实用技巧      | 说明                                       |
| ------------- | ------------------------------------------ |
| 节流/防抖     | 页面滚动、搜索框防止频繁触发               |
| 深拷贝/浅拷贝 | Vue2 的响应式与对象引用密切相关            |
| JSON 操作     | `JSON.stringify()` / `JSON.parse()`        |
| 本地存储      | `localStorage` / `sessionStorage`          |
| 调试技巧      | `console.log()`、断点调试、Chrome DevTools |

------

## 📋 整体学习建议与顺序安排（建议顺序）：

```text
基础语法 → 数组与对象 → 函数与作用域 → DOM操作 → 异步编程 → 模块化与ES6 → 工具函数
```

### 🚀 实战配合练习：

每学完一个模块，就配套做一个练手项目，例如：

- 学完数组 → 做一个 Todo List
- 学完 DOM → 实现一个模态框 + 表单验证
- 学完异步 → 做一个天气查询工具（调用 API）

------

