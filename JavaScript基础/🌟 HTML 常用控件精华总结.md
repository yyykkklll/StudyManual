# 🧱 HTML 常见元素全总结（含示例）

> ✅ 每个元素配一个最基本的使用案例，方便快速掌握。

------

## 📦 布局与结构元素

### `<div>` – 通用容器（无语义）

```html
<div>这是一个容器</div>
```

### `<section>` – 语义化内容区域

```html
<section>
  <h2>新闻</h2>
  <p>这里是新闻内容</p>
</section>
```

### `<header>` / `<footer>` – 页头 / 页尾

```html
<header>网站标题</header>
<footer>版权信息</footer>
```

### `<main>` – 页面主要内容

```html
<main>
  <h1>文章正文</h1>
</main>
```

### `<article>` – 独立内容块

```html
<article>
  <h2>博客文章标题</h2>
  <p>博客内容...</p>
</article>
```

### `<nav>` – 导航链接区域

```html
<nav>
  <a href="/">首页</a>
  <a href="/about">关于</a>
</nav>
```

------

## 📝 文本相关元素

### `<h1>` ~ `<h6>` – 标题（h1 最大）

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
```

### `<p>` – 段落

```html
<p>这是一段文本内容。</p>
```

### `<span>` – 行内文本容器（无语义）

```html
<span style="color:red">高亮文字</span>
```

### `<strong>` / `<em>` – 强调 / 斜体

```html
<strong>加粗内容</strong>
<em>倾斜内容</em>
```

### `<br>` – 换行

```html
一行<br>换行了
```

------

## 🔗 链接与媒体

### `<a>` – 超链接

```html
<a href="https://example.com">访问网站</a>
```

### `<img>` – 图片

```html
<img src="image.jpg" alt="描述文字">
```

### `<video>` – 视频播放

```html
<video src="video.mp4" controls></video>
```

### `<audio>` – 音频播放

```html
<audio src="audio.mp3" controls></audio>
```

------

## 📋 列表元素

### `<ul>` / `<ol>` / `<li>` – 无序/有序列表

```html
<ul>
  <li>苹果</li>
  <li>香蕉</li>
</ul>
<ol>
  <li>第一步</li>
  <li>第二步</li>
</ol>
```

------

## 🧾 表格元素

### `<table>` / `<tr>` / `<td>` / `<th>`

```html
<table>
  <tr>
    <th>姓名</th>
    <th>年龄</th>
  </tr>
  <tr>
    <td>张三</td>
    <td>18</td>
  </tr>
</table>
```

------

## ✅ 表单控件元素（重点）

### `<form>` – 表单容器

```html
<form action="/submit" method="post"></form>
```

### `<input>` – 文本输入、密码、单选、复选等

```html
<input type="text" placeholder="用户名">
<input type="password" placeholder="密码">
<input type="radio" name="gender" value="male"> 男
<input type="checkbox" name="agree"> 同意
```

### `<textarea>` – 多行文本输入

```html
<textarea rows="4">输入内容</textarea>
```

### `<select>` / `<option>` – 下拉框

```html
<select>
  <option value="1">选项一</option>
</select>
```

### `<button>` – 按钮

```html
<button type="submit">提交</button>
```

------

## 🔧 元信息和结构标签

### `<!DOCTYPE html>` – 声明文档类型

```html
<!DOCTYPE html>
```

### `<html>` / `<head>` / `<body>`

```html
<html>
  <head>
    <title>网页标题</title>
  </head>
  <body>
    页面内容
  </body>
</html>
```

### `<meta>` – 页面元信息

```html
<meta charset="UTF-8">
```

### `<link>` – 外部资源链接（如 CSS）

```html
<link rel="stylesheet" href="style.css">
```

### `<script>` – 脚本

```html
<script src="main.js"></script>
```

------

## 📌 常用全局属性（适用于几乎所有元素）

| 属性名     | 作用示例                            |
| ---------- | ----------------------------------- |
| `id`       | 唯一标识符 `<div id="box">`         |
| `class`    | 类名 `<p class="info">`             |
| `style`    | 内联样式 `<span style="color:red">` |
| `title`    | 鼠标悬停提示 `<a title="跳转">`     |
| `hidden`   | 隐藏元素 `<div hidden>`             |
| `disabled` | 禁用控件 `<input disabled>`         |

------

