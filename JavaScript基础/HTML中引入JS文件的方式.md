# 在 HTML 中引入 JavaScript 有多种方式，主要可以分为以下几类：

---

## ✅ 1. **内联 JavaScript（Inline JavaScript）**

在 HTML 元素的事件属性中直接编写 JavaScript 代码。

```html
<button onclick="alert('Hello!')">点击我</button>
```

* **优点**：简单直观，适用于少量逻辑。
* **缺点**：不利于维护，不符合结构与行为分离的理念。

---

## ✅ 2. **嵌入式 JavaScript（Embedded JavaScript）**

在 `<script>` 标签中直接写入 JavaScript 代码，通常放在 HTML 文件的 `<head>` 或 `<body>` 中。

```html
<!DOCTYPE html>
<html>
<head>
  <title>嵌入式 JS 示例</title>
  <script>
    console.log("页面加载中...");
  </script>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

* **优点**：方便快速开发。
* **缺点**：HTML 和 JS 混杂，不利于模块化与复用。

---

## ✅ 3. **外部 JavaScript 文件（External JavaScript）**

通过 `<script src="路径">` 引入外部的 `.js` 文件。

```html
<!DOCTYPE html>
<html>
<head>
  <title>外部 JS 示例</title>
  <script src="main.js"></script>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

`main.js` 内容：

```javascript
console.log("这是外部 JS 文件！");
```

* **优点**：

  * 可复用；
  * 更易维护；
  * 实现 HTML 与 JS 的分离。
* **推荐做法**：将 `<script>` 标签放在 HTML 的底部或加 `defer`/`async` 来优化加载性能（见下面）。

---

## ✅ 4. **使用 `defer` 与 `async` 属性**

用于控制外部脚本加载与执行的时机：

### ✅ `defer`

```html
<script src="main.js" defer></script>
```

* 异步加载脚本，但**等待 HTML 全部解析完后再执行**；
* **执行顺序按在 HTML 中的顺序**；
* 适合大多数情况。

### ✅ `async`

```html
<script src="main.js" async></script>
```

* 异步加载脚本，加载完**立即执行**；
* 执行顺序**不确定**（与 HTML 中位置无关）；
* 一般用于第三方脚本（如广告、分析代码）。

---

## ✅ 5. **模块化 JavaScript（ES6 模块）**

通过 `<script type="module">` 引入模块，支持 `import/export` 语法。

```html
<script type="module" src="main.js"></script>
```

* `main.js` 中可使用 ES6 的模块化语法：

```javascript
import { sayHello } from './utils.js';
sayHello();
```

* **特点**：

  * 自动 `defer`；
  * 支持现代模块开发；
  * 推荐用于现代项目架构。

---

## 🔚 总结：常见场景选型建议

| 引入方式           | 使用场景              | 是否推荐   |
| -------------- | ----------------- | ------ |
| 内联事件           | 简单测试、教学           | ❌ 不推荐  |
| 嵌入式 `<script>` | 小型页面或快速原型         | ⚠️ 可用  |
| 外部脚本 `src`     | 生产项目、结构化开发        | ✅ 推荐   |
| `defer`        | 多脚本文件、DOM 操作      | ✅ 强烈推荐 |
| `async`        | 独立脚本（如广告、统计）      | ✅ 推荐   |
| ES6 模块         | 模块化开发、前端框架（Vue 等） | ✅ 推荐   |

