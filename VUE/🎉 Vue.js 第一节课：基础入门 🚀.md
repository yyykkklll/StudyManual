# 🎉 Vue.js 第一节课：基础入门 🚀

欢迎开始学习 Vue.js！本节课将带你快速了解 Vue 的核心知识，帮你轻松上手。我们会逐步讲解每个重点，并配上简单示例，最后还有两个综合练习巩固你的成果！💪✨

------

## 1. 什么是 Vue，为什么选择它？🤔

### 什么是 Vue？

Vue.js 是一个 **渐进式 JavaScript 框架**，专注于构建用户界面（UI）。它轻量、灵活又高效，特别适合快速打造交互式网页应用。Vue 的核心库只关注视图层，方便与其他库或项目结合。

### 为什么选择 Vue？

- 🐣 **轻量**：核心包只有约 20KB，加载飞快！
- 🧑‍🎓 **易学**：语法直观，初学者友好，开发效率高。
- 🔄 **响应式**：数据变化自动更新视图，省时省力。
- 🌳 **生态丰富**：支持 Vue Router、Pinia、Vuex 等官方工具，适用范围广。
- 💬 **社区活跃**：文档完善，资源丰富，遇到问题轻松找到答案。

------

## 2. 创建 Vue 实例（使用 CDN）🌐

不想复杂安装？Vue 支持直接通过 CDN 引入，快速体验！试试这个示例：

```html
<!DOCTYPE html>
<html>
<head>
  <title>Vue 第一课</title>
  <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
  <div id="app">
    {{ message }}
  </div>

  <script>
    const { createApp } = Vue;
    createApp({
      data() {
        return {
          message: 'Hello, Vue! 👋'
        };
      }
    }).mount('#app');
  </script>
</body>
</html>
```

**说明：**

- 通过 `<script>` 引入 Vue。
- `createApp` 创建 Vue 应用。
- `mount('#app')` 把 Vue 绑定到页面元素。
- `data()` 返回的数据可以在模板中用 `{{ message }}` 显示。

------

## 3. 模板语法基础：插值 {{}}、v-bind、v-on 🖋️

### 插值 {{}}

用来显示数据，像这样：

```html
<div id="app">
  <p>欢迎你，{{ username }}！🎉</p>
</div>

<script>
  createApp({
    data() {
      return {
        username: 'Vue 小白'
      };
    }
  }).mount('#app');
</script>
```

------

### v-bind 动态绑定属性

动态绑定元素属性，比如图片地址：

```html
<div id="app">
  <img :src="imageUrl" alt="示例图片">
</div>

<script>
  createApp({
    data() {
      return {
        imageUrl: 'https://via.placeholder.com/150'
      };
    }
  }).mount('#app');
</script>
```

> 提示：`v-bind:src` 可以简写成 `:src`。

------

### v-on 绑定事件监听器

绑定点击等事件：

```html
<div id="app">
  <button @click="sayHello">点击我！✨</button>
</div>

<script>
  createApp({
    methods: {
      sayHello() {
        alert('Hello, Vue! 🎈');
      }
    }
  }).mount('#app');
</script>
```

> 提示：`v-on:click` 简写为 `@click`。

------

## 4. 响应式数据与 data() 💧

Vue 的核心魔法：数据变化时视图自动更新！

```html
<div id="app">
  <p>计数：{{ count }}</p>
  <button @click="count++">+1</button>
</div>

<script>
  createApp({
    data() {
      return {
        count: 0
      };
    }
  }).mount('#app');
</script>
```

------

## 5. 事件绑定与 methods 🔧

通过事件触发函数，动态更新页面：

```html
<div id="app">
  <p>{{ message }}</p>
  <button @click="changeMessage">点我变消息！</button>
</div>

<script>
  createApp({
    data() {
      return {
        message: 'Vue 真有趣！'
      };
    },
    methods: {
      changeMessage() {
        this.message = 'Vue 更棒了！🚀';
      }
    }
  }).mount('#app');
</script>
```

------

## 6. 双向绑定：v-model 🔄

让输入框和数据实时同步：

```html
<div id="app">
  <input v-model="inputText" placeholder="输入点什么吧~" />
  <p>你输入了：{{ inputText }}</p>
</div>

<script>
  createApp({
    data() {
      return {
        inputText: ''
      };
    }
  }).mount('#app');
</script>
```

------

## 7. 条件渲染：v-if vs v-show 👀

### v-if

根据条件决定元素是否渲染：

```html
<p v-if="isVisible">我出现了！✨</p>
<button @click="isVisible = !isVisible">切换显示</button>
```

### v-show

元素始终存在，用 CSS 控制显示：

```html
<p v-show="isVisible">我用 v-show 控制哦！👻</p>
<button @click="isVisible = !isVisible">切换显示</button>
```

**区别**：

- `v-if` 真正添加/删除元素，适合不频繁切换。
- `v-show` 只控制显示隐藏，切换快。

------

## 8. 列表渲染：v-for 📝

遍历数组渲染列表：

```html
<ul>
  <li v-for="item in items" :key="item.id">{{ item.name }}</li>
</ul>

<script>
  createApp({
    data() {
      return {
        items: [
          { id: 1, name: '🍎 苹果' },
          { id: 2, name: '🍌 香蕉' },
          { id: 3, name: '🍊 橙子' }
        ]
      };
    }
  }).mount('#app');
</script>
```

------

## 🏆 综合练习题

### 练习 1：计数器应用

- 显示数字（初始 0）。
- “+1”和“-1”按钮调整数字。
- 数字大于 5 时显示提示。
- 用到 `data`、`@click`、`methods`、`v-if`。

------

### 练习 2：待办事项列表

- 输入框输入事项内容。
- 点击“添加”按钮加入列表。
- 用 `v-for` 显示待办事项。
- 每项带“删除”按钮，能删除对应项。
- 用到 `v-model`、`v-for`、`@click`、`methods`。

------

## ✨ 总结

本节课带你了解了：

- Vue 是什么及其优势。
- 用 CDN 快速创建 Vue 应用。
- 模板语法（插值、v-bind、v-on）。
- 响应式数据和 `data()`。
- 事件绑定与 `methods`。
- 双向绑定 `v-model`。
- 条件渲染 `v-if` 和 `v-show`。
- 列表渲染 `v-for`。

完成练习后，欢迎试着自己动手写代码，感受 Vue 的魅力！下节课我们将深入组件系统与生命周期，敬请期待！🎉🎉🎉

------

