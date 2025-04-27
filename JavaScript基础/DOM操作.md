# DOM操作节点

------

# 什么是 DOM？

DOM（Document Object Model，文档对象模型）是**浏览器把网页（HTML）变成的一个对象模型**，可以让 JavaScript 访问和操作网页的内容、结构和样式。

简单说：**HTML页面 => 变成了对象 => 你可以用JS去读、改、加、删！**

------

# 操作元素节点（Element Nodes）

常见的操作可以分为：

- **查找元素**
- **修改元素内容**
- **修改元素属性**
- **修改元素样式**
- **添加新元素**
- **删除元素**

------

## 1. 查找元素

**方法：**

- `document.getElementById('id')`
- `document.getElementsByClassName('class')`
- `document.getElementsByTagName('tag')`
- `document.querySelector('选择器')`
- `document.querySelectorAll('选择器')`

**示例：**

```html
<div id="myDiv" class="box">Hello</div>
const div1 = document.getElementById('myDiv');  // 根据id查找
const div2 = document.querySelector('.box');    // 根据类名查找（只找第一个）
console.log(div1.textContent); // 输出: Hello
```

------

## 2. 修改元素内容

**方法：**

- `innerHTML`（可以解析HTML标签）
- `textContent`（只改文本，不解析HTML）

**示例：**

```javascript
const div = document.getElementById('myDiv');

// 改成带HTML的
div.innerHTML = '<strong>加粗文字</strong>';

// 只改文本
div.textContent = '纯文本内容';
```

------

## 3. 修改元素属性

**方法：**

- `element.setAttribute('属性名', '属性值')`
- `element.getAttribute('属性名')`
- 直接修改属性，比如 `element.href = 'xxx'`

**示例：**

```html
<a id="myLink" href="https://www.example.com">点我</a>
const link = document.getElementById('myLink');

// 修改链接地址
link.setAttribute('href', 'https://www.google.com');

// 也可以直接改
link.href = 'https://www.baidu.com';
```

------

## 4. 修改元素样式

**方法：**

- 直接操作 `style` 对象

**示例：**

```javascript
const div = document.getElementById('myDiv');

// 改变样式
div.style.color = 'red';
div.style.backgroundColor = 'yellow';
div.style.fontSize = '20px';
```

------

## 5. 添加新元素

**方法：**

- `document.createElement('标签名')`
- `父元素.appendChild(子元素)`

**示例：**

```javascript
// 创建一个新的 <p> 元素
const p = document.createElement('p');
p.textContent = '这是新添加的段落。';

// 把它加到 body 里
document.body.appendChild(p);
```

------

## 6. 删除元素

**方法：**

- `父元素.removeChild(子元素)`
- 或者用 `element.remove()`（更简单，兼容性好）

**示例：**

```javascript
const div = document.getElementById('myDiv');

// 方法一：传统方法
div.parentNode.removeChild(div);

// 方法二：现代方法（推荐）
div.remove();
```

------

# 总结小表格📋

| 目的     | 方法                                  |
| -------- | ------------------------------------- |
| 查找元素 | `getElementById()`、`querySelector()` |
| 改内容   | `innerHTML`、`textContent`            |
| 改属性   | `setAttribute()`、直接改属性          |
| 改样式   | `style.属性名`                        |
| 添加元素 | `createElement()` + `appendChild()`   |
| 删除元素 | `removeChild()`、`remove()`           |

------

