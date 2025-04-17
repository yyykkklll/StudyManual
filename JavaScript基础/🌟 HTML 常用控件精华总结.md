# 🌟 HTML 常用控件精华总结

------

## 🧾 1. 文本类输入控件（`<input>`）

### ✅ 单行文本输入

```html
<input type="text" placeholder="请输入内容">
```

### 🔐 密码输入

```html
<input type="password" placeholder="请输入密码">
```

### 📧 邮箱输入

```html
<input type="email" placeholder="example@mail.com">
```

------

## 🔘 2. 选择类控件

### ✅ 单选框（Radio）

一组选项中只能选一个，**必须设置相同的 name 才能互斥**：

```html
<input type="radio" name="gender" value="male"> 男
<input type="radio" name="gender" value="female"> 女
```

### ✅ 复选框（Checkbox）

可以选择多个：

```html
<input type="checkbox" name="hobby" value="music"> 音乐
<input type="checkbox" name="hobby" value="sports"> 运动
```

### 🔽 下拉选择框（Select）

```html
<select name="city">
  <option value="beijing">北京</option>
  <option value="shanghai">上海</option>
</select>
```

------

## 📝 3. 多行文本输入（`<textarea>`）

```html
<textarea rows="4" placeholder="请输入留言..."></textarea>
```

------

## 🧩 4. 按钮（`<button>` 和 `input[type=submit]`）

### ✅ 表单提交按钮

```html
<button type="submit">提交</button>
<!-- 或者 -->
<input type="submit" value="提交">
```

### 🚫 普通按钮（用于 JS 交互）

```html
<button type="button" onclick="alert('点击了按钮')">点击我</button>
```

------

## 📦 5. 表单容器（`<form>`）

```html
<form action="/submit" method="post">
  <!-- 各类控件放在这里 -->
</form>
```

常用属性：

- `action`: 提交的 URL
- `method`: `get` 或 `post`

------

## 🛠️ 常用属性汇总

| 属性          | 说明                           |
| ------------- | ------------------------------ |
| `placeholder` | 输入提示文字                   |
| `name`        | 控件名称，提交表单时作为 key   |
| `value`       | 默认值                         |
| `required`    | 是否必填                       |
| `checked`     | 是否默认选中（radio/checkbox） |
| `disabled`    | 是否禁用                       |

------

