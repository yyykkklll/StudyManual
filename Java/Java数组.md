# Java数组

---

### 一、Java数组概述
数组（Array）是Java中一种用于存储**固定长度**、**同类型**数据的数据结构。数组一旦定义，其大小不可更改。数组元素通过**索引**访问，索引从`0`开始。

---

### 二、数组的常见定义方式
Java中定义数组有以下几种方式：

1. **声明并初始化（静态初始化）**：
   - 直接在定义时指定数组内容。
   ```java
   int[] numbers = {1, 2, 3, 4, 5}; // 定义并初始化一个包含5个整数的数组
   ```

2. **声明后指定大小（动态初始化）**：
   - 先定义数组长度，元素默认初始化（数值类型为0，引用类型为null）。
   ```java
   int[] numbers = new int[5]; // 定义一个长度为5的数组，元素默认值为0
   numbers[0] = 1; // 手动赋值
   numbers[1] = 2;
   ```

3. **先声明后分配空间**：
   - 分步完成声明和初始化。
   ```java
   int[] numbers; // 声明
   numbers = new int[3]; // 分配空间
   numbers[0] = 10; // 赋值
   ```

4. **多维数组**（以二维为例）：
   ```java
   int[][] matrix = {{1, 2}, {3, 4}}; // 静态初始化
   // 或者
   int[][] matrix2 = new int[2][2]; // 动态初始化
   matrix2[0][0] = 1; // 赋值
   ```

---

### 三、数组的遍历方式
遍历数组是为了访问或操作数组中的每个元素。以下是常见的遍历方式：

1. **for循环（通过索引）**：
   - 适合需要操作索引的场景。
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   for (int i = 0; i < numbers.length; i++) {
       System.out.println(numbers[i]);
   }
   ```

2. **增强型for循环（foreach）**：
   - 简洁，适合只访问元素而不涉及索引。
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   for (int num : numbers) {
       System.out.println(num);
   }
   ```

3. **多维数组遍历**（以二维为例）：
   - 通常需要嵌套循环。
   ```java
   int[][] matrix = {{1, 2}, {3, 4}};
   for (int i = 0; i < matrix.length; i++) {
       for (int j = 0; j < matrix[i].length; j++) {
           System.out.print(matrix[i][j] + " ");
       }
       System.out.println();
   }
   ```

4. **使用流（Stream API，Java 8+）**：
   - 适合函数式编程风格。
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   java.util.Arrays.stream(numbers).forEach(System.out::println);
   ```

---

### 四、数组常用函数（方法）
Java中数组操作主要依赖`java.util.Arrays`类或数组本身的属性。以下是常用的函数/方法，每个附带简单示例：

1. **获取数组长度：`length`**  
   - 功能：返回数组的元素个数（属性，不是方法）。
   - 示例：
   ```java
   int[] numbers = {1, 2, 3, 4, 5};
   System.out.println("数组长度: " + numbers.length); // 输出: 数组长度: 5
   ```

2. **数组排序：`Arrays.sort()`**  
   - 功能：对数组元素进行升序排序。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] numbers = {5, 2, 8, 1, 9};
   Arrays.sort(numbers);
   System.out.println(Arrays.toString(numbers)); // 输出: [1, 2, 5, 8, 9]
   ```

3. **数组复制：`Arrays.copyOf()`**  
   - 功能：复制数组到新的长度（可扩展或截断）。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] numbers = {1, 2, 3};
   int[] newArray = Arrays.copyOf(numbers, 5); // 复制并扩展到长度5
   System.out.println(Arrays.toString(newArray)); // 输出: [1, 2, 3, 0, 0]
   ```

4. **数组填充：`Arrays.fill()`**  
   - 功能：用指定值填充整个数组或部分范围。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] numbers = new int[5];
   Arrays.fill(numbers, 10); // 填充10
   System.out.println(Arrays.toString(numbers)); // 输出: [10, 10, 10, 10, 10]
   ```

5. **数组转字符串：`Arrays.toString()`**  
   - 功能：将数组转换为易读的字符串格式。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] numbers = {1, 2, 3, 4, 5};
   System.out.println(Arrays.toString(numbers)); // 输出: [1, 2, 3, 4, 5]
   ```

6. **查找元素：`Arrays.binarySearch()`**  
   - 功能：在**已排序**数组中查找指定元素，返回索引（未找到返回负值）。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] numbers = {1, 2, 3, 4, 5};
   Arrays.sort(numbers); // 确保已排序
   int index = Arrays.binarySearch(numbers, 3);
   System.out.println("元素3的索引: " + index); // 输出: 元素3的索引: 2
   ```

7. **比较数组：`Arrays.equals()`**  
   - 功能：比较两个数组是否相等（长度和元素均相同）。
   - 示例：
   ```java
   import java.util.Arrays;
   int[] array1 = {1, 2, 3};
   int[] array2 = {1, 2, 3};
   boolean isEqual = Arrays.equals(array1, array2);
   System.out.println("数组相等: " + isEqual); // 输出: 数组相等: true
   ```

8. **部分复制：`System.arraycopy()`**  
   - 功能：将数组的一部分复制到另一个数组。
   - 示例：
   ```java
   int[] source = {1, 2, 3, 4, 5};
   int[] target = new int[3];
   System.arraycopy(source, 1, target, 0, 3); // 从source索引1开始复制3个元素
   System.out.println(Arrays.toString(target)); // 输出: [2, 3, 4]
   ```

---

### 五、注意事项
1. **数组越界**：访问超出数组长度的索引会抛出`ArrayIndexOutOfBoundsException`。
   ```java
   int[] numbers = {1, 2, 3};
   // System.out.println(numbers[3]); // 错误！索引3不存在
   ```

2. **不可变长度**：数组大小固定，若需动态调整，考虑使用`ArrayList`。
3. **初始化默认值**：
   - 整数类型（如`int`）：0
   - 浮点类型（如`double`）：0.0
   - 布尔类型：`false`
   - 引用类型（如`String`）：`null`

---

### 六、总结
- **定义方式**：静态初始化、动态初始化、多维数组等。

- **遍历方式**：for循环、foreach、Stream API等。

- **常用方法**：`length`、`Arrays.sort()`、`Arrays.copyOf()`、`Arrays.fill()`、`Arrays.toString()`、`Arrays.binarySearch()`、`Arrays.equals()`、`System.arraycopy()`。

  

