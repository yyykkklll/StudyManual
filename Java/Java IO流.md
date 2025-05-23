# Java IO 流

---

### 一、Java IO流概述
**IO流**（Input/Output Stream）是Java用于处理输入和输出的机制，主要用于**读取数据**（如从文件、网络、键盘等）或**写入数据**（如到文件、控制台、网络等）。Java的IO操作主要基于`java.io`包。

- **核心概念**：
  - **流（Stream）**：数据传输的抽象表示，像水流一样连续传递数据。
  - **输入流（Input Stream）**：从数据源（如文件）读取数据到程序。
  - **输出流（Output Stream）**：从程序写入数据到目标（如文件）。
  - **节点流 vs 处理流**：
    - 节点流：直接与数据源交互（如文件流）。
    - 处理流：包装节点流，提供增强功能（如缓冲流）。

- **分类**：
  - **按数据单位**：
    - **字节流**（Byte Stream）：以字节为单位，适合处理二进制数据（如图片、视频）。
    - **字符流**（Character Stream）：以字符为单位，适合处理文本数据。
  - **按流向**：
    - 输入流：读取数据。
    - 输出流：写入数据。
  - **按功能**：
    - 节点流：直接操作数据源。
    - 处理流：增强节点流（如缓冲、转换等）。

---

### 二、Java IO流体系
Java的IO流类主要位于`java.io`包，以下是常见的类及其关系：

#### 1. 字节流
- **抽象基类**：
  - `InputStream`：字节输入流基类。
  - `OutputStream`：字节输出流基类。
- **常见子类**：
  - `FileInputStream` / `FileOutputStream`：文件字节流。
  - `BufferedInputStream` / `BufferedOutputStream`：缓冲字节流。
  - `ObjectInputStream` / `ObjectOutputStream`：对象序列化流。

#### 2. 字符流
- **抽象基类**：
  - `Reader`：字符输入流基类。
  - `Writer`：字符输出流基类。
- **常见子类**：
  - `FileReader` / `FileWriter`：文件字符流。
  - `BufferedReader` / `BufferedWriter`：缓冲字符流。
  - `InputStreamReader` / `OutputStreamWriter`：字节流到字符流的桥梁。

#### 3. 其他流
- `DataInputStream` / `DataOutputStream`：处理基本数据类型。
- `PrintStream` / `PrintWriter`：格式化输出。

---

### 三、字节流
字节流以字节（8位）为单位，适合处理所有类型的数据（如文本、图片、视频等）。

#### 1. `FileInputStream`（文件字节输入流）
- **功能**：从文件中读取字节数据。
- **常用方法**：
  - `int read()`：读取单个字节，返回-1表示文件末尾。
  - `int read(byte[] b)`：读取字节到数组，返回读取的字节数。
  - `void close()`：关闭流。

**示例**：读取文件内容
```java
import java.io.FileInputStream;
import java.io.IOException;

public class FileInputStreamDemo {
    public static void main(String[] args) {
        try (FileInputStream fis = new FileInputStream("input.txt")) {
            int data;
            // 逐字节读取
            while ((data = fis.read()) != -1) {
                System.out.print((char) data);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：假设`input.txt`内容为`Hello`，输出为`Hello`。
- **注意**：使用`try-with-resources`自动关闭流，避免资源泄漏。

#### 2. `FileOutputStream`（文件字节输出流）
- **功能**：向文件中写入字节数据。
- **常用方法**：
  - `void write(int b)`：写入单个字节。
  - `void write(byte[] b)`：写入字节数组。
  - `void flush()`：刷新缓冲区。
  - `void close()`：关闭流。

**示例**：写入文件
```java
import java.io.FileOutputStream;
import java.io.IOException;

public class FileOutputStreamDemo {
    public static void main(String[] args) {
        try (FileOutputStream fos = new FileOutputStream("output.txt")) {
            String text = "Hello, Java!";
            fos.write(text.getBytes()); // 写入字节数组
            fos.flush(); // 确保数据写入
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：会在`output.txt`中写入`Hello, Java!`。
- **注意**：若文件不存在，会自动创建；若存在，默认覆盖（可通过构造方法追加）。

#### 3. `BufferedInputStream` / `BufferedOutputStream`（缓冲字节流）
- **功能**：通过缓冲区减少对底层系统的直接访问，提高效率。
- **使用方式**：包装节点流（如`FileInputStream`）。

**示例**：使用缓冲流复制文件
```java
import java.io.*;

public class BufferedStreamDemo {
    public static void main(String[] args) {
        try (BufferedInputStream bis = new BufferedInputStream(new FileInputStream("source.jpg"));
             BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream("copy.jpg"))) {
            byte[] buffer = new byte[1024]; // 缓冲区
            int bytesRead;
            while ((bytesRead = bis.read(buffer)) != -1) {
                bos.write(buffer, 0, bytesRead);
            }
            bos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：复制图片文件`source.jpg`到`copy.jpg`。
- **优点**：通过缓冲区（默认8KB）减少IO操作，提高性能。

---

### 四、字符流
字符流以字符（16位Unicode）为单位，专门处理文本数据，自动处理字符编码（如UTF-8）。

#### 1. `FileReader`（文件字符输入流）
- **功能**：从文件中读取字符数据。
- **常用方法**：
  - `int read()`：读取单个字符。
  - `int read(char[] cbuf)`：读取字符到数组。

**示例**：读取文本文件
```java
import java.io.FileReader;
import java.io.IOException;

public class FileReaderDemo {
    public static void main(String[] args) {
        try (FileReader fr = new FileReader("input.txt")) {
            char[] buffer = new char[1024];
            int charsRead;
            while ((charsRead = fr.read(buffer)) != -1) {
                System.out.print(new String(buffer, 0, charsRead));
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：读取`input.txt`并输出内容。

#### 2. `FileWriter`（文件字符输出流）
- **功能**：向文件中写入字符数据。
- **常用方法**：
  - `void write(String str)`：写入字符串。
  - `void write(char[] cbuf)`：写入字符数组。

**示例**：写入文本文件
```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWriterDemo {
    public static void main(String[] args) {
        try (FileWriter fw = new FileWriter("output.txt")) {
            fw.write("Hello, Java!\n");
            fw.write("This is a test.");
            fw.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：在`output.txt`中写入两行文本。

#### 3. `BufferedReader` / `BufferedWriter`（缓冲字符流）
- **功能**：提供缓冲功能，`BufferedReader`支持按行读取，效率更高。
- **常用方法**：
  - `BufferedReader.readLine()`：读取一行文本。
  - `BufferedWriter.newLine()`：写入换行符。

**示例**：按行读写文本
```java
import java.io.*;

public class BufferedReaderWriterDemo {
    public static void main(String[] args) {
        try (BufferedReader br = new BufferedReader(new FileReader("input.txt"));
             BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
            String line;
            while ((line = br.readLine()) != null) {
                bw.write(line.toUpperCase());
                bw.newLine();
            }
            bw.flush();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：将`input.txt`的每行转换为大写，写入`output.txt`。
- **优点**：`readLine()`方便处理文本行，缓冲提高效率。

---

### 五、字节流与字符流的转换
字节流和字符流通过**桥梁类**相互转换：
- `InputStreamReader`：字节输入流转字符输入流。
- `OutputStreamWriter`：字符输出流转字节输出流。

**示例**：读取文件并指定编码
```java
import java.io.*;

public class InputStreamReaderDemo {
    public static void main(String[] args) {
        try (InputStreamReader isr = new InputStreamReader(new FileInputStream("input.txt"), "UTF-8");
             BufferedReader br = new BufferedReader(isr)) {
            String line;
            while ((line = br.readLine()) != null) {
                System.out.println(line);
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
- **说明**：以UTF-8编码读取文件，避免乱码。

---

### 六、对象流（序列化）
`ObjectInputStream`和`ObjectOutputStream`用于对象的序列化和反序列化，对象需实现`Serializable`接口。

**示例**：序列化与反序列化对象
```java
import java.io.*;

public class ObjectStreamDemo {
    public static void main(String[] args) {
        // 序列化
        try (ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("person.dat"))) {
            Person person = new Person("Alice", 25);
            oos.writeObject(person);
        } catch (IOException e) {
            e.printStackTrace();
        }
        
        // 反序列化
        try (ObjectInputStream ois = new ObjectInputStream(new FileInputStream("person.dat"))) {
            Person person = (Person) ois.readObject();
            System.out.println("Name: " + person.getName() + ", Age: " + person.getAge());
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}

class Person implements Serializable {
    private String name;
    private int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    public String getName() { return name; }
    public int getAge() { return age; }
}
```
- **说明**：将`Person`对象写入`person.dat`，然后读取并输出。
- **注意**：类需实现`Serializable`，否则抛出`NotSerializableException`。

---

### 七、其他常见流
1. **PrintStream / PrintWriter**：
   - 功能：格式化输出，`System.out`就是`PrintStream`实例。
   - 示例：
   ```java
   try (PrintWriter pw = new PrintWriter("output.txt")) {
       pw.println("Hello, Java!");
       pw.printf("Age: %d", 25);
   } catch (FileNotFoundException e) {
       e.printStackTrace();
   }
   ```

2. **DataInputStream / DataOutputStream**：
   - 功能：读写基本数据类型（如`int`、`double`）。
   - 示例：
   ```java
   try (DataOutputStream dos = new DataOutputStream(new FileOutputStream("data.dat"))) {
       dos.writeInt(42);
       dos.writeDouble(3.14);
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

3. **RandomAccessFile**：
   - 功能：支持随机读写，可定位文件指针。
   - 示例：
   ```java
   try (RandomAccessFile raf = new RandomAccessFile("test.txt", "rw")) {
       raf.write("Hello".getBytes());
       raf.seek(0); // 移到开头
       byte[] buffer = new byte[5];
       raf.read(buffer);
       System.out.println(new String(buffer)); // 输出: Hello
   } catch (IOException e) {
       e.printStackTrace();
   }
   ```

---

### 八、异常处理与资源管理
- **IO异常**：IO操作可能抛出`IOException`（如文件不存在、权限不足）。
- **资源管理**：
  - 使用`try-with-resources`（Java 7+）自动关闭流。
  - 确保调用`flush()`和`close()`，否则可能丢失数据。

**示例**（错误处理）：
```java
try (FileInputStream fis = new FileInputStream("nonexistent.txt")) {
    int data = fis.read();
} catch (FileNotFoundException e) {
    System.out.println("文件未找到: " + e.getMessage());
} catch (IOException e) {
    e.printStackTrace();
}
```

---

### 九、注意事项
1. **字节流 vs 字符流**：
   - 文本文件优先用字符流（`Reader`/`Writer`），避免编码问题。
   - 二进制文件（如图片）必须用字节流（`InputStream`/`OutputStream`）。

2. **缓冲流**：
   - 总是优先使用`Buffered*`流，减少底层IO操作。
   - `BufferedReader.readLine()`是处理文本的利器。

3. **编码问题**：
   - 使用`InputStreamReader`/`OutputStreamWriter`指定编码（如`UTF-8`）。
   - 默认编码依赖操作系统，可能导致乱码。

4. **性能优化**：
   - 使用适当的缓冲区大小（如`byte[1024]`）。
   - 避免逐字节/字符读取，尽量批量操作。

5. **序列化注意**：
   - 实现`Serializable`的类需定义`serialVersionUID`以确保版本兼容。
   ```java
   private static final long serialVersionUID = 1L;
   ```

---

### 十、总结
- **IO流分类**：
  - **字节流**：`InputStream`/`OutputStream`，如`FileInputStream`、`BufferedInputStream`。
  - **字符流**：`Reader`/`Writer`，如`FileReader`、`BufferedReader`。
  - **对象流**：`ObjectInputStream`/`ObjectOutputStream`。
  - **其他**：`PrintStream`、`RandomAccessFile`等。
- **核心操作**：
  - 文件读写：字节流适合二进制，字符流适合文本。
  - 缓冲流：提高效率，`BufferedReader`支持按行读取。
  - 序列化：保存/恢复对象状态。
- **实践要点**：
  - 使用`try-with-resources`管理资源。
  - 注意编码和异常处理。
  - 根据数据类型选择合适的流。

Java的IO流体系功能强大，掌握这些类和方法后，你可以轻松处理文件、网络数据等操作。如果想深入某个部分（如NIO、网络IO）或需要练习题目（比如文件复制、CSV解析），告诉我，我可以进一步讲解或提供代码！😊