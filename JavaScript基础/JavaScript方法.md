# JavaScript 中的方法：声明与使用方式

## **什么是方法？**

在 JavaScript 中，方法是一个与对象关联的函数，通常用来描述对象的行为。例如，一个 `Person` 对象可能有 `walk` 或 `talk` 方法。方法本质上是对象的属性，其值是一个函数。

## **方法的声明方式**

### **1.在对象字面量中声明方法**
直接在对象字面量中定义方法，语法简洁。

**语法**
```javascript
const 对象 = {
  方法名: function(参数) {
    // 方法逻辑
  }
};
```

**示例**
```javascript
const person = {
  name: "小明",
  greet: function() {
    console.log(`你好，我是 ${this.name}`);
  }
};

person.greet(); // 输出: 你好，我是 小明
```

**ES6 简写**

ES6 允许省略 `function` 关键字，直接写方法名和参数。
```javascript
const person = {
  name: "小明",
  greet() { // 简写形式
    console.log(`你好，我是 ${this.name}`);
  }
};

person.greet(); // 输出: 你好，我是 小明
```

**解释**
- `this` 指向调用方法的对象（这里是 `person`）。
- ES6 简写更简洁，推荐使用。

---

### 2. **在构造函数中声明方法**
通过构造函数为对象实例添加方法。

**语法**
```javascript
function 对象类型(参数) {
  this.方法名 = function() {
    // 方法逻辑
  };
}
```

**示例**
```javascript
function Car(model) {
  this.model = model;
  this.drive = function() {
    console.log(`我在开 ${this.model}`);
  };
}

const car1 = new Car("特斯拉");
car1.drive(); // 输出: 我在开 特斯拉
```

**注意**
- 这种方式为每个实例创建独立的方法副本，浪费内存。
- 更好的做法是将方法定义在原型上（见下文）。

---

### 3. **在原型上声明方法**
将方法添加到构造函数的 `prototype`，所有实例共享同一个方法。

**语法**
```javascript
function 对象类型(参数) {
  this.属性 = 参数;
}
对象类型.prototype.方法名 = function() {
  // 方法逻辑
};
```

**示例**
```javascript
function Dog(name) {
  this.name = name;
}
Dog.prototype.bark = function() {
  console.log(`${this.name} 在汪汪叫`);
};

const dog1 = new Dog("旺财");
const dog2 = new Dog("小黑");

dog1.bark(); // 输出: 旺财 在汪汪叫
dog2.bark(); // 输出: 小黑 在汪汪叫
```

**解释**
- 方法定义在 `Dog.prototype` 上，所有 `Dog` 实例共享此方法，节省内存。
- 通过原型链，实例可以访问原型上的方法。

---

### 4. **使用 `class` 声明方法**
ES6 的 `class` 语法提供了一种更现代的方式声明方法。

**语法**
```javascript
class 类名 {
  constructor(参数) {
    this.属性 = 参数;
  }
  方法名() {
    // 方法逻辑
  }
}
```

**示例**
```javascript
class Student {
  constructor(name, grade) {
    this.name = name;
    this.grade = grade;
  }
  study() {
    console.log(`${this.name} 在学习 ${this.grade} 年级课程`);
  }
}

const student = new Student("小红", 3);
student.study(); // 输出: 小红 在学习 3 年级课程
```

**解释**
- 方法自动绑定到类的原型上，所有实例共享。
- 语法清晰，适合面向对象编程。

---

### 5. **箭头函数作为方法**
可以用箭头函数定义方法，但要注意 `this` 的行为。

**示例**
```javascript
const person = {
  name: "小刚",
  greet: () => {
    console.log(`你好，我是 ${this.name}`);
  }
};

person.greet(); // 输出: 你好，我是 undefined
```

**解释**
- 箭头函数没有自己的 `this`，它从定义时的外层作用域继承 `this`。
- 在对象字面量中，`this` 不会指向 `person`，通常是 `undefined`（在严格模式下）。
- 如果需要正确绑定 `this`，使用普通函数或显式绑定。

**正确用法**

箭头函数更适合用在回调或不需要动态 `this` 的场景：
```javascript
const person = {
  name: "小刚",
  greet() {
    setTimeout(() => {
      console.log(`你好，我是 ${this.name}`); // this 绑定到 person
    }, 1000);
  }
};

person.greet(); // 1 秒后输出: 你好，我是 小刚
```

---

## **方法的使用方式**

### 1. **直接调用**
通过对象调用方法，使用 `.` 或 `[]`。
```javascript
const cat = {
  name: "小花",
  meow() {
    console.log(`${this.name} 喵喵`);
  }
};

cat.meow();       // 输出: 小花 喵喵
cat["meow"]();    // 输出: 小花 喵喵
```

### 2. **传递参数**
方法可以接收参数，像普通函数一样使用。
```javascript
const calculator = {
  add(a, b) {
    return a + b;
  }
};

console.log(calculator.add(3, 5)); // 输出: 8
```

### 3. **使用 `call`、`apply` 或 `bind` 改变 `this`**
这些方法可以控制方法中的 `this` 指向。

**示例**：`call`
```javascript
const person1 = { name: "小明" };
const person2 = { name: "小红" };

function sayHello() {
  console.log(`你好，我是 ${this.name}`);
}

sayHello.call(person1); // 输出: 你好，我是 小明
sayHello.call(person2); // 输出: 你好，我是 小红
```

**示例**：`bind`
```javascript
const greetPerson1 = sayHello.bind(person1);
greetPerson1(); // 输出: 你好，我是 小明
```

```
# 文件：model.py
import torch
import torch.nn as nn
import torch.nn.functional as F
from vit import DualViT, TransformerEncoder

def weights_init_kaiming(m):
    """
    使用Kaiming初始化卷积层、线性层和BatchNorm1d的权重
    """
    classname = m.__class__.__name__
    if 'Conv' in classname:
        nn.init.kaiming_normal_(m.weight.data, a=0, mode='fan_in')
    elif 'Linear' in classname:
        nn.init.kaiming_normal_(m.weight.data, a=0, mode='fan_out')
        nn.init.zeros_(m.bias.data)
    elif 'BatchNorm1d' in classname:
        nn.init.normal_(m.weight.data, 1.0, 0.01)
        nn.init.zeros_(m.bias.data)

def weights_init_classifier(m):
    """
    初始化分类器线性层的权重和偏置
    """
    if 'Linear' in m.__class__.__name__:
        nn.init.normal_(m.weight.data, 0, 0.001)
        if m.bias is not None:
            nn.init.zeros_(m.bias.data)

class Normalize(nn.Module):
    """
    对特征进行L2归一化
    """
    def __init__(self, power=2):
        super().__init__()
        self.power = power

    def forward(self, x):
        norm = x.pow(self.power).sum(1, keepdim=True).pow(1. / self.power)
        return x.div(norm)

class BaseViT(nn.Module):
    """
    基础ViT模型,提取特征层
    """
    def __init__(self, embed_dim=768, depth=12, num_heads=12, img_h=384, img_w=384):
        super().__init__()
        self.transformer = TransformerEncoder(embed_dim=embed_dim, depth=depth, num_heads=num_heads)
        self.n_patches = (img_h // 16) ** 2  # 根据动态 img_h 和 img_w 计算

    def forward(self, x):
        x = self.transformer(x)  # (B, n_patches, embed_dim)
        return x 

class DEEModule(nn.Module):
    def __init__(self, embed_dim, reduction=16):
        super().__init__()
        self.fc1 = nn.Conv1d(embed_dim, embed_dim // 4, kernel_size=3, stride=1, padding=1, dilation=1)
        self.fc2 = nn.Conv1d(embed_dim, embed_dim // 4, kernel_size=3, stride=1, padding=2, dilation=2)
        self.fc3 = nn.Conv1d(embed_dim, embed_dim // 4, kernel_size=3, stride=1, padding=3, dilation=3)
        self.fc_out = nn.Conv1d(embed_dim // 4, embed_dim, kernel_size=1)
        self.dropout = nn.Dropout(p=0.01)
        self.apply(weights_init_kaiming)
        self.scale = nn.Parameter(torch.tensor(1.0))  # 可学习的缩放因子

    def forward(self, x):
        x = x.transpose(1, 2)  # (B, embed_dim, n_patches)
        x1 = (self.fc1(x) + self.fc2(x) + self.fc3(x)) / 3
        x1 = self.fc_out(F.relu(x1))
        x1 = x1 * self.scale  # 缩放
        x1 = x1.transpose(1, 2)  # (B, n_patches, embed_dim)
        return self.dropout(x1)

class CNL(nn.Module):
    """
    Cross-Modal Non-local模块,适配ViT的序列化特征
    """
    def __init__(self, high_dim, low_dim, flag=0):
        super().__init__()
        self.g = nn.Conv1d(high_dim, low_dim, kernel_size=1)
        self.theta = nn.Conv1d(high_dim, low_dim, kernel_size=1)
        self.phi = nn.Conv1d(high_dim, low_dim, kernel_size=1)
        self.W = nn.Sequential(
            nn.Conv1d(low_dim, high_dim, kernel_size=1),
            nn.BatchNorm1d(high_dim)
        )
        nn.init.constant_(self.W[1].weight, 0.0)
        nn.init.constant_(self.W[1].bias, 0.0)

    def forward(self, x_h, x_l):
        B = x_h.size(0)
        x_h = x_h.transpose(1, 2)  # (B, embed_dim, n_patches)
        x_l = x_l.transpose(1, 2)  # (B, embed_dim, n_patches)
        g_x = self.g(x_l)  # (B, low_dim, n_patches)
        theta_x = self.theta(x_h)  # (B, low_dim, n_patches)
        phi_x = self.phi(x_l)  # (B, low_dim, n_patches)
        energy = torch.bmm(theta_x.transpose(1, 2), phi_x)  # (B, n_patches, n_patches)
        attention = energy / energy.size(-1)
        y = torch.bmm(attention, g_x.transpose(1, 2))  # (B, n_patches, low_dim)
        y = y.transpose(1, 2)  # (B, low_dim, n_patches)
        y = self.W(y)  # (B, high_dim, n_patches)
        return (y + x_h).transpose(1, 2)  # (B, n_patches, high_dim)

class PNL(nn.Module):
    """
    Pyramid Non-local模块,适配ViT的序列化特征
    """
    def __init__(self, high_dim, low_dim, reduc_ratio=2):
        super().__init__()
        self.g = nn.Conv1d(high_dim, low_dim // reduc_ratio, kernel_size=1)
        self.theta = nn.Conv1d(high_dim, low_dim // reduc_ratio, kernel_size=1)
        self.phi = nn.Conv1d(high_dim, low_dim // reduc_ratio, kernel_size=1)
        self.W = nn.Sequential(
            nn.Conv1d(low_dim // reduc_ratio, high_dim, kernel_size=1),
            nn.BatchNorm1d(high_dim)
        )
        nn.init.constant_(self.W[1].weight, 0.0)
        nn.init.constant_(self.W[1].bias, 0.0)

    def forward(self, x_h, x_l):
        B = x_h.size(0)
        x_h = x_h.transpose(1, 2)  # (B, embed_dim, n_patches)
        x_l = x_l.transpose(1, 2)  # (B, embed_dim, n_patches)
        g_x = self.g(x_l).transpose(1, 2)  # (B, n_patches, low_dim // reduc_ratio)
        theta_x = self.theta(x_h).transpose(1, 2)  # (B, n_patches, low_dim // reduc_ratio)
        phi_x = self.phi(x_l)  # (B, low_dim // reduc_ratio, n_patches)
        energy = torch.bmm(theta_x, phi_x)  # (B, n_patches, n_patches)
        attention = energy / energy.size(-1)
        y = torch.bmm(attention, g_x).transpose(1, 2)  # (B, low_dim // reduc_ratio, n_patches)
        y = self.W(y)  # (B, high_dim, n_patches)
        return (y + x_h).transpose(1, 2)  # (B, n_patches, high_dim)

class MFA_Block(nn.Module):
    """
    Multi-Feature Alignment块,适配ViT
    """
    def __init__(self, high_dim, low_dim, flag):
        super().__init__()
        self.CNL = CNL(high_dim, low_dim, flag)
        self.PNL = PNL(high_dim, low_dim)

    def forward(self, x, x0):
        z = self.CNL(x, x0)
        return self.PNL(z, x0)

class EmbedNet(nn.Module):
    def __init__(self, n_class, dataset, embed_dim=768, depth=12, num_heads=12, img_h=384, img_w=384):
        super(EmbedNet, self).__init__()
        self.dataset = dataset
        assert img_h == img_w, "EmbedNet assumes square input images (img_h == img_w)"
        img_size = img_h  # DualViT 使用单一的 img_size 参数
        self.n_patches = (img_size // 16) ** 2  # 假设 patch_size=16，与 DualViT 默认值一致

        # 初始化 backbone (DualViT)
        self.backbone = DualViT(
            img_size=img_size,        # 使用 img_h 作为 img_size
            patch_size=16,            # 默认值，与 VisualTransformer 一致
            in_channels=3,            # RGB 图像输入
            embed_dim=embed_dim,
            depth=depth,
            num_heads=num_heads,
            dropout=0.1               # 默认 dropout
        )

        # 初始化 BaseViT
        self.base_vit = BaseViT(embed_dim=embed_dim, depth=depth, num_heads=num_heads, img_h=img_h, img_w=img_w)

        # 初始化 MFA 和 DEE 模块
        self.MFA1 = MFA_Block(high_dim=embed_dim, low_dim=embed_dim // 2, flag=0)
        self.MFA2 = MFA_Block(high_dim=embed_dim, low_dim=embed_dim // 2, flag=1)
        self.MFA3 = MFA_Block(high_dim=embed_dim, low_dim=embed_dim // 2, flag=2) if dataset != 'regdb' else None
        self.DEE = DEEModule(embed_dim=embed_dim)

        # 池化层
        self.pool = nn.AdaptiveAvgPool1d(1)  # 适配 ViT 的序列特征

        # Bottleneck 和分类器
        self.bottleneck = nn.Sequential(
            nn.Linear(embed_dim, embed_dim),
            nn.BatchNorm1d(embed_dim),
            nn.ReLU()
        )
        self.bottleneck.apply(weights_init_kaiming)

        self.classifier = nn.Linear(embed_dim, n_class)
        self.classifier.apply(weights_init_classifier)

        # L2 归一化
        self.l2norm = Normalize(2)

    def forward(self, x1, x2, modal=0):
        x = self.backbone(x1, x2, modal)  # (B, n_patches, embed_dim)
        x_ = x
        x = self.base_vit(x)
        x_ = self.MFA1(x, x_)
        x = self.base_vit(x)
        x_ = self.MFA2(x, x_)
        if self.dataset == 'regdb':
            x_ = self.DEE(x_)
            x = self.base_vit(x)
        else:
            x = self.base_vit(x)
            x_ = self.MFA3(x, x_) if self.MFA3 else x
            x_ = self.DEE(x_)
            x = self.base_vit(x)
        
        x_ = F.normalize(x_, p=2, dim=2)  # 沿 embed_dim 维度归一化
        xp = self.pool(x_.transpose(1, 2)).squeeze(-1)  # (B, embed_dim)
        x_pool = xp
        feat = self.bottleneck(x_pool)

        if self.training:
            xps = x_.permute(0, 2, 1)  # (B, embed_dim, n_patches)
            batch_size = x_.size(0)
            n_patches = x_.size(1)
            if batch_size % 2 == 0:
                xp1, xp2 = torch.chunk(xps, 2, dim=0)
                xpss = torch.cat((xp2, xp1), dim=0)
                xpss_norm = F.normalize(xpss, p=2, dim=1)
                ortho_mat = torch.bmm(xpss_norm, xpss_norm.permute(0, 2, 1))
                ortho_mat.diagonal(dim1=1, dim2=2).zero_()
                loss_ort = torch.clamp(ortho_mat.abs().sum() / (batch_size * n_patches * (n_patches - 1)), min=0.0)
            else:
                raise ValueError("Batch size must be even for current loss computation.")
            return x_pool, self.classifier(feat), loss_ort
        return self.l2norm(x_pool), self.l2norm(feat)

# 确保 embed_net 可被导入
embed_net = EmbedNet
```

- `call(thisArg, arg1, arg2, ...)`：立即调用，参数逐个传递。
- `apply(thisArg, [args])`：立即调用，参数以数组传递。
- `bind(thisArg)`：返回新函数，不立即调用。

---

## **综合示例**
```javascript
class Pet {
  constructor(name, type) {
    this.name = name;
    this.type = type;
  }
  // 实例方法
  introduce() {
    console.log(`我是 ${this.name}，一种 ${this.type}`);
  }
  // 静态方法（只能通过类调用）
  static info() {
    console.log("宠物是人类的好朋友");
  }
}

const pet = new Pet("小白", "兔子");
pet.introduce();    // 输出: 我是 小白，一种 兔子
Pet.info();         // 输出: 宠物是人类的好朋友
```

**解释**
- `introduce` 是实例方法，绑定到原型上。
- `static info` 是静态方法，属于类本身，不能通过实例调用。

---

## **总结**
| 声明方式   | 特点                         | 适用场景             |
| ---------- | ---------------------------- | -------------------- |
| 对象字面量 | 简单直观                     | 单个对象快速定义     |
| 构造函数   | 每个实例独立方法             | 小规模对象（不推荐） |
| 原型       | 共享方法，节省内存           | 多实例复用方法       |
| `class`    | 现代语法，清晰结构           | 面向对象编程         |
| 箭头函数   | 无自身 `this`， lexical 绑定 | 回调或特定场景       |

---

## **练习**
1. 创建一个 `Book` 对象，包含 `title` 和 `author` 属性，添加一个 `read` 方法输出阅读信息。
2. 用 `class` 定义一个 `Animal` 类，包含 `eat` 方法，然后用原型或 `class` 添加一个新方法。

完成后可以给我看代码，我帮你检查！接下来想学什么？函数作用域、闭包，还是其他？