## 一、异步编程简介

JavaScript是单线程语言，异步编程用于处理耗时操作（如网络请求、文件读取、定时器等），避免阻塞主线程。**Promise**和**async/await**是解决异步问题的现代方案，取代了传统的回调函数，代码更清晰、可读性更高。

- **Promise**：一个表示异步操作最终完成或失败的对象，提供了链式调用和错误处理机制。
- **async/await**：基于Promise的语法糖，让异步代码看起来像同步代码，简化流程。

---

## 二、Promise详解

### 1. Promise基础
**Promise**是一个对象，表示一个异步操作的最终结果（成功或失败）。它有三种状态：
- **Pending（等待）**：初始状态，操作尚未完成。
- **Fulfilled（履行）**：操作成功完成，返回结果。
- **Rejected（拒绝）**：操作失败，返回错误。

Promise通过`new Promise()`创建，接收一个执行器函数，包含`resolve`（成功）和`reject`（失败）两个参数。

#### 示例：基本Promise
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        let success = true; // 模拟异步操作
        if (success) {
            resolve("操作成功！");
        } else {
            reject("操作失败！");
        }
    }, 1000);
});

promise.then(result => {
    console.log(result); // 1秒后打印："操作成功！"
}).catch(error => {
    console.log(error); // 如果失败，打印错误
});
```

### 2. Promise常用方法

#### (1) `Promise.then()`
- **作用**：处理Promise成功（Fulfilled）时的结果，接收一个回调函数。
- **示例**：
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("数据加载完成"), 1000);
});
promise.then(data => {
    console.log(data); // 打印："数据加载完成"
});
```

#### (2) `Promise.catch()`
- **作用**：捕获Promise失败（Rejected）时的错误。
- **示例**：
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => reject("数据加载失败"), 1000);
});
promise.catch(error => {
    console.log(error); // 打印："数据加载失败"
});
```

#### (3) `Promise.finally()`
- **作用**：无论Promise成功或失败，都会执行的回调。
- **示例**：
```javascript
let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("完成"), 1000);
});
promise
    .then(result => console.log(result)) // 打印："完成"
    .catch(error => console.log(error))
    .finally(() => console.log("无论成功或失败都执行")); // 打印此消息
```

#### (4) `Promise.all()`
- **作用**：接收一个Promise数组，当所有Promise都成功时返回结果数组；若任一失败，则返回第一个失败的错误。
- **示例**：
```javascript
let p1 = Promise.resolve("任务1完成");
let p2 = new Promise(resolve => setTimeout(() => resolve("任务2完成"), 1000));
let p3 = Promise.resolve("任务3完成");

Promise.all([p1, p2, p3]).then(results => {
    console.log(results); // 打印：["任务1完成", "任务2完成", "任务3完成"]
}).catch(error => console.log(error));
```

#### (5) `Promise.race()`
- **作用**：接收一个Promise数组，返回最先完成（成功或失败）的Promise结果。
- **示例**：
```javascript
let p1 = new Promise(resolve => setTimeout(() => resolve("慢任务"), 2000));
let p2 = new Promise(resolve => setTimeout(() => resolve("快任务"), 1000));

Promise.race([p1, p2]).then(result => {
    console.log(result); // 打印："快任务"（p2更快）
});
```

#### (6) `Promise.resolve()` 和 `Promise.reject()`
- **作用**：快速创建已解决或已拒绝的Promise。
- **示例**：
```javascript
Promise.resolve("立即成功").then(result => {
    console.log(result); // 打印："立即成功"
});

Promise.reject("立即失败").catch(error => {
    console.log(error); // 打印："立即失败"
});
```

### 3. Promise链式调用
Promise支持`.then()`链式调用，每个`.then()`返回一个新的Promise，方便处理连续的异步操作。

#### 示例：链式调用
```javascript
let promise = new Promise(resolve => {
    setTimeout(() => resolve(1), 1000);
});
promise
    .then(num => {
        console.log(num); // 打印：1
        return num + 1;
    })
    .then(num => {
        console.log(num); // 打印：2
        return num + 1;
    })
    .then(num => console.log(num)); // 打印：3
```

---

## 三、async/await详解

### 1. async/await基础
**async/await**是Promise的语法糖，简化异步代码的编写：
- **`async`**：声明一个异步函数，返回一个Promise。
- **`await`**：暂停异步函数执行，等待Promise解析（只能在async函数中使用）。

#### 示例：基本async/await
```javascript
async function fetchData() {
    let promise = new Promise(resolve => {
        setTimeout(() => resolve("数据获取成功"), 1000);
    });
    let result = await promise; // 等待Promise解析
    console.log(result); // 打印："数据获取成功"
}
fetchData();
```

### 2. 错误处理
使用`try...catch`捕获异步操作中的错误，替代Promise的`.catch()`。

#### 示例：错误处理
```javascript
async function fetchData() {
    try {
        let promise = new Promise((resolve, reject) => {
            setTimeout(() => reject("数据获取失败"), 1000);
        });
        let result = await promise;
        console.log(result);
    } catch (error) {
        console.log(error); // 打印："数据获取失败"
    }
}
fetchData();
```

### 3. 结合Promise.all()
`await`可以与`Promise.all()`结合，处理多个异步操作。

#### 示例：并行请求
```javascript
async function fetchMultiple() {
    let p1 = new Promise(resolve => setTimeout(() => resolve("数据1"), 1000));
    let p2 = new Promise(resolve => setTimeout(() => resolve("数据2"), 2000));
    let results = await Promise.all([p1, p2]);
    console.log(results); // 打印：["数据1", "数据2"]
}
fetchMultiple();
```

### 4. 实际应用：模拟API请求
以下是一个模拟从API获取数据的例子，展示async/await的实用性。

#### 示例：模拟API调用
```javascript
async function getUserData(userId) {
    try {
        let response = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
        let data = await response.json();
        console.log(data.name); // 打印用户姓名
    } catch (error) {
        console.error("获取数据失败：", error);
    }
}
getUserData(1); // 获取ID为1的用户数据
```

---

## 四、Promise与async/await的对比

| 特性         | Promise                       | async/await                  |
| ------------ | ----------------------------- | ---------------------------- |
| **语法**     | 链式调用（.then/.catch）      | 类似同步代码（try/catch）    |
| **可读性**   | 复杂时嵌套较多，回调地狱风险  | 代码更简洁，像写同步代码     |
| **错误处理** | 使用.catch()                  | 使用try/catch                |
| **并行处理** | Promise.all()、Promise.race() | 结合Promise.all()使用        |
| **适用场景** | 适合简单异步或需要链式操作    | 适合复杂逻辑，追求代码可读性 |

---

## 五、异步编程实用案例

以下是一个综合案例，结合Promise和async/await，模拟从多个API获取数据并处理。

```javascript
async function fetchPostsAndComments() {
    try {
        // 并行获取帖子和评论
        let [posts, comments] = await Promise.all([
            fetch("https://jsonplaceholder.typicode.com/posts").then(res => res.json()),
            fetch("https://jsonplaceholder.typicode.com/comments").then(res => res.json())
        ]);
        console.log("帖子数量：", posts.length); // 打印帖子数量
        console.log("评论数量：", comments.length); // 打印评论数量
    } catch (error) {
        console.error("获取数据失败：", error);
    }
}
fetchPostsAndComments();
```

---

