# JavaScript流程控制流语句

### 1. **条件语句（if / else）**

根据条件执行不同代码块。

#### 语法

```javascript
if (条件) {
  // 条件为 true 时执行
} else if (另一个条件) {
  // 另一个条件为 true 时执行
} else {
  // 都不满足时执行
}
```

#### 示例

```javascript
let temperature = 25;
if (temperature > 30) {
  console.log("太热了！");
} else if (temperature > 20) {
  console.log("天气不错。");
} else {
  console.log("有点冷。");
}
// 输出: 天气不错。
```

---

### 2. **多分支语句（switch）**

根据表达式的值选择执行路径。

#### 语法

```javascript
switch (表达式) {
  case 值1:
    // 代码
    break;
  case 值2:
    // 代码
    break;
  default:
    // 默认代码
}
```

#### 示例

```javascript
let day = 3;
switch (day) {
  case 1:
    console.log("星期一");
    break;
  case 3:
    console.log("星期三");
    break;
  default:
    console.log("其他天");
}
// 输出: 星期三
```

#### 注意

- `break` 防止代码“贯穿”（fall-through）。
- `default` 是可选的默认分支。

---

### 3. **循环语句**

#### **for 循环**

重复执行固定次数。

##### 语法

```javascript
for (初始化; 条件; 更新) {
  // 循环体
}
```

##### 示例

```javascript
for (let i = 0; i < 5; i++) {
  console.log(`第 ${i} 次`);
}
// 输出: 第 0 次, 第 1 次, ..., 第 4 次
```

#### **while 循环**

条件为真时持续执行。

##### 语法

```javascript
while (条件) {
  // 循环体
}
```

##### 示例

```javascript
let count = 0;
while (count < 3) {
  console.log(count);
  count++;
}
// 输出: 0, 1, 2
```

#### **do...while 循环**

至少执行一次，然后根据条件继续。

##### 语法

```javascript
do {
  // 循环体
} while (条件);
```

##### 示例

```javascript
let num = 0;
do {
  console.log(num);
  num++;
} while (num < 3);
// 输出: 0, 1, 2
```

---

### 4. **循环控制**

- **break**：跳出循环。
- **continue**：跳过当前迭代，继续下一次。

#### 示例

```javascript
for (let i = 0; i < 5; i++) {
  if (i === 2) continue; // 跳过 i = 2
  if (i === 4) break;    // 在 i = 4 时退出
  console.log(i);
}
// 输出: 0, 1, 3
```

---

## **综合示例**

```javascript
let score = 75;
let message = score >= 60 ? "通过" : "未通过"; // 三元运算符

if (score >= 90) {
  console.log("优秀");
} else if (score >= 60) {
  console.log("合格");
} else {
  console.log("不及格");
}
// 输出: 合格

for (let i = 1; i <= 3; i++) {
  console.log(`第 ${i} 次尝试: ${message}`);
}
// 输出:
// 第 1 次尝试: 通过
// 第 2 次尝试: 通过
// 第 3 次尝试: 通过
```

