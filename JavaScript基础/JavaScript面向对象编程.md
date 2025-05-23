# JavaScript面向对象编程

## 1.JavaScript对象

**JavaScript 中创建对象的方式**

在 JavaScript 中，对象（Object）是一种非常重要的数据结构，用于存储**键值对（key-value pairs）**。创建对象有多种方式，每种方式都有自己的特点和适用场景。

1. **对象字面量（Object Literal）**

这是最简单、最常用的创建对象的方式，直接使用花括号 `{}` 定义键值对。

**语法**

```javascript
const 对象名 = { 键1: 值1, 键2: 值2 };
```

**示例**

```javascript
const person = {
  name: "小明",
  age: 20,
  sayHello: function() {
    console.log("你好，我是" + this.name);
  }
};

console.log(person.name); // 输出: 小明
person.sayHello(); // 输出: 你好，我是小明
```

**解释**

- `name` 和 `age` 是属性（properties），`sayHello` 是一个方法（method）。
- 使用 `.` 或 `[]` 可以访问对象的属性，比如 `person.name` 或 `person["age"]`。

**2. 使用 `new Object()` 构造函数**

通过内置的 `Object` 构造函数创建对象，然后逐一添加属性和方法。

**语法**

```javascript
const 对象名 = new Object();
对象名.键 = 值;
```

**示例**

```javascript
const car = new Object();
car.brand = "Toyota";
car.color = "blue";
car.drive = function() {
  console.log("正在开 " + this.brand);
};

console.log(car.color); // 输出: blue
car.drive(); // 输出: 正在开 Toyota
```

**解释**

- `new Object()` 创建一个空对象，然后通过 `.` 添加属性或方法。
- 这种方式功能上与对象字面量相同，但更繁琐，通常不常用。

3. **使用构造函数（Constructor Function）**

通过定义一个函数来创建多个类似的对象，类似于“模板”。

**语法**

```javascript
function 对象类型(参数1, 参数2) {
  this.键1 = 参数1;
  this.键2 = 参数2;
}
const 对象名 = new 对象类型(值1, 值2);
```

**示例**

```javascript
function Student(name, grade) {
  this.name = name;
  this.grade = grade;
  this.study = function() {
    console.log(this.name + " 在学习 " + this.grade + " 年级课程");
  };
}

const student1 = new Student("小红", 3);
const student2 = new Student("小刚", 5);

student1.study(); // 输出: 小红 在学习 3 年级课程
student2.study(); // 输出: 小刚 在学习 5 年级课程
```

**解释**

- `this` 指向新创建的对象实例。
- 使用 `new` 关键字调用构造函数，生成一个新对象。
- 适合创建多个结构相同的对象。

4. **使用 `Object.create()` 方法**

通过指定一个原型对象来创建新对象，新对象会继承原型对象的属性。

语法

```javascript
const 新对象 = Object.create(原型对象);
```

示例

```javascript
const animal = {
  eat: function() {
    console.log("我在吃东西");
  }
};

const dog = Object.create(animal);
dog.bark = function() {
  console.log("汪汪");
};

dog.eat(); // 输出: 我在吃东西（继承自 animal）
dog.bark(); // 输出: 汪汪
```

解释

- `dog` 继承了 `animal` 的属性和方法，同时可以添加自己的属性。
- 这种方式常用于实现继承。

5. **使用 `class` 语法（ES6 引入）**

ES6 引入了 `class` 关键字，提供了一种更现代、更清晰的方式来创建对象，类似于其他面向对象语言。

**语法**

```javascript
class 类名 {
  constructor(参数1, 参数2) {
    this.键1 = 参数1;
    this.键2 = 参数2;
  }
  方法名() {
    // 方法逻辑
  }
}
const 对象名 = new 类名(值1, 值2);
```

**示例**

```javascript
class Book {
  constructor(title, author) {
    this.title = title;
    this.author = author;
  }
  read() {
    console.log("我在读 " + this.title + " by " + this.author);
  }
}

const book1 = new Book("JavaScript 入门", "张三");
book1.read(); // 输出: 我在读 JavaScript 入门 by 张三
```

解释

- `constructor` 是类的构造函数，用于初始化对象。
- `class` 是构造函数的“语法糖”，更直观，适合面向对象编程。

**总结**

| 方法              | 特点                   | 适用场景           |
| ----------------- | ---------------------- | ------------------ |
| 对象字面量        | 简单直接               | 单个对象快速创建   |
| `new Object()`    | 手动添加属性，较繁琐   | 不常用，了解即可   |
| 构造函数          | 可批量创建类似对象     | 需要多个相似对象时 |
| `Object.create()` | 基于原型创建，强调继承 | 需要继承时         |
| `class`           | 现代语法，清晰面向对象 | 复杂项目中推荐使用 |

---

## 2.多态和继承

**JavaScript 中的多态和继承**

现在进入面向对象编程（OOP）的两个核心概念：**继承**和**多态**。我会详细讲解它们的定义、在 JavaScript 中的实现方式，并提供清晰的例子帮助你理解。

---

### 2.1 继承（Inheritance）

**什么是继承？**

继承是指一个对象（或类）可以获取另一个对象（或类）的属性和方法。子类（派生类）继承父类（基类）的特性，并可以扩展或修改这些特性。继承的目的是代码复用和建立对象之间的层次关系。

**JavaScript 中的实现**

JavaScript 是基于原型的语言，继承主要通过**原型链（Prototype Chain）**实现。ES6 引入的 `class` 语法让继承更直观，但底层仍是原型机制。

使用构造函数和原型实现继承

在 ES5 中，继承通过构造函数和原型链实现。

**示例**

```javascript
// 父类：动物
function Animal(name) {
  this.name = name;
}
Animal.prototype.eat = function() {
  console.log(`${this.name} 在吃东西`);
};

// 子类：狗
function Dog(name, breed) {
  Animal.call(this, name); // 继承属性
  this.breed = breed;
}
// 继承方法
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog; // 修正 constructor
Dog.prototype.bark = function() {
  console.log(`${this.name} 在汪汪叫`);
};

// 创建实例
const dog = new Dog("旺财", "哈士奇");
dog.eat();  // 输出: 旺财 在吃东西
dog.bark(); // 输出: 旺财 在汪汪叫
```

**解释**

- `Animal.call(this, name)`：调用父类的构造函数，继承属性。
- `Dog.prototype = Object.create(Animal.prototype)`：将子类的原型指向父类的原型副本，继承方法。
- `Dog.prototype.constructor = Dog`：修正构造函数指向。

**使用 `class` 语法（ES6）**

ES6 的 `class` 和 `extends` 提供了更现代的继承方式。

**示例**

```javascript
// 父类
class Animal {
  constructor(name) {
    this.name = name;
  }
  eat() {
    console.log(`${this.name} 在吃东西`);
  }
}

// 子类
class Cat extends Animal {
  constructor(name, color) {
    super(name); // 调用父类的构造函数
    this.color = color;
  }
  meow() {
    console.log(`${this.name} 在喵喵叫`);
  }
}

// 创建实例
const cat = new Cat("小花", "橘色");
cat.eat();  // 输出: 小花 在吃东西
cat.meow(); // 输出: 小花 在喵喵叫
```

**解释**

- `extends`：指定继承关系。
- `super()`：调用父类的构造函数，必须在子类中使用 `this` 前调用。
- 子类可以添加自己的属性和方法。

---

### 2.2 多态（Polymorphism）

**什么是多态？**

多态是指同一个方法在不同对象上表现出不同的行为。多态通常与继承结合使用，子类可以重写（override）父类的方法，以实现特定行为。

**JavaScript 中的实现**

JavaScript 的多态通过方法重写和动态类型实现。由于 JavaScript 是弱类型语言，多态非常灵活。

**示例 1：方法重写实现多态**

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }
  speak() {
    console.log(`${this.name} 发出声音`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} 汪汪叫`);
  }
}

class Bird extends Animal {
  speak() {
    console.log(`${this.name} 叽叽叫`);
  }
}

// 测试多态
const animals = [
  new Animal("未知生物"),
  new Dog("旺财"),
  new Bird("小黄")
];

animals.forEach(animal => animal.speak());
// 输出:
// 未知生物 发出声音
// 旺财 汪汪叫
// 小黄 叽叽叫
```

**解释**

- `speak()` 方法在父类 `Animal` 中定义。
- 子类 `Dog` 和 `Bird` 重写了 `speak()`，实现不同的行为。
- 在循环中，`animal.speak()` 根据对象类型调用相应的方法，这就是多态。

**示例 2：动态类型实现多态**

```javascript
function makeAnimalSpeak(animal) {
  animal.speak(); // 不关心具体类型，只要有 speak 方法
}

const dog = {
  name: "小黑",
  speak: function() {
    console.log(`${this.name} 汪汪`);
  }
};

const duck = {
  name: "唐老鸭",
  speak: function() {
    console.log(`${this.name} 嘎嘎`);
  }
};

makeAnimalSpeak(dog);  // 输出: 小黑 汪汪
makeAnimalSpeak(duck); // 输出: 唐老鸭 嘎嘎
```

**解释**

- `makeAnimalSpeak` 函数不关心传入的对象具体是什么类型，只要它有 `speak` 方法即可。
- 这种“鸭子类型”（Duck Typing）是 JavaScript 多态的另一种体现：如果它像鸭子一样走路和叫唤，那就是鸭子。

**继承与多态的结合**

继承为多态提供了基础。多态的核心是子类可以根据需要改变父类的行为。

**综合示例**

```javascript
class Vehicle {
  constructor(name) {
    this.name = name;
  }
  move() {
    console.log(`${this.name} 在移动`);
  }
}

class Car extends Vehicle {
  move() {
    console.log(`${this.name} 在公路上行驶`);
  }
}

class Plane extends Vehicle {
  move() {
    console.log(`${this.name} 在天上飞`);
  }
}

const vehicles = [new Car("汽车"), new Plane("飞机")];
vehicles.forEach(v => v.move());
// 输出:
// 汽车 在公路上行驶
// 飞机 在天上飞
```

**解释**

- `Vehicle` 是父类，定义了通用方法 `move()`。
- `Car` 和 `Plane` 继承并重写了 `move()`，表现出不同行为。
- 多态让 `v.move()` 根据对象类型动态调用正确的方法。

**总结**

| 概念 | 定义                         | JavaScript 实现方式                        |
| ---- | ---------------------------- | ------------------------------------------ |
| 继承 | 子类获取父类的属性和方法     | 原型链（ES5）、`class` 和 `extends`（ES6） |
| 多态 | 同一方法在不同对象上不同行为 | 方法重写、鸭子类型                         |

**优点**

- **继承**：代码复用，减少重复。
- **多态**：灵活性高，扩展性强。

**注意点**

- 使用 `super` 时确保正确调用父类方法。
- 重写方法时注意是否需要保留父类逻辑（可以用 `super.方法名()` 调用父类方法）。
