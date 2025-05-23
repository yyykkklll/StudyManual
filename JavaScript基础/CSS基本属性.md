# **CSS 常见属性** 

------

## 🧱 一、布局相关属性

### 1.1 `display` - 控制元素的显示类型

```css
/* 常见取值 */
display: block;       /* 块级元素 */
display: inline;      /* 行内元素 */
display: inline-block;/* 行内块元素 */
display: flex;        /* 弹性布局 */
display: grid;        /* 网格布局 */
```

### 1.2 `position` + `top/right/bottom/left` - 定位

```css
position: static;   /* 默认值 */
position: relative; /* 相对定位 */
position: absolute; /* 绝对定位 */
position: fixed;    /* 固定定位 */
position: sticky;   /* 粘性定位 */

top: 10px;
left: 20px;
```

### 1.3 `z-index` - 控制层级

```css
z-index: 10;
```

### 1.4 `float` 和 `clear` - 浮动布局

```css
float: left;
clear: both;
```

------

## 📏 二、尺寸与盒子模型

### 2.1 `width` / `height` / `max-` / `min-`

```css
width: 200px;
height: auto;
max-width: 100%;
min-height: 300px;
```

### 2.2 `margin` / `padding` - 外边距 / 内边距

```css
margin: 10px 20px;
padding: 15px 10px 5px 0;
```

### 2.3 `border` - 边框

```css
border: 1px solid #000;
border-radius: 8px;
```

### 2.4 `box-sizing` - 盒模型设置

```css
box-sizing: border-box; /* 推荐 */
```

------

## 🎨 三、文字与字体样式

### 3.1 `font-family` / `font-size` / `font-weight` / `font-style`

```css
font-family: "Arial", sans-serif;
font-size: 16px;
font-weight: bold;
font-style: italic;
```

### 3.2 `text-align` / `text-decoration` / `line-height` / `letter-spacing`

```css
text-align: center;
text-decoration: underline;
line-height: 1.5;
letter-spacing: 0.05em;
```

------

## 🎨 四、颜色与背景

### 4.1 `color` / `background-color`

```css
color: #333;
background-color: #f0f0f0;
```

### 4.2 `background-image` / `background-size` / `background-position`

```css
background-image: url("bg.jpg");
background-size: cover;
background-position: center;
```

------

## 🧭 五、弹性布局（Flexbox）

```css
display: flex;
flex-direction: row;        /* 横向排列 */
justify-content: center;    /* 主轴对齐 */
align-items: center;        /* 交叉轴对齐 */
gap: 10px;
```

------

## 🧱 六、网格布局（Grid）

```css
display: grid;
grid-template-columns: repeat(3, 1fr);
grid-gap: 20px;
```

------

## 🧩 七、伪类和伪元素

```css
/* 伪类 */
a:hover {
  color: red;
}

li:first-child {
  font-weight: bold;
}

/* 伪元素 */
p::before {
  content: "→ ";
}
```

------

## 🌀 八、动画与过渡

### 8.1 `transition` - 过渡动画

```css
transition: all 0.3s ease;
```

### 8.2 `transform` - 变形

```css
transform: scale(1.2) rotate(15deg);
```

### 8.3 `animation` - 关键帧动画

```css
@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

div {
  animation: fadeIn 1s ease-in-out;
}
```

------

## 🔐 九、其他常用属性

### 9.1 `overflow`

```css
overflow: hidden;
```

### 9.2 `visibility` 和 `opacity`

```css
visibility: hidden; /* 占位置但不可见 */
opacity: 0.5;       /* 透明度 */
```

### 9.3 `cursor`

```css
cursor: pointer;
```

------

