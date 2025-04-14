# JavaScript 的变量类型及作用域

JavaScript 中有两种主要的数据类型分类：**基本类型（Primitive Types）**和**引用类型（Reference Types）**。以下是所有的类型：

## 一.变量类型

### **1. 基本类型（Primitive Types）**

这些类型直接存储值，不可变（immutable），在内存中占用固定大小。

- **Number（数字）**  
  表示整数或浮点数。
  - 示例：`42`, `3.14`

- **String（字符串）**  
  表示文本，用单引号、双引号或反引号包裹。
  - 示例：`"hello"`, `'world'`, `` `hi` ``

- **Boolean（布尔值）**  
  表示真或假，只有 `true` 和 `false` 两个值。
  - 示例：`true`, `false`

- **Undefined（未定义）**  
  表示变量已声明但未赋值，默认值。
  - 示例：`let x; // x 是 undefined`

- **Null（空值）**  
  表示“无值”或“空对象引用”，需要手动赋值。
  - 示例：`null`

- **Symbol（符号，ES6 引入）**  
  表示唯一且不可变的值，通常用于对象属性的唯一标识。
  - 示例：`Symbol("id")`

- **BigInt（大整数，ES2020 引入）**  
  表示任意精度的整数，用 `n` 结尾。
  - 示例：`12345678901234567890n`

### **2. 引用类型（Reference Types）**
这些类型存储的是值的引用（内存地址），可变（mutable），通常是复杂数据结构。

- **Object（对象）**  
  键值对集合，包括普通对象、数组、函数等。
  - 示例：`{ name: "小明" }`, `[1, 2, 3]`, `function() {}`

### **3.对象子类型**

- **Array（数组）**：有序列表，继承自 `Object`。
- **Function（函数）**：可执行的代码块，也是对象。
- **Date（日期）**、**RegExp（正则表达式）** 等内置对象。

## 二.如何声明变量

JavaScript 提供了三种声明变量的关键字：`var`、`let` 和 `const`，它们决定了变量的作用域和行为。

###  **1.使用 `var` 声明**
- **特点**：函数作用域，存在变量提升（hoisting），可重复声明。
- **语法**：`var 变量名 = 值;`

**示例**
```javascript
var name = "小明";
console.log(name); // 输出: 小明

var name = "小红"; // 重复声明覆盖
console.log(name); // 输出: 小红
```

### **2.使用 `let` 声明**
- **特点**：块级作用域，无变量提升，可重新赋值。
- **语法**：`let 变量名 = 值;`

**示例**
```javascript
let age = 25;
age = 26; // 可以重新赋值
console.log(age); // 输出: 26

// let age = 30; // 报错：不能重复声明
```

### 3. **使用 `const` 声明**
- **特点**：块级作用域，无变量提升，值不可重新赋值（但对象内部属性可变）。
- **语法**：`const 变量名 = 值;`

**示例**
```javascript
const pi = 3.14;
// pi = 3.14159; // 报错：不能重新赋值
console.log(pi); // 输出: 3.14

const person = { name: "小刚" };
person.name = "小李"; // 对象属性可以修改
console.log(person.name); // 输出: 小李
```

## 三.变量的作用域（Scope）

作用域决定了变量的可访问范围。JavaScript 中有以下几种作用域：

### **1.全局作用域（Global Scope）**
- 定义在任何函数或块之外的变量，任何地方都可以访问。
- 使用 `var`、`let` 或 `const` 声明的全局变量会绑定到 `window`（浏览器中）或 `global`（Node.js 中）。

**示例**
```javascript
var globalVar = "我是全局的";
function test() {
  console.log(globalVar);
}
test(); // 输出: 我是全局的
```

### **2.函数作用域（Function Scope）**
- 使用 `var` 声明的变量只在定义它的函数内有效。
- `let` 和 `const` 不受此限制（它们用块级作用域）。

**示例**
```javascript
function sayHello() {
  var message = "你好";
  console.log(message); // 输出: 你好
}
sayHello();
console.log(typeof message); // 输出: undefined（message 不可访问）
```

## 四.变量提升（Hoisting）

`var` 声明的变量会被提升到函数顶部，但赋值不会提升。

```javascript
function test() {
  console.log(x); // 输出: undefined
  var x = 10;
}
test();
```

## 五.块级作用域（Block Scope）

- 使用 `let` 和 `const` 声明的变量只在 `{}` 块内有效（如 `if`、`for`）。
- `var` 无块级作用域。

**示例**
```javascript
if (true) {
  var a = 1;     // 函数或全局作用域
  let b = 2;     // 块级作用域
  const c = 3;   // 块级作用域
}
console.log(a);    // 输出: 1
console.log(typeof b); // 输出: undefined
console.log(typeof c); // 输出: undefined
```

**示例**：循环中的作用域
```javascript
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// 输出: 3 3 3（var 是函数作用域，循环结束后 i = 3）

for (let j = 0; j < 3; j++) {
  setTimeout(() => console.log(j), 1000);
}
// 输出: 0 1 2（let 是块级作用域，每次循环有独立 j）
```

## 六.类型检测

可以用 `typeof` 操作符检查变量类型。

**示例**

```javascript
console.log(typeof 42);          // "number"
console.log(typeof "hello");     // "string"
console.log(typeof true);        // "boolean"
console.log(typeof undefined);   // "undefined"
console.log(typeof null);        // "object"（历史遗留问题）
console.log(typeof Symbol("id")); // "symbol"
console.log(typeof 123n);        // "bigint"
console.log(typeof { name: "小明" }); // "object"
console.log(typeof [1, 2, 3]);   // "object"
console.log(typeof function() {}); // "function"
```

## 七.综合示例

```javascript
// 全局变量
const appName = "我的应用";

// 函数作用域
function createUser() {
  var userId = 1001; // 函数作用域

  // 块级作用域
  if (true) {
    let userName = "小红"; // 块级作用域
    const userAge = 20;   // 块级作用域
    console.log(`${appName} 创建用户: ID=${userId}, 名字=${userName}, 年龄=${userAge}`);
  }

  console.log(userId);      // 输出: 1001
  console.log(typeof userName); // 输出: undefined
}

createUser();
```

**输出**
```
我的应用 创建用户: ID=1001, 名字=小红, 年龄=20
1001
undefined
```

## 八.总结

| 类型      | 示例           | 特点             |
| --------- | -------------- | ---------------- |
| Number    | `42`, `3.14`   | 数字，整数或浮点 |
| String    | `"hi"`         | 文本             |
| Boolean   | `true`         | 真假值           |
| Undefined | `undefined`    | 未赋值           |
| Null      | `null`         | 空值             |
| Symbol    | `Symbol("id")` | 唯一标识         |
| BigInt    | `123n`         | 大整数           |
| Object    | `{}`           | 键值对集合       |

| 声明方式 | 作用域    | 可否重新赋值 | 变量提升 |
| -------- | --------- | ------------ | -------- |
| `var`    | 函数/全局 | 是           | 是       |
| `let`    | 块级      | 是           | 否       |
| `const`  | 块级      | 否           | 否       |

---

## **练习**
1. 声明几个变量（用 `var`、`let`、`const`），分别赋值不同类型（数字、字符串、对象等），用 `typeof` 检查类型。
2. 写一个函数，里面用 `var` 和 `let` 声明变量，测试它们的作用域差异。

完成后可以给我看代码，我帮你检查！接下来想学什么？类型转换、运算符，还是其他？