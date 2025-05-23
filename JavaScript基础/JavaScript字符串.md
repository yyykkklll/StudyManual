# JavaScript字符串

---

### 一、JavaScript字符串概述
在JavaScript中，字符串（`String`）是一种基本数据类型，用于表示文本数据。字符串由零个或多个字符组成，字符可以是字母、数字、符号等，基于**Unicode**编码。

- **特点**：
  - **不可变性**：字符串内容一旦创建不可更改，修改操作会返回新字符串。
  - **包装对象**：JavaScript会自动将字符串基本类型包装为`String`对象，允许调用`String`对象的方法。
  - **灵活性**：支持模板字面量（Template Literals，ES6+）和丰富的内置方法。
  - **存储**：字符串可以是单引号（`'`）、双引号（`"`）或反引号（`` ` ``）包裹。

---

### 二、字符串的定义方式
JavaScript中定义字符串有以下几种方式：

1. **使用单引号或双引号**：
   - 最常见的方式，单引号和双引号功能相同。
   ```javascript
   let str1 = 'Hello';
   let str2 = "World";
   ```

2. **使用反引号（模板字面量，ES6+）**：
   - 支持多行字符串和插值表达式（`${}`）。
   ```javascript
   let name = 'Alice';
   let str3 = `Hello, ${name}!`; // 输出: Hello, Alice!
   let multiLine = `
     Line 1
     Line 2
   `;
   ```

3. **通过`String`构造函数**：
   - 创建字符串对象（不推荐直接使用，因性能稍差）。
   ```javascript
   let str4 = new String('Hello'); // String对象
   console.log(typeof str4); // 输出: object
   ```

4. **字符串拼接**：
   - 使用`+`或模板字面量拼接。
   ```javascript
   let str5 = 'Hello' + ' ' + 'World'; // Hello World
   let str6 = `${str1} World`; // Hello World
   ```

**注意**：
- 基本类型字符串（`let s = 'hi'`）和`String`对象（`new String('hi')`）在大多数操作中表现类似，但`===`比较时不同。
  ```javascript
  let s1 = 'hi';
  let s2 = new String('hi');
  console.log(s1 === s2); // false（类型不同）
  console.log(s1 === s2.valueOf()); // true（内容相同）
  ```

---

### 三、字符串的遍历方式
JavaScript提供了多种方式遍历字符串的字符：

1. **使用`for`循环（通过索引）**：
   - 通过`length`属性和索引访问字符。
   ```javascript
   let str = 'Hello';
   for (let i = 0; i < str.length; i++) {
       console.log(str[i]);
   }
   // 输出: H e l l o
   ```

2. **使用`for...of`循环**：
   - 直接迭代字符串的每个字符（支持Unicode字符）。
   ```javascript
   let str = 'Hello';
   for (let char of str) {
       console.log(char);
   }
   // 输出: H e l l o
   ```

3. **使用`forEach`和`split()`**：
   - 将字符串转为数组后遍历。
   ```javascript
   let str = 'Hello';
   str.split('').forEach(char => console.log(char));
   // 输出: H e l l o
   ```

4. **使用`String.prototype[Symbol.iterator]`**：
   - 字符串是可迭代对象，支持迭代器协议。
   ```javascript
   let str = 'Hello';
   let iterator = str[Symbol.iterator]();
   let char = iterator.next();
   while (!char.done) {
       console.log(char.value);
       char = iterator.next();
   }
   // 输出: H e l l o
   ```

---

### 四、字符串常用方法
JavaScript的`String`对象提供了丰富的内置方法，以下是常用的方法，每个附带简单代码示例：

1. **获取长度：`length`**  
   - 功能：返回字符串的字符数（属性，不是方法）。
   - 示例：
   ```javascript
   let str = 'Hello';
   console.log(str.length); // 输出: 5
   ```

2. **获取指定索引字符：`charAt(index)` / 索引访问**  
   - 功能：返回指定索引的字符（`charAt`或`str[index]`）。
   - 示例：
   ```javascript
   let str = 'Hello';
   console.log(str.charAt(1)); // 输出: e
   console.log(str[1]); // 输出: e
   ```
   - **注意**：`charAt`返回空字符串（`''`）若索引无效，`str[index]`返回`undefined`。

3. **子字符串：`slice(start, end)` / `substring(start, end)`**  
   - 功能：提取从`start`到`end-1`的子字符串（`slice`支持负索引）。
   - 示例：
   ```javascript
   let str = 'Hello, World';
   console.log(str.slice(0, 5)); // 输出: Hello
   console.log(str.substring(7, 12)); // 输出: World
   console.log(str.slice(-5)); // 输出: World
   ```

4. **字符串拼接：`concat(...strings)`**  
   - 功能：拼接多个字符串（通常用`+`或模板字面量更常见）。
   - 示例：
   ```javascript
   let str = 'Hello';
   console.log(str.concat(', ', 'World')); // 输出: Hello, World
   ```

5. **大小写转换：`toUpperCase()` / `toLowerCase()`**  
   - 功能：转换为全大写或全小写。
   - 示例：
   ```javascript
   let str = 'Hello';
   console.log(str.toUpperCase()); // 输出: HELLO
   console.log(str.toLowerCase()); // 输出: hello
   ```

6. **查找子字符串：`indexOf(searchValue, fromIndex)` / `lastIndexOf(searchValue, fromIndex)`**  
   - 功能：返回子字符串首次/最后出现的位置，未找到返回-1。
   - 示例：
   ```javascript
   let str = 'Hello, Hello';
   console.log(str.indexOf('Hello')); // 输出: 0
   console.log(str.lastIndexOf('Hello')); // 输出: 7
   ```

7. **替换：`replace(searchValue, newValue)` / `replaceAll(searchValue, newValue)`**  
   - 功能：替换首次（`replace`）或所有（`replaceAll`）匹配的子字符串。
   - 示例：
   ```javascript
   let str = 'Hello, World';
   console.log(str.replace('World', 'Java')); // 输出: Hello, Java
   console.log(str.replaceAll('l', 'L')); // 输出: HeLLo, WorLd
   ```

8. **分割：`split(separator, limit)`**  
   - 功能：根据分隔符将字符串分割为数组，可指定最大分割数。
   - 示例：
   ```javascript
   let str = 'apple,banana,orange';
   console.log(str.split(',')); // 输出: ['apple', 'banana', 'orange']
   console.log(str.split(',', 2)); // 输出: ['apple', 'banana']
   ```

9. **去除首尾空白：`trim()` / `trimStart()` / `trimEnd()`**  
   - 功能：去除字符串首尾（或首/尾）的空白字符。
   - 示例：
   ```javascript
   let str = '  Hello  ';
   console.log(str.trim()); // 输出: Hello
   console.log(str.trimStart()); // 输出: Hello  
   console.log(str.trimEnd()); // 输出:   Hello
   ```

10. **判断是否包含：`includes(searchString, position)`**  
    - 功能：检查字符串是否包含指定子字符串。
    - 示例：
    ```javascript
    let str = 'Hello, World';
    console.log(str.includes('World')); // 输出: true
    console.log(str.includes('Java')); // 输出: false
    ```

11. **判断开头/结尾：`startsWith(searchString, position)` / `endsWith(searchString, length)`**  
    - 功能：检查字符串是否以指定字符串开头/结尾。
    - 示例：
    ```javascript
    let str = 'Hello, World';
    console.log(str.startsWith('Hello')); // 输出: true
    console.log(str.endsWith('World')); // 输出: true
    ```

12. **重复：`repeat(count)`**  
    - 功能：重复字符串指定次数。
    - 示例：
    ```javascript
    let str = 'Hi ';
    console.log(str.repeat(3)); // 输出: Hi Hi Hi 
    ```

13. **填充：`padStart(targetLength, padString)` / `padEnd(targetLength, padString)`**  
    - 功能：在字符串开头/结尾填充字符至指定长度。
    - 示例：
    ```javascript
    let str = '5';
    console.log(str.padStart(3, '0')); // 输出: 005
    console.log(str.padEnd(3, '0')); // 输出: 500
    ```

14. **正则表达式匹配：`match(regex)`**  
    - 功能：根据正则表达式查找匹配项，返回匹配数组或`null`。
    - 示例：
    ```javascript
    let str = 'Hello123';
    console.log(str.match(/\d+/)); // 输出: ['123', index: 5, input: 'Hello123', groups: undefined]
    ```

15. **Unicode字符：`charCodeAt(index)` / `codePointAt(index)`**  
    - 功能：返回指定索引处的字符的Unicode编码（`codePointAt`支持多字节字符）。
    - 示例：
    ```javascript
    let str = 'Hello';
    console.log(str.charCodeAt(0)); // 输出: 72（H的Unicode）
    console.log('😊'.codePointAt(0)); // 输出: 128522（表情符号）
    ```

---

### 五、模板字面量（额外特性，ES6+）
模板字面量使用反引号（`` ` ``）定义，支持：
- **多行字符串**：无需手动添加`\n`。
- **插值表达式**：嵌入变量或表达式。

**示例**：
```javascript
let name = 'Bob';
let age = 25;
let greeting = `
  Name: ${name}
  Age: ${age}
  Is adult: ${age >= 18 ? 'Yes' : 'No'}
`;
console.log(greeting);
// 输出:
// Name: Bob
// Age: 25
// Is adult: Yes
```

---

### 六、注意事项
1. **不可变性**：
   - 字符串方法不会修改原字符串，而是返回新字符串。
   ```javascript
   let str = 'Hello';
   str.toUpperCase();
   console.log(str); // 输出: Hello（原字符串不变）
   str = str.toUpperCase();
   console.log(str); // 输出: HELLO
   ```

2. **性能问题**：
   - 频繁拼接字符串（尤其是循环中用`+`）可能影响性能，建议使用数组`join()`。
   ```javascript
   let arr = [];
   for (let i = 0; i < 3; i++) {
       arr.push('Hello' + i);
   }
   console.log(arr.join(' ')); // 输出: Hello0 Hello1 Hello2
   ```

3. **编码问题**：
   - JavaScript字符串基于Unicode，`length`和索引基于UTF-16编码单元，可能影响多字节字符（如表情符号）。
   ```javascript
   let str = '😊';
   console.log(str.length); // 输出: 2（UTF-16编码单元）
   ```

4. **正则表达式支持**：
   - 方法如`replace`、`match`、`split`支持正则表达式，功能强大。
   ```javascript
   let str = 'hello123world';
   console.log(str.replace(/\d+/, '!!!')); // 输出: hello!!!world
   ```

5. **与Java字符串对比**（参考你之前的学习）：
   - JavaScript字符串更灵活（如模板字面量），但缺乏Java的严格类型检查。
   - JavaScript无`StringBuilder`等优化类，需用数组优化拼接。
   - JavaScript的`split`、`replace`等方法与Java类似，但语法更简洁。

---

### 七、总结
- **定义方式**：单引号、双引号、反引号（模板字面量）、`String`构造函数。
- **遍历方式**：`for`循环、`for...of`、数组`forEach`、迭代器。
- **常用方法**：`length`、`charAt`、`slice`/`substring`、`concat`、`toUpperCase`/`toLowerCase`、`indexOf`/`lastIndexOf`、`replace`/`replaceAll`、`split`、`trim`、`includes`、`startsWith`/`endsWith`、`repeat`、`padStart`/`padEnd`、`match`、`charCodeAt`等。
- **特色**：模板字面量支持多行和插值，正则表达式增强字符串操作。
- 字符串是JavaScript中最常用的数据类型，掌握这些方法能让你轻松处理文本、格式化数据等任务。
