# JavaScript网络请求之fetch API

---

## 一、fetch API 简介

**`fetch`** 是现代JavaScript内置的API，用于发送HTTP请求（如GET、POST）并处理响应。它基于Promise，返回一个Promise对象，提供了简洁、灵活的方式来与服务器交互。相比`XMLHttpRequest`，`fetch`语法更简洁，支持Promise和async/await，易于错误处理和链式操作。

### 核心特点：
- 返回**Promise**，可与async/await结合。
- 支持多种HTTP方法（GET、POST、PUT、DELETE等）。
- 默认不发送cookie，需手动配置。
- 响应需要手动解析（如JSON、文本等）。

---

## 二、fetch 的基本用法

### 1. 基本语法
`fetch`函数接收两个参数：
- **url**：请求的目标地址（字符串）。
- **options**（可选）：配置对象，指定请求方法、头信息、请求体等。

返回一个Promise，解析为**Response**对象，包含响应状态、头信息和数据。

#### 示例：简单GET请求
```javascript
fetch("https://jsonplaceholder.typicode.com/users/1")
    .then(response => response.json()) // 解析为JSON
    .then(data => console.log(data.name)) // 打印用户姓名
    .catch(error => console.error("请求失败：", error));
```

#### 使用 async/await 重写
```javascript
async function getUser() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/users/1");
        let data = await response.json();
        console.log(data.name); // 打印用户姓名
    } catch (error) {
        console.error("请求失败：", error);
    }
}
getUser();
```

---

## 三、fetch 的常用方法和属性

以下是`fetch`及相关**Response**对象的常用方法和属性，涵盖最常见的使用场景。

### 1. fetch 请求配置（options）
`fetch(url, options)`的`options`对象用于定制请求，常用属性包括：

- **method**：HTTP方法（如`"GET"`、`"POST"`）。
- **headers**：请求头（如设置Content-Type）。
- **body**：请求体（POST/PUT请求时使用，需序列化为字符串）。
- **credentials**：控制是否发送cookie（`"omit"`、`"same-origin"`、`"include"`）。

#### 示例：发送POST请求
```javascript
async function createPost() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/posts", {
            method: "POST",
            headers: {
                "Content-Type": "application/json"
            },
            body: JSON.stringify({
                title: "New Post",
                body: "This is a new post",
                userId: 1
            })
        });
        let data = await response.json();
        console.log("创建的帖子：", data);
    } catch (error) {
        console.error("请求失败：", error);
    }
}
createPost();
```

### 2. Response 对象常用方法
`fetch`返回的`Response`对象包含响应信息，常用方法用于解析响应体：

#### (1) `response.json()`
- **作用**：将响应体解析为JSON对象。
- **示例**：
```javascript
fetch("https://jsonplaceholder.typicode.com/todos/1")
    .then(response => response.json())
    .then(data => console.log(data.title)); // 打印todo标题
```

#### (2) `response.text()`
- **作用**：将响应体解析为纯文本。
- **示例**：
```javascript
fetch("https://api.example.com/text")
    .then(response => response.text())
    .then(text => console.log(text)); // 打印文本内容
```

#### (3) `response.blob()`
- **作用**：将响应体解析为二进制数据（用于图片、文件等）。
- **示例**：
```javascript
async function getImage() {
    let response = await fetch("https://example.com/image.jpg");
    let blob = await response.blob();
    let img = document.createElement("img");
    img.src = URL.createObjectURL(blob);
    document.body.appendChild(img); // 显示图片
}
getImage();
```

#### (4) `response.ok`
- **作用**：布尔值，检查响应状态是否成功（状态码200-299）。
- **示例**：
```javascript
async function checkResponse() {
    let response = await fetch("https://jsonplaceholder.typicode.com/users/1");
    if (response.ok) {
        let data = await response.json();
        console.log("成功：", data);
    } else {
        console.error("请求失败，状态码：", response.status);
    }
}
checkResponse();
```

#### (5) `response.status`
- **作用**：获取HTTP状态码（如200、404）。
- **示例**：
```javascript
fetch("https://jsonplaceholder.typicode.com/invalid")
    .then(response => {
        console.log("状态码：", response.status); // 打印：404
    });
```

---

## 四、常见场景和模式

### 1. 处理多个请求（Promise.all）
使用`Promise.all`并行发送多个`fetch`请求，提高效率。

#### 示例：并行获取用户和帖子
```javascript
async function fetchData() {
    try {
        let [user, posts] = await Promise.all([
            fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json()),
            fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then(res => res.json())
        ]);
        console.log("用户：", user.name);
        console.log("帖子数量：", posts.length);
    } catch (error) {
        console.error("请求失败：", error);
    }
}
fetchData();
```

### 2. 设置请求头和认证
通过`headers`添加自定义头信息，如API密钥或认证令牌。

#### 示例：带认证的请求
```javascript
async function getProtectedData() {
    try {
        let response = await fetch("https://api.example.com/data", {
            headers: {
                "Authorization": "Bearer your-token-here"
            }
        });
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("请求失败：", error);
    }
}
getProtectedData();
```

### 3. 处理错误
`fetch`不会自动抛出HTTP错误（如404、500），需手动检查`response.ok`或`response.status`。

#### 示例：错误处理
```javascript
async function fetchWithErrorHandling() {
    try {
        let response = await fetch("https://jsonplaceholder.typicode.com/invalid");
        if (!response.ok) {
            throw new Error(`HTTP错误，状态码：${response.status}`);
        }
        let data = await response.json();
        console.log(data);
    } catch (error) {
        console.error("请求失败：", error.message);
    }
}
fetchWithErrorHandling();
```

### 4. 上传文件
使用`FormData`对象上传文件。

#### 示例：上传文件
```javascript
async function uploadFile(file) {
    let formData = new FormData();
    formData.append("file", file); // file是<input type="file">选择的文件

    try {
        let response = await fetch("https://api.example.com/upload", {
            method: "POST",
            body: formData
        });
        let result = await response.json();
        console.log("上传成功：", result);
    } catch (error) {
        console.error("上传失败：", error);
    }
}

// 示例调用（假设有一个文件输入框）
document.querySelector("input[type=file]").addEventListener("change", (event) => {
    uploadFile(event.target.files[0]);
});
```

---

## 五、fetch 的注意事项

1. **不自动抛出HTTP错误**：需检查`response.ok`或`response.status`。
2. **默认不发送cookie**：需设置`credentials: "include"`以发送cookie。
3. **跨域请求**：受CORS（跨源资源共享）限制，服务器需配置允许跨域。
4. **性能优化**：并行请求使用`Promise.all`，避免逐个等待。
5. **兼容性**：`fetch`在现代浏览器中广泛支持，但在IE中需使用polyfill。

---

## 六、实际案例：综合应用

以下是一个综合案例，展示如何使用`fetch`获取数据并动态更新DOM。

```javascript
async function displayUserPosts() {
    try {
        // 获取用户和帖子
        let [user, posts] = await Promise.all([
            fetch("https://jsonplaceholder.typicode.com/users/1").then(res => res.json()),
            fetch("https://jsonplaceholder.typicode.com/posts?userId=1").then(res => res.json())
        ]);

        // 更新DOM
        let container = document.createElement("div");
        container.innerHTML = `<h2>${user.name}的帖子</h2>`;
        posts.forEach(post => {
            let p = document.createElement("p");
            p.textContent = post.title;
            container.appendChild(p);
        });
        document.body.appendChild(container);
    } catch (error) {
        console.error("获取数据失败：", error);
    }
}
displayUserPosts();
```

