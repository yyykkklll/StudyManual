# let 和 var的主要区别

## 1. 作用域（Scope）

- `var` **是函数作用域（Function Scope）**，即变量的作用域仅限于所在的函数。
- `let` **是块级作用域（Block Scope）**，即变量的作用域仅限于 `{}` 代码块内部。

**示例**

```javascript
function testScope() {
    if (true) {
        var a = 10;
        let b = 20;
    }
    console.log(a); // ✅ 10（var 变量在整个函数内可访问）
    console.log(b); // ❌ ReferenceError: b is not defined（let 变量仅在 if 代码块内有效）
}

testScope();
```

**总结**

- `var` 变量可以跨越 `{}` 代码块，在整个函数内部可用。
- `let` 变量只在 `{}` 代码块内部有效，避免了不必要的变量污染。

## 2. 变量提升（Hoisting）

- `var` **会被提升（Hoisting）到作用域的顶部，但值不会提升**，未赋值时默认为 `undefined`。
- `let` **也会被提升，但不会初始化**，在访问前会报 `ReferenceError`（称为“暂时性死区”）。

**示例**

```javascript
console.log(x); // ✅ undefined（var 变量提升）
var x = 5;

console.log(y); // ❌ ReferenceError: Cannot access 'y' before initialization
let y = 10;
```

**总结**

- `var` 变量声明会被提升到顶部，但值不会提升，所以访问它时会得到 `undefined`。
- `let` 变量也会提升，但不会初始化，因此在赋值前访问会报错（暂时性死区，TDZ）。

## 3. 变量可重复声明

- `var` **允许在同一作用域内重复声明**，但容易引发问题。
- `let` **不允许在同一作用域内重复声明**，可以减少变量覆盖的错误。

**示例**

```javascript
var a = 10;
var a = 20; // ✅ 不会报错，a 变成 20

let b = 30;
let b = 40; // ❌ SyntaxError: Identifier 'b' has already been declared
```

**总结**

- `var` 允许重复声明变量，可能导致意外覆盖变量值。
- `let` 不允许重复声明，能避免变量名冲突的错误。

## 4. 是否绑定到全局对象（Window 对象）

- `var` **声明的变量会绑定到 `window`（全局对象）**，可以通过 `window.varName` 访问。
- `let` **不会绑定到 `window`**，更安全。

**示例**

```javascript
var globalVar = "Hello";
let globalLet = "World";

console.log(window.globalVar); // ✅ "Hello"
console.log(window.globalLet); // ❌ undefined
```

**总结**

- `var` 在全局作用域下声明的变量会成为 `window` 对象的属性。
- `let` 则不会绑定到 `window`，更加安全，避免了污染全局环境。

## 5. 在 `for` 循环中的行为

- `var` **在 `for` 循环中不会创建块级作用域**，循环中的变量在外部仍然可见。
- `let` **在 `for` 循环中是块级作用域**，每次迭代都会创建新的作用域。

**示例**

```javascript
for (var i = 0; i < 3; i++) {
    setTimeout(() => console.log(i), 1000); // 3, 3, 3
}

for (let j = 0; j < 3; j++) {
    setTimeout(() => console.log(j), 1000); // 0, 1, 2
}
```

**为什么 `var` 输出 `3, 3, 3`？**

- `var` 没有块级作用域，循环结束后 `i = 3`，所有 `setTimeout` 执行时访问的 `i` 都是 `3`。
- `let` 具有块级作用域，每次循环都会创建一个新的 `j`，所以 `setTimeout` 访问的是不同的 `j` 值。

## 6. 总结

| 特性                      | `var`                        | `let`                        |
| ------------------------- | ---------------------------- | ---------------------------- |
| **作用域**                | 函数作用域                   | 块级作用域                   |
| **变量提升**              | 提升但初始化为 `undefined`   | 提升但不初始化（暂时性死区） |
| **可重复声明**            | 允许                         | 不允许                       |
| **绑定 `window`**         | 是                           | 否                           |
| **在 `for` 循环中的行为** | 共享作用域，循环变量不会独立 | 每次迭代创建新的作用域       |

**什么时候使用 `let` 而不是 `var`？**

> **最佳实践**：在现代 JavaScript 代码中，**应始终使用 `let`**，除非你需要 `const`（不可变变量）。

- `let` **更安全**，不会导致变量覆盖问题。
- `let` **避免了变量提升导致的 `undefined` 问题**。
- `let` **在 `for` 循环中作用域正确**，不会导致意外的变量共享。

**总结：用 `let` 代替 `var` 是更好的习惯！** 🚀