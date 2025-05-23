# Java字符串

---

### 一、Java字符串概述
在Java中，`String` 是一个类（`java.lang.String`），用于表示字符序列。字符串是**不可变**的（Immutable），即一旦创建，其内容无法更改。`String` 对象的操作通常会返回一个新的字符串，而不是修改原字符串。

- **特点**：
  - 不可变性：保证线程安全，但频繁操作可能影响性能（可考虑`StringBuilder`或`StringBuffer`）。
  - 存储在字符串常量池（String Pool）中，相同内容的字符串可复用。
  - 支持大量内置方法，操作方便。

---

### 二、字符串的定义方式
以下是Java中常见的字符串定义方式：

1. **直接赋值（使用字符串字面量）**：
   - 字符串存储在常量池中，相同内容共享同一对象。
   ```java
   String str1 = "Hello"; // 直接赋值
   ```

2. **使用`new`关键字**：
   - 在堆内存中创建新对象（即使内容相同，也不是常量池中的对象）。
   ```java
   String str2 = new String("Hello"); // 使用构造方法
   ```

3. **通过字符数组创建**：
   ```java
   char[] chars = {'H', 'e', 'l', 'l', 'o'};
   String str3 = new String(chars); // 从字符数组构造
   ```

4. **字符串拼接**：
   ```java
   String str4 = "Hello" + ", World!"; // 拼接生成新字符串
   ```

**注意**：
- 使用`==`比较字符串对象时，比较的是引用地址；用`equals()`比较内容。
- 常量池中的字符串（如`"Hello"`）会被复用，而`new String()`创建的字符串不会。

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");
System.out.println(str1 == str2); // true（常量池复用）
System.out.println(str1 == str3); // false（不同对象）
System.out.println(str1.equals(str3)); // true（内容相同）
```

---

### 三、字符串的遍历方式
字符串本质上是字符序列，可以通过以下方式遍历：

1. **使用`charAt()`方法（通过索引）**：
   - 通过索引逐个访问字符。
   ```java
   String str = "Hello";
   for (int i = 0; i < str.length(); i++) {
       System.out.println(str.charAt(i));
   }
   ```

2. **转换为字符数组后遍历**：
   - 使用`toCharArray()`将字符串转为`char[]`。
   ```java
   String str = "Hello";
   char[] chars = str.toCharArray();
   for (char c : chars) {
       System.out.println(c);
   }
   ```

3. **使用`forEach`和`chars()`（Java 8+）**：
   - 通过字符的Unicode码点流式处理。
   ```java
   String str = "Hello";
   str.chars().forEach(c -> System.out.println((char) c));
   ```

---

### 四、字符串常用方法
`String` 类提供了丰富的内置方法，以下是常用的方法，每个附带简单代码示例：

1. **获取长度：`length()`**  
   - 功能：返回字符串的字符数。
   - 示例：
   ```java
   String str = "Hello";
   System.out.println("长度: " + str.length()); // 输出: 长度: 5
   ```

2. **获取指定索引字符：`charAt(int index)`**  
   - 功能：返回指定索引的字符。
   - 示例：
   ```java
   String str = "Hello";
   System.out.println("索引2的字符: " + str.charAt(2)); // 输出: 索引2的字符: l
   ```

3. **子字符串：`substring(int beginIndex, int endIndex)`**  
   - 功能：提取从`beginIndex`到`endIndex-1`的子字符串。
   - 示例：
   ```java
   String str = "Hello, World";
   System.out.println("子字符串: " + str.substring(0, 5)); // 输出: 子字符串: Hello
   ```

4. **字符串拼接：`concat(String str)`**  
   - 功能：在字符串末尾追加另一个字符串。
   - 示例：
   ```java
   String str = "Hello";
   System.out.println("拼接后: " + str.concat(", World")); // 输出: 拼接后: Hello, World
   ```

5. **大小写转换：`toUpperCase()` / `toLowerCase()`**  
   - 功能：将字符串转换为全大写或全小写。
   - 示例：
   ```java
   String str = "Hello";
   System.out.println("大写: " + str.toUpperCase()); // 输出: 大写: HELLO
   System.out.println("小写: " + str.toLowerCase()); // 输出: 小写: hello
   ```

6. **查找子字符串：`indexOf(String str)` / `lastIndexOf(String str)`**  
   - 功能：返回子字符串首次/最后出现的位置，未找到返回-1。
   - 示例：
   ```java
   String str = "Hello, Hello";
   System.out.println("首次出现'Hello': " + str.indexOf("Hello")); // 输出: 首次出现'Hello': 0
   System.out.println("最后出现'Hello': " + str.lastIndexOf("Hello")); // 输出: 最后出现'Hello': 7
   ```

7. **替换：`replace(CharSequence target, CharSequence replacement)`**  
   - 功能：替换所有匹配的子字符串。
   - 示例：
   ```java
   String str = "Hello, World";
   System.out.println("替换后: " + str.replace("World", "Java")); // 输出: 替换后: Hello, Java
   ```

8. **分割：`split(String regex)`**  
   - 功能：根据正则表达式分割字符串为数组。
   - 示例：
   ```java
   String str = "apple,banana,orange";
   String[] fruits = str.split(",");
   System.out.println(Arrays.toString(fruits)); // 输出: [apple, banana, orange]
   ```

9. **去除首尾空白：`trim()`**  
   - 功能：去除字符串首尾的空白字符（空格、制表符等）。
   - 示例：
   ```java
   String str = "  Hello  ";
   System.out.println("去除空白: " + str.trim()); // 输出: 去除空白: Hello
   ```

10. **判断是否包含：`contains(CharSequence s)`**  
    - 功能：检查字符串是否包含指定子字符串。
    - 示例：
    ```java
    String str = "Hello, World";
    System.out.println("包含'World': " + str.contains("World")); // 输出: 包含'World': true
    ```

11. **比较字符串：`equals(Object obj)` / `equalsIgnoreCase(String str)`**  
    - 功能：比较字符串内容是否相等（`equalsIgnoreCase`忽略大小写）。
    - 示例：
    ```java
    String str1 = "Hello";
    String str2 = "hello";
    System.out.println("相等: " + str1.equals(str2)); // 输出: 相等: false
    System.out.println("忽略大小写相等: " + str1.equalsIgnoreCase(str2)); // 输出: 忽略大小写相等: true
    ```

12. **判断空字符串：`isEmpty()`**  
    - 功能：检查字符串是否为空（长度为0）。
    - 示例：
    ```java
    String str = "";
    System.out.println("是否为空: " + str.isEmpty()); // 输出: 是否为空: true
    ```

---

### 五、注意事项
1. **不可变性**：
   - `String` 的任何修改操作（如`replace`、`substring`）都会返回新对象，原字符串不变。
   ```java
   String str = "Hello";
   str.toUpperCase(); // 不会改变str
   System.out.println(str); // 输出: Hello
   str = str.toUpperCase(); // 必须重新赋值
   System.out.println(str); // 输出: HELLO
   ```

2. **性能问题**：
   - 频繁拼接字符串（如在循环中用`+`）会创建多个临时对象，效率低。建议使用`StringBuilder`。
   ```java
   StringBuilder sb = new StringBuilder();
   for (int i = 0; i < 3; i++) {
       sb.append("Hello").append(i);
   }
   System.out.println(sb.toString()); // 输出: Hello0Hello1Hello2
   ```

3. **空字符串与`null`**：
   - 空字符串`""`是长度为0的字符串；`null`表示没有对象。
   ```java
   String str = null;
   // System.out.println(str.length()); // 抛出NullPointerException
   ```

4. **正则表达式**：
   - `split()`、`replace()`等方法支持正则表达式，需注意转义字符。
   ```java
   String str = "a.b.c";
   String[] parts = str.split("\\."); // 点号需转义
   System.out.println(Arrays.toString(parts)); // 输出: [a, b, c]
   ```

---

### 六、总结
- **定义方式**：字面量、构造方法、字符数组、拼接等。
- **遍历方式**：`charAt()`、字符数组、`chars()`流等。
- **常用方法**：`length()`、`charAt()`、`substring()`、`concat()`、`toUpperCase()`/`toLowerCase()`、`indexOf()`/`lastIndexOf()`、`replace()`、`split()`、`trim()`、`contains()`、`equals()`/`equalsIgnoreCase()`、`isEmpty()`等。
