# JavaScript字符串

---

### 一、字符串的基本概念
字符串可以用单引号（`'`）、双引号（`"`）或反引号（`` ` ``）创建：
```javascript
let str1 = "Hello";
let str2 = 'World';
let str3 = `Hello, ${str2}!`; // 模板字符串，支持插值
console.log(str3); // 输出: "Hello, World!"
```
字符串的长度可以通过 `length` 属性获取：
```javascript
let str = "JavaScript";
console.log(str.length); // 输出: 10
```

---

### 二、字符串的常用方法
以下是 JavaScript 中字符串的常用方法，按照功能分类并附上示例：

#### 1. **访问和提取字符串**
- **`charAt(index)`**  
  返回指定索引处的字符。如果索引无效，返回空字符串。
  
  ```javascript
  let str = "Hello";
  console.log(str.charAt(1)); // 输出: "e"
  console.log(str.charAt(5)); // 输出: ""（超出范围）
  ```
  
- **`charCodeAt(index)`**  
  返回指定索引处的字符的 Unicode 编码。如果索引无效，返回 `NaN`。
  
  ```javascript
  let str = "Hello";
  console.log(str.charCodeAt(0)); // 输出: 72（"H" 的 Unicode 编码）
  console.log(str.charCodeAt(5)); // 输出: NaN
  ```
  
- **`slice(start, end)`**  
  提取字符串的一部分并返回新字符串（end 不包含）。不修改原字符串。
  ```javascript
  let str = "JavaScript";
  console.log(str.slice(0, 4)); // 输出: "Java"
  console.log(str.slice(4));    // 输出: "Script"（从索引 4 到末尾）
  ```

- **`substring(start, end)`**  
  类似于 `slice`，但不支持负索引，且如果 `start > end`，会自动交换参数。
  ```javascript
  let str = "JavaScript";
  console.log(str.substring(0, 4)); // 输出: "Java"
  console.log(str.substring(4, 0)); // 输出: "Java"（自动调整顺序）
  ```

- **`substr(start, length)`**  
  从指定索引开始提取指定长度的子字符串。
  ```javascript
  let str = "JavaScript";
  console.log(str.substr(4, 6)); // 输出: "Script"
  ```

---

#### 2. **搜索和查找**
- **`indexOf(searchValue, start)`**  
  返回指定子字符串第一次出现的索引，未找到返回 -1。
  ```javascript
  let str = "Hello World";
  console.log(str.indexOf("World")); // 输出: 6
  console.log(str.indexOf("xyz"));   // 输出: -1
  ```

- **`lastIndexOf(searchValue, start)`**  
  返回指定子字符串最后一次出现的索引，未找到返回 -1。
  ```javascript
  let str = "Hello Hello World";
  console.log(str.lastIndexOf("Hello")); // 输出: 6
  ```

- **`includes(searchValue, start)`**  
  判断字符串是否包含指定子字符串，返回布尔值。
  ```javascript
  let str = "Hello World";
  console.log(str.includes("World")); // 输出: true
  console.log(str.includes("xyz"));   // 输出: false
  ```

- **`startsWith(searchValue, start)`**  
  判断字符串是否以指定子字符串开头，返回布尔值。
  ```javascript
  let str = "Hello World";
  console.log(str.startsWith("Hello")); // 输出: true
  console.log(str.startsWith("World")); // 输出: false
  ```

- **`endsWith(searchValue, end)`**  
  判断字符串是否以指定子字符串结尾，返回布尔值。
  ```javascript
  let str = "Hello World";
  console.log(str.endsWith("World")); // 输出: true
  console.log(str.endsWith("Hello")); // 输出: false
  ```

---

#### 3. **修改和转换**
- **`toLowerCase()`**  
  将字符串转换为小写，不修改原字符串。
  ```javascript
  let str = "Hello World";
  console.log(str.toLowerCase()); // 输出: "hello world"
  console.log(str);               // 输出: "Hello World"（原字符串不变）
  ```

- **`toUpperCase()`**  
  将字符串转换为大写，不修改原字符串。
  ```javascript
  let str = "Hello World";
  console.log(str.toUpperCase()); // 输出: "HELLO WORLD"
  ```

- **`trim()`**  
  移除字符串两端的空白字符，不修改原字符串。
  ```javascript
  let str = "   Hello World   ";
  console.log(str.trim()); // 输出: "Hello World"
  ```

- **`trimStart()`**  
  移除字符串开头的空白字符。
  ```javascript
  let str = "   Hello World";
  console.log(str.trimStart()); // 输出: "Hello World"
  ```

- **`trimEnd()`**  
  移除字符串末尾的空白字符。
  ```javascript
  let str = "Hello World   ";
  console.log(str.trimEnd()); // 输出: "Hello World"
  ```

- **`replace(searchValue, newValue)`**  
  替换第一个匹配的子字符串，返回新字符串。
  ```javascript
  let str = "Hello World";
  console.log(str.replace("World", "JavaScript")); // 输出: "Hello JavaScript"
  ```

- **`replaceAll(searchValue, newValue)`**  
  替换所有匹配的子字符串，返回新字符串。
  ```javascript
  let str = "Hello Hello World";
  console.log(str.replaceAll("Hello", "Hi")); // 输出: "Hi Hi World"
  ```

- **`padStart(targetLength, padString)`**  
  在字符串开头填充指定字符，直到达到目标长度。
  ```javascript
  let str = "5";
  console.log(str.padStart(3, "0")); // 输出: "005"
  ```

- **`padEnd(targetLength, padString)`**  
  在字符串末尾填充指定字符，直到达到目标长度。
  ```javascript
  let str = "5";
  console.log(str.padEnd(3, "0")); // 输出: "500"
  ```

---

#### 4. **分割和连接**
- **`split(separator)`**  
  将字符串按指定分隔符分割成数组。
  ```javascript
  let str = "apple,banana,orange";
  let fruits = str.split(",");
  console.log(fruits); // 输出: ["apple", "banana", "orange"]
  ```

- **`concat(...strings)`**  
  将多个字符串合并为一个新字符串。
  ```javascript
  let str1 = "Hello";
  let str2 = "World";
  console.log(str1.concat(" ", str2)); // 输出: "Hello World"
  ```

---

#### 5. **其他实用方法**
- **`repeat(count)`**  
  将字符串重复指定次数，返回新字符串。
  ```javascript
  let str = "Hi ";
  console.log(str.repeat(3)); // 输出: "Hi Hi Hi "
  ```

- **`match(regexp)`**  
  使用正则表达式匹配字符串，返回匹配结果数组或 null。
  ```javascript
  let str = "The year is 2025";
  console.log(str.match(/\d+/)); // 输出: ["2025", ...]
  ```

- **`search(regexp)`**  
  返回正则表达式匹配的第一个子字符串的索引，未找到返回 -1。
  ```javascript
  let str = "The year is 2025";
  console.log(str.search(/\d+/)); // 输出: 12
  ```

---

### 三、注意事项
1. **不可变性**：  
   字符串方法不会修改原字符串，而是返回新字符串。例如：
   ```javascript
   let str = "Hello";
   str.toLowerCase();
   console.log(str); // 输出: "Hello"（原字符串不变）
   ```

2. **正则表达式支持**：  
   方法如 `replace`、`match`、`search` 可以结合正则表达式使用，功能更强大。

3. **模板字符串**：  
   使用反引号（`` ` ``）创建的字符串支持 `${}` 插值，非常适合动态生成内容：
   ```javascript
   let name = "Alice";
   console.log(`Hello, ${name}!`); // 输出: "Hello, Alice!"
   ```

---

### 四、总结
JavaScript 的字符串方法非常丰富，涵盖了访问、搜索、修改、转换和分割等多种操作。通过这些方法，你可以灵活地处理文本数据。每个方法都有其独特用途，结合实际需求选择合适的方法即可。如果需要更深入的讲解或具体应用场景，欢迎随时告诉我！