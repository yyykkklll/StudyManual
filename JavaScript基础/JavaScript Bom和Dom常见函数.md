# Bom Dom

---

## 一、BOM（Browser Object Model）概述

**BOM**是浏览器对象模型，允许JavaScript与浏览器窗口交互，操作浏览器的各种组件（如窗口、历史记录、屏幕等）。BOM没有正式标准，但各浏览器实现了一些通用的对象和方法。主要包括以下核心对象：

- **window**：全局对象，代表浏览器窗口。
- **navigator**：提供浏览器信息（如版本、用户代理）。
- **location**：控制浏览器URL和页面跳转。
- **history**：管理浏览器的历史记录。
- **screen**：提供屏幕信息（如分辨率）。

以下是BOM中最常用的方法和属性的讲解与示例：

### 1. window对象常用方法
`window`是BOM的核心，代表整个浏览器窗口。以下是几个常用方法：

#### (1) `window.alert()`
- **作用**：弹出一个简单的警告框，显示消息。
- **示例**：
```javascript
window.alert("欢迎学习JavaScript！");
// 弹出一个提示框，显示“欢迎学习JavaScript！”
```

#### (2) `window.prompt()`
- **作用**：弹出一个输入框，允许用户输入内容，返回输入的字符串。
- **示例**：
```javascript
let name = window.prompt("请输入你的名字：");
console.log("你输入的名字是：" + name);
// 用户输入名字后，控制台打印输入内容
```

#### (3) `window.confirm()`
- **作用**：弹出一个确认框，返回布尔值（true/false）。
- **示例**：
```javascript
let result = window.confirm("你确定要退出吗？");
if (result) {
    console.log("用户选择了确认");
} else {
    console.log("用户选择了取消");
}
// 根据用户选择，打印不同信息
```

#### (4) `window.setTimeout()`
- **作用**：在指定时间后执行一次函数。
- **示例**：
```javascript
setTimeout(() => {
    console.log("2秒后执行此消息");
}, 2000);
// 2秒后在控制台打印消息
```

#### (5) `window.setInterval()`
- **作用**：每隔指定时间重复执行函数。
- **示例**：
```javascript
let count = 0;
let timer = setInterval(() => {
    console.log("计数：" + count++);
    if (count > 3) clearInterval(timer); // 停止定时器
}, 1000);
// 每秒打印一次计数，4次后停止
```

#### (6) `window.open()`
- **作用**：打开一个新窗口或标签页。
- **示例**：
```javascript
window.open("https://www.example.com", "_blank");
// 在新标签页打开example.com
```

### 2. location对象常用方法和属性
`location`对象控制浏览器的URL和页面跳转。

#### (1) `location.href`
- **作用**：获取或设置当前页面的URL。
- **示例**：
```javascript
console.log(location.href); // 打印当前页面URL
location.href = "https://www.example.com"; // 跳转到新页面
```

#### (2) `location.reload()`
- **作用**：重新加载当前页面。
- **示例**：
```javascript
location.reload(); // 刷新当前页面
```

#### (3) `location.assign()`
- **作用**：加载新页面，与设置`location.href`类似。
- **示例**：
```javascript
location.assign("https://www.example.com"); // 跳转到指定页面
```

### 3. history对象常用方法
`history`对象管理浏览器的历史记录。

#### (1) `history.back()`
- **作用**：返回上一页，相当于点击浏览器的“后退”按钮。
- **示例**：
```javascript
history.back(); // 返回上一页
```

#### (2) `history.forward()`
- **作用**：前往下一页，相当于点击浏览器的“前进”按钮。
- **示例**：
```javascript
history.forward(); // 前往下一页
```

#### (3) `history.go()`
- **作用**：跳转到历史记录中的指定页面，正数向前，负数向后。
- **示例**：
```javascript
history.go(-2); // 返回前两页
```

### 4. navigator对象常用属性
`navigator`提供浏览器相关信息。

#### (1) `navigator.userAgent`
- **作用**：返回浏览器的用户代理字符串，用于判断浏览器类型。
- **示例**：
```javascript
console.log(navigator.userAgent);
// 打印类似："Mozilla/5.0 (Windows NT 10.0; Win64; x64)..."
```

#### (2) `navigator.language`
- **作用**：返回浏览器的语言设置。
- **示例**：
```javascript
console.log(navigator.language); // 打印类似："zh-CN"（中文）
```

### 5. screen对象常用属性
`screen`提供屏幕信息。

#### (1) `screen.width` 和 `screen.height`
- **作用**：获取屏幕的宽度和高度（像素）。
- **示例**：
```javascript
console.log(`屏幕分辨率：${screen.width} x ${screen.height}`);
// 打印屏幕分辨率，例如："1920 x 1080"
```

---

## 二、DOM（Document Object Model）概述

**DOM**是文档对象模型，表示HTML文档的树形结构，允许JavaScript动态操作网页内容、结构和样式。`document`对象是DOM的入口点，代表整个HTML文档。

DOM的核心功能包括：
- **查找元素**：通过ID、类、标签等获取DOM节点。
- **操作元素**：修改内容、属性、样式等。
- **创建和删除元素**：动态添加或移除DOM节点。
- **事件处理**：响应用户交互（如点击、输入）。

以下是DOM中最常用的方法和属性的讲解与示例：

### 1. 查找元素
以下方法用于在DOM树中查找节点。

#### (1) `document.getElementById()`
- **作用**：通过ID获取单个元素。
- **示例**：
```javascript
<div id="myDiv">Hello</div>
<script>
    let div = document.getElementById("myDiv");
    console.log(div.textContent); // 打印："Hello"
</script>
```

#### (2) `document.getElementsByClassName()`
- **作用**：通过类名获取元素集合（HTMLCollection）。
- **示例**：
```javascript
<div class="box">Box 1</div>
<div class="box">Box 2</div>
<script>
    let boxes = document.getElementsByClassName("box");
    console.log(boxes[0].textContent); // 打印："Box 1"
</script>
```

#### (3) `document.getElementsByTagName()`
- **作用**：通过标签名获取元素集合。
- **示例**：
```javascript
<p>Paragraph 1</p>
<p>Paragraph 2</p>
<script>
    let paragraphs = document.getElementsByTagName("p");
    console.log(paragraphs[1].textContent); // 打印："Paragraph 2"
</script>
```

#### (4) `document.querySelector()`
- **作用**：使用CSS选择器获取第一个匹配的元素。
- **示例**：
```javascript
<div class="box">Box</div>
<script>
    let box = document.querySelector(".box");
    console.log(box.textContent); // 打印："Box"
</script>
```

#### (5) `document.querySelectorAll()`
- **作用**：使用CSS选择器获取所有匹配的元素（NodeList）。
- **示例**：
```javascript
<div class="box">Box 1</div>
<div class="box">Box 2</div>
<script>
    let boxes = document.querySelectorAll(".box");
    boxes.forEach(box => console.log(box.textContent)); // 打印："Box 1", "Box 2"
</script>
```

### 2. 操作元素内容和属性
以下方法用于修改元素的内容或属性。

#### (1) `element.innerHTML`
- **作用**：获取或设置元素的HTML内容。
- **示例**：
```javascript
<div id="myDiv">Old content</div>
<script>
    let div = document.getElementById("myDiv");
    div.innerHTML = "<strong>New content</strong>";
    // 元素内容变为加粗的"New content"
</script>
```

#### (2) `element.textContent`
- **作用**：获取或设置元素的纯文本内容。
- **示例**：
```javascript
<div id="myDiv">Old text</div>
<script>
    let div = document.getElementById("myDiv");
    div.textContent = "New text";
    // 元素内容变为"New text"
</script>
```

#### (3) `element.getAttribute()`
- **作用**：获取元素的指定属性值。
- **示例**：
```javascript
<img id="myImg" src="image.jpg">
<script>
    let img = document.getElementById("myImg");
    console.log(img.getAttribute("src")); // 打印："image.jpg"
</script>
```

#### (4) `element.setAttribute()`
- **作用**：设置元素的指定属性值。
- **示例**：
```javascript
<img id="myImg" src="old.jpg">
<script>
    let img = document.getElementById("myImg");
    img.setAttribute("src", "new.jpg");
    // 图片的src属性变为"new.jpg"
</script>
```

### 3. 操作元素样式
以下方法用于修改元素的CSS样式。

#### (1) `element.style`
- **作用**：直接修改元素的内联样式。
- **示例**：
```javascript
<div id="myDiv">Styled div</div>
<script>
    let div = document.getElementById("myDiv");
    div.style.backgroundColor = "blue";
    div.style.color = "white";
    // 元素背景变为蓝色，文字变为白色
</script>
```

#### (2) `element.classList`
- **作用**：操作元素的类名（如添加、移除、切换）。
- **示例**：
```javascript
<style>
    .highlight { background-color: yellow; }
</style>
<div id="myDiv">Content</div>
<script>
    let div = document.getElementById("myDiv");
    div.classList.add("highlight"); // 添加highlight类
    div.classList.remove("highlight"); // 移除highlight类
    div.classList.toggle("highlight"); // 切换highlight类
</script>
```

### 4. 创建和删除元素
以下方法用于动态添加或移除DOM节点。

#### (1) `document.createElement()`
- **作用**：创建新元素。
- **示例**：
```javascript
let newDiv = document.createElement("div");
newDiv.textContent = "New Div";
document.body.appendChild(newDiv);
// 在body末尾添加一个新div，内容为"New Div"
```

#### (2) `element.appendChild()`
- **作用**：将子节点添加到指定父节点。
- **示例**：
```javascript
<div id="container"></div>
<script>
    let container = document.getElementById("container");
    let p = document.createElement("p");
    p.textContent = "New paragraph";
    container.appendChild(p);
    // 在container中添加一个p元素
</script>
```

#### (3) `element.remove()`
- **作用**：移除指定元素。
- **示例**：
```javascript
<div id="myDiv">Remove me</div>
<script>
    let div = document.getElementById("myDiv");
    div.remove();
    // div元素从DOM中移除
</script>
```

### 5. 事件处理
DOM支持通过事件与用户交互，以下是常用的方法。

#### (1) `element.addEventListener()`
- **作用**：为元素绑定事件监听器。
- **示例**：
```javascript
<button id="myButton">Click me</button>
<script>
    let button = document.getElementById("myButton");
    button.addEventListener("click", () => {
        console.log("按钮被点击！");
    });
    // 点击按钮后，控制台打印消息
</script>
```

#### (2) `element.removeEventListener()`
- **作用**：移除事件监听器。
- **示例**：
```javascript
<button id="myButton">Click me</button>
<script>
    let button = document.getElementById("myButton");
    let handler = () => console.log("按钮被点击！");
    button.addEventListener("click", handler);
    button.removeEventListener("click", handler); // 移除监听器
    // 移除后，点击按钮无反应
</script>
```

---

## 三、BOM与DOM的区别和联系

- **区别**：
  - **BOM**：操作浏览器窗口和功能（如弹窗、跳转页面、获取浏览器信息）。
  - **DOM**：操作网页的文档结构（如修改HTML内容、样式、处理事件）。
- **联系**：
  - 两者都通过`window`对象访问，`document`是`window`的一个属性。
  - BOM提供浏览器环境支持，DOM依赖于BOM的`document`对象来操作页面内容。

