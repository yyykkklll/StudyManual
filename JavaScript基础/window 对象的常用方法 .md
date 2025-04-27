# window 对象的常用方法 

------

### 1. `window.alert()`

弹出一个提示框。

```javascript
window.alert('欢迎来到我的网站！');
```

------

### 2. `window.confirm()`

弹出一个带有确定和取消按钮的对话框，返回 `true` 或 `false`。

```javascript
const result = window.confirm('你确定要退出吗？');
if (result) {
    console.log('用户点击了确定');
} else {
    console.log('用户点击了取消');
}
```

------

### 3. `window.prompt()`

弹出一个提示框，要求用户输入内容。

```javascript
const name = window.prompt('请输入你的名字：');
console.log('你好，' + name);
```

------

### 4. `window.open()`

打开一个新的浏览器窗口或标签页。

```javascript
const newWindow = window.open('https://www.example.com', '_blank');
```

------

### 5. `window.close()`

关闭当前窗口（只能关闭由 `window.open()` 打开的窗口）。

```javascript
const myWindow = window.open('https://www.example.com', '_blank');
// 关闭新窗口
myWindow.close();
```

------

### 6. `window.setTimeout()`

延迟一段时间后执行某个函数（只执行一次）。

```javascript
window.setTimeout(() => {
    console.log('3秒后执行的代码');
}, 3000);
```

------

### 7. `window.setInterval()`

每隔一段时间重复执行某个函数。

```javascript
const intervalId = window.setInterval(() => {
    console.log('每2秒执行一次');
}, 2000);

// 停止定时器（通常在某个条件下停止）
window.setTimeout(() => {
    window.clearInterval(intervalId);
}, 10000); // 10秒后停止
```

------

### 8. `window.clearTimeout()`

取消 `setTimeout()` 创建的定时任务。

```javascript
const timeoutId = window.setTimeout(() => {
    console.log('不会执行到这行');
}, 5000);

// 立即取消
window.clearTimeout(timeoutId);
```

------

### 9. `window.scrollTo()`

滚动窗口到指定位置。

```javascript
// 滚动到页面顶部
window.scrollTo(0, 0);

// 滚动到 500px 位置
window.scrollTo({
    top: 500,
    behavior: 'smooth' // 平滑滚动
});
```

------

### 10. `window.location`

虽然 `location` 是一个对象，但经常以 `window.location.href` 这样的方法操作页面跳转。

```javascript
// 跳转到一个新页面
window.location.href = 'https://www.example.com';
```

------

