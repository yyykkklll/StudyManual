# **Java面向对象编程（OOP）**。

---

### 一、面向对象编程概述
面向对象编程（OOP）是一种以**对象**为核心的编程范式，旨在通过模拟现实世界中的实体来组织代码。Java是完全面向对象的语言，OOP的核心思想包括：

- **类（Class）**：对象的蓝图，定义了对象的属性（数据）和行为（方法）。
- **对象（Object）**：类的实例，具体化了类的定义。
- **四大特性**：封装、继承、多态、抽象。

---

### 二、核心概念与实现

#### 1. 类与对象
- **类**：定义了对象的结构和行为，使用`class`关键字声明。
- **对象**：类的实例，通过`new`关键字创建。

**定义类的示例**：
```java
public class Student {
    // 属性（成员变量）
    String name;
    int age;
    
    // 方法
    void study() {
        System.out.println(name + " is studying.");
    }
}
```

**创建和使用对象的示例**：
```java
public class Main {
    public static void main(String[] args) {
        // 创建对象
        Student student = new Student();
        // 设置属性
        student.name = "Alice";
        student.age = 20;
        // 调用方法
        student.study(); // 输出: Alice is studying.
    }
}
```

**注意**：
- 类是静态的模板，对象是动态的实例。
- 对象通过`.`操作符访问属性和方法。

---

#### 2. 封装（Encapsulation）
- **定义**：将数据（属性）和操作数据的方法绑定在一起，通过访问控制（`private`、`public`等）隐藏内部实现，保护数据安全。
- **实现**：使用`private`修饰属性，提供`public`的`getter`和`setter`方法。

**封装示例**：
```java
public class Student {
    private String name;
    private int age;
    
    // getter 方法
    public String getName() {
        return name;
    }
    
    // setter 方法
    public void setName(String name) {
        this.name = name; // this 区分成员变量和参数
    }
    
    public int getAge() {
        return age;
    }
    
    public void setAge(int age) {
        if (age >= 0) { // 添加逻辑检查
            this.age = age;
        }
    }
    
    public void study() {
        System.out.println(name + " is studying.");
    }
}

public class Main {
    public static void main(String[] args) {
        Student student = new Student();
        student.setName("Bob");
        student.setAge(22);
        System.out.println("Name: " + student.getName() + ", Age: " + student.getAge());
        student.study(); // 输出: Name: Bob, Age: 22
                        //      Bob is studying.
    }
}
```

**优点**：
- 隐藏实现细节，防止直接修改数据。
- 提高代码可维护性和安全性。

---

#### 3. 继承（Inheritance）
- **定义**：子类通过`extends`关键字继承父类的属性和方法，实现代码复用。
- **特点**：
  - 子类可以扩展父类（添加新属性/方法）。
  - 子类可以重写（Override）父类方法。
  - Java只支持**单继承**（一个类只能继承一个父类）。

**继承示例**：
```java
public class Person {
    protected String name;
    protected int age;
    
    public void introduce() {
        System.out.println("I am " + name + ", " + age + " years old.");
    }
}

public class Student extends Person {
    private String school;
    
    public void setSchool(String school) {
        this.school = school;
    }
    
    // 重写父类方法
    @Override
    public void introduce() {
        System.out.println("I am " + name + ", a student at " + school + ".");
    }
}

public class Main {
    public static void main(String[] args) {
        Student student = new Student();
        student.name = "Charlie"; // 继承的属性
        student.age = 18;
        student.setSchool("High School");
        student.introduce(); // 输出: I am Charlie, a student at High School.
    }
}
```

**注意**：
- 使用`protected`让子类可以访问父类成员。
- `@Override`注解确保方法正确重写。
- 父类构造方法不会被继承，但子类可以通过`super()`调用。

---

#### 4. 多态（Polymorphism）
- **定义**：同一接口或父类引用可以指向不同子类对象，调用对应子类的实现。
- **类型**：
  - **编译时多态**：方法重载（Overloading）。
  - **运行时多态**：方法重写（Overriding）+父类引用指向子类对象。

**多态示例**：
```java
public class Animal {
    public void makeSound() {
        System.out.println("Some sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Woof!");
    }
}

public class Cat extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal1 = new Dog(); // 父类引用指向子类对象
        Animal animal2 = new Cat();
        animal1.makeSound(); // 输出: Woof!
        animal2.makeSound(); // 输出: Meow!
    }
}
```

**方法重载示例**（编译时多态）：
```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
    
    public double add(double a, double b) {
        return a + b;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(2, 3)); // 输出: 5
        System.out.println(calc.add(2.5, 3.7)); // 输出: 6.2
    }
}
```

**优点**：
- 提高代码灵活性和扩展性。
- 父类引用可统一操作不同子类对象。

---

#### 5. 抽象类（Abstract Class）
- **定义**：使用`abstract`关键字声明，不能直接实例化，包含抽象方法（无实现）或普通方法。
- **用途**：定义通用模板，子类必须实现抽象方法。

**抽象类示例**：
```java
public abstract class Shape {
    public abstract double getArea(); // 抽象方法
    
    public void printInfo() { // 普通方法
        System.out.println("This is a shape.");
    }
}

public class Circle extends Shape {
    private double radius;
    
    public Circle(double radius) {
        this.radius = radius;
    }
    
    @Override
    public double getArea() {
        return Math.PI * radius * radius;
    }
}

public class Main {
    public static void main(String[] args) {
        Shape circle = new Circle(5.0);
        circle.printInfo(); // 输出: This is a shape.
        System.out.println("Area: " + circle.getArea()); // 输出: Area: 78.53981633974483
    }
}
```

**注意**：
- 抽象类可以包含非抽象方法。
- 子类必须实现所有抽象方法，否则也必须声明为`abstract`。

---

#### 6. 接口（Interface）
- **定义**：使用`interface`关键字，是一组方法的契约（默认`public abstract`），Java 8+支持`default`和`static`方法。
- **用途**：实现多继承效果，定义标准行为。

**接口示例**：
```java
public interface Flyable {
    void fly(); // 抽象方法
    
    default void show() { // 默认方法
        System.out.println("I can fly!");
    }
}

public class Bird implements Flyable {
    @Override
    public void fly() {
        System.out.println("Bird is flying.");
    }
}

public class Main {
    public static void main(String[] args) {
        Bird bird = new Bird();
        bird.fly(); // 输出: Bird is flying.
        bird.show(); // 输出: I can fly!
    }
}
```

**多接口示例**：
```java
public interface Swimmable {
    void swim();
}

public class Duck implements Flyable, Swimmable {
    @Override
    public void fly() {
        System.out.println("Duck is flying.");
    }
    
    @Override
    public void swim() {
        System.out.println("Duck is swimming.");
    }
}

public class Main {
    public static void main(String[] args) {
        Duck duck = new Duck();
        duck.fly(); // 输出: Duck is flying.
        duck.swim(); // 输出: Duck is swimming.
    }
}
```

**注意**：
- 类通过`implements`实现接口，必须实现所有抽象方法。
- 接口支持多实现，弥补Java单继承的限制。

---

### 三、其他重要概念

1. **构造方法（Constructor）**：
   - 用于初始化对象，方法名与类名相同，无返回值。
   - 默认提供无参构造，若定义有参构造需手动提供无参构造。
   ```java
   public class Student {
       String name;
       
       public Student(String name) {
           this.name = name;
       }
   }
   ```

2. **`this`和`super`**：
   - `this`：引用当前对象，区分成员变量和参数。
   - `super`：调用父类构造方法或方法。
   ```java
   public class Student extends Person {
       public Student(String name) {
           super(name); // 调用父类构造
       }
   }
   ```

3. **方法重写（Override）与重载（Overload）**：
   - **重写**：子类重新定义父类方法，签名相同。
   - **重载**：同一类中方法名相同，参数列表不同。

4. **final关键字**：
   - 修饰类：不可被继承（如`String`）。
   - 修饰方法：不可被重写。
   - 修饰变量：值不可更改（常量）。
   ```java
   final class FinalClass {
       final int VALUE = 10;
       final void method() {
           System.out.println("Final method");
       }
   }
   ```

5. **static关键字**：
   - 修饰属性/方法：属于类，不依赖对象。
   ```java
   public class Counter {
       static int count = 0;
       
       Counter() {
           count++;
       }
   }
   ```

---

### 四、注意事项
1. **访问修饰符**：
   - `public`：公开访问。
   - `protected`：同包或子类访问。
   - `default`（无修饰符）：同包访问。
   - `private`：类内部访问。

2. **对象初始化**：
   - 属性默认值：`int`为0，引用类型为`null`。
   - 构造方法确保对象初始化。

3. **抽象类 vs 接口**：
   - 抽象类可包含实现，接口（Java 8前）仅定义抽象方法。
   - 接口支持多实现，抽象类支持单继承。

4. **性能与设计**：
   - 过度使用继承可能导致耦合，优先考虑组合或接口。
   - 封装提高代码可维护性，尽量隐藏实现细节。

---

### 五、总结
- **核心概念**：类与对象、封装、继承、多态、抽象类、接口。
- **关键特性**：
  - 封装：隐藏数据，暴露接口。
  - 继承：复用代码，扩展功能。
  - 多态：灵活调用子类实现。
  - 抽象类/接口：定义规范，增强扩展性。
