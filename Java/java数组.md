# Java数组

### **1. 数组的定义方式**

#### **方式一：先声明，再初始化**
```java
int[] numbers; // 声明一个整型数组
numbers = new int[5]; // 初始化数组，大小为5
```

#### **方式二：声明和初始化同时进行**
```java
int[] numbers = new int[5]; // 声明并初始化数组
```

#### **方式三：直接赋值**
```java
int[] numbers = {1, 2, 3, 4, 5}; // 声明并直接赋值
```

### **2. 数组的遍历方式**

#### **方式一：传统的for循环**
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

#### **方式二：增强型for循环（foreach）**
```java
int[] numbers = {1, 2, 3, 4, 5};
for (int number : numbers) {
    System.out.println(number);
}
```

#### **方式三：使用Java 8的Stream API**
```java
import java.util.Arrays;

int[] numbers = {1, 2, 3, 4, 5};
Arrays.stream(numbers).forEach(System.out::println);
```

### **3. 数组的常用函数**

#### **函数一：`Arrays.toString()`**
用于将数组转换为字符串，方便打印。
```java
import java.util.Arrays;

int[] numbers = {1, 2, 3, 4, 5};
System.out.println(Arrays.toString(numbers)); // 输出：[1, 2, 3, 4, 5]
```

#### **函数二：`Arrays.sort()`**
对数组进行排序。
```java
import java.util.Arrays;

int[] numbers = {5, 2, 3, 4, 1};
Arrays.sort(numbers); // 排序后数组变为 [1, 2, 3, 4, 5]
System.out.println(Arrays.toString(numbers));
```

#### **函数三：`Arrays.binarySearch()`**
在排序后的数组中查找元素，返回索引。
```java
import java.util.Arrays;

int[] numbers = {1, 2, 3, 4, 5};
int index = Arrays.binarySearch(numbers, 3); // 查找元素3
System.out.println(index); // 输出：2
```

#### **函数四：`Arrays.copyOf()`**
复制数组。
```java
import java.util.Arrays;

int[] numbers = {1, 2, 3, 4, 5};
int[] copy = Arrays.copyOf(numbers, numbers.length); // 复制整个数组
System.out.println(Arrays.toString(copy)); // 输出：[1, 2, 3, 4, 5]
```

#### **函数五：`Arrays.fill()`**
用指定值填充数组。
```java
import java.util.Arrays;

int[] numbers = new int[5];
Arrays.fill(numbers, 10); // 将数组所有元素填充为10
System.out.println(Arrays.toString(numbers)); // 输出：[10, 10, 10, 10, 10]
```

### **总结**
- **定义数组**：可以通过声明和初始化分开，或者直接赋值。
- **遍历数组**：可以使用传统的for循环、增强型for循环（foreach）或者Java 8的Stream API。
- **常用函数**：`Arrays.toString()`、`Arrays.sort()`、`Arrays.binarySearch()`、`Arrays.copyOf()`和`Arrays.fill()`等，用于操作数组。
