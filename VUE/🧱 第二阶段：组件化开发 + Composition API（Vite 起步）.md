## 🧱 第二阶段：组件化开发 + Composition API（Vite 起步）

### 🎯 学习目标
1. 理解 Vue 组件结构
2. 掌握 `props` 和 `emit` 通信机制
3. 熟练使用 Composition API

---

## 📖 学习内容

### 1. ✅ 安装 Vite 并初始化 Vue3 项目

Vite 是一个现代化的前端构建工具，速度快、配置简单，非常适合 Vue3 项目。

#### 步骤：
1. 确保你的环境安装了 Node.js（建议版本 16 或以上）。
2. 使用以下命令初始化一个 Vue3 项目：

```bash
# 使用 npm 初始化项目
npm create vite@latest my-vue-app -- --template vue

# 进入项目目录
cd my-vue-app

# 安装依赖
npm install

# 启动开发服务器
npm run dev
```

3. 打开浏览器，访问 `http://localhost:5173`，你会看到 Vite 提供的默认 Vue 项目页面。

#### 说明：
- `npm create vite@latest` 会让你选择项目模板，我们选择 `vue`。
- Vite 会自动生成一个简单的 Vue3 项目，包含基本的文件结构。
- `npm run dev` 启动开发服务器，支持热更新（代码修改后页面自动刷新）。

---

### 2. ✅ 项目结构解析（main.js、App.vue）

初始化后的项目结构如下（仅列出核心文件）：

```plaintext
my-vue-app/
├── public/                # 静态资源
├── src/
│   ├── assets/           # 图片、CSS 等静态资源
│   ├── components/       # 组件存放目录
│   ├── App.vue          # 根组件
│   ├── main.js          # 项目入口文件
├── package.json          # 项目依赖和脚本
```

#### main.js 解析
`main.js` 是项目的入口文件，负责创建 Vue 应用并挂载到 HTML。

```javascript
// src/main.js
import { createApp } from 'vue' // 从 vue 包导入 createApp 函数
import App from './App.vue' // 导入根组件 App.vue

// 创建 Vue 应用实例并挂载到 #app 元素
createApp(App).mount('#app')
```

**说明**：
- `createApp(App)` 创建一个 Vue 应用实例，`App` 是根组件。
- `.mount('#app')` 将应用挂载到 HTML 中的 `<div id="app"></div>`。

#### App.vue 解析
`App.vue` 是项目的根组件，通常作为其他组件的容器。

```html
<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>Welcome to Vue3!</h1>
  </div>
</template>

<script>
export default {
  name: 'App' // 组件名称
}
</script>

<style>
#app {
  text-align: center;
  margin-top: 60px;
}
</style>
```

**说明**：
- `<template>` 定义组件的 HTML 模板。
- `<script>` 定义组件的 JavaScript 逻辑（Vue2 使用 Options API，这里我们将改为 Composition API）。
- `<style>` 定义组件的 CSS 样式，支持 `scoped`（样式仅作用于当前组件）。

---

### 3. ✅ 单文件组件 `.vue` 格式

Vue3 使用单文件组件（SFC，Single File Component），一个 `.vue` 文件包含三部分：
- `<template>`：HTML 模板
- `<script>`：JavaScript 逻辑（支持 Composition API 或 Options API）
- `<style>`：CSS 样式（可选 `scoped`）

#### 示例：创建一个简单的组件
在 `src/components/` 下创建 `HelloWorld.vue`：

```html
<!-- src/components/HelloWorld.vue -->
<template>
  <div>
    <h2>{{ message }}</h2>
    <button @click="changeMessage">Change Message</button>
  </div>
</template>

<script>
import { ref } from 'vue' // 导入 ref

export default {
  name: 'HelloWorld',
  setup() {
    // 定义响应式数据
    const message = ref('Hello, Vue3!')

    // 定义方法
    function changeMessage() {
      message.value = 'Hello, Composition API!'
    }

    // 返回给模板使用的变量和方法
    return {
      message,
      changeMessage
    }
  }
}
</script>

<style scoped>
h2 {
  color: #42b983;
}
</style>
```

**说明**：
- `<template>` 使用 `{{ message }}` 展示响应式数据。
- `<script>` 使用 Composition API 的 `setup` 函数，`ref` 创建响应式变量。
- `<style scoped>` 确保样式仅作用于当前组件。
- `@click` 是 Vue 的事件绑定指令，点击按钮触发 `changeMessage` 方法。

---

### 4. ✅ 组件嵌套、注册、拆分

Vue 组件可以嵌套，父组件通过引入子组件来构建复杂的页面结构。

#### 示例：组件嵌套
1. 在 `src/components/` 下创建 `ChildComponent.vue`：

```html
<!-- src/components/ChildComponent.vue -->
<template>
  <div>
    <p>我是子组件！</p>
  </div>
</template>

<script>
export default {
  name: 'ChildComponent'
}
</script>
```

2. 在 `App.vue` 中引入并使用 `ChildComponent`：

```html
<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>根组件</h1>
    <HelloWorld />
    <ChildComponent />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import ChildComponent from './components/ChildComponent.vue'

export default {
  name: 'App',
  components: {
    HelloWorld, // 注册组件
    ChildComponent
  }
}
</script>
```

**说明**：
- 在 `<script>` 中通过 `import` 引入子组件，并通过 `components` 选项注册。
- 注册后，子组件可以在 `<template>` 中以标签形式使用（如 `<HelloWorld />`）。
- 组件可以无限嵌套，适合拆分复杂的页面结构。

---

### 5. ✅ 父子通信

Vue 组件通过 `props` 和 `emit` 实现父子通信。

#### 父传子：`props`
父组件通过 `props` 向子组件传递数据。

##### 示例：
1. 修改 `ChildComponent.vue` 接收 `props`：

```html
<!-- src/components/ChildComponent.vue -->
<template>
  <div>
    <p>来自父组件的数据：{{ parentMessage }}</p>
  </div>
</template>

<script>
export default {
  name: 'ChildComponent',
  props: {
    parentMessage: String // 定义 props，指定类型为 String
  }
}
</script>
```

2. 在 `App.vue` 中传递数据：

```html
<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>根组件</h1>
    <ChildComponent parentMessage="Hello from Parent!" />
  </div>
</template>

<script>
import ChildComponent from './components/ChildComponent.vue'

export default {
  name: 'App',
  components: {
    ChildComponent
  }
}
</script>
```

**说明**：
- `props` 在子组件中定义，指定数据类型（如 `String`）。
- 父组件通过属性（如 `parentMessage`）传递数据。
- 子组件通过 `{{ parentMessage }}` 使用父组件传递的数据。

#### 子传父：`emit`
子组件通过 `$emit` 触发事件通知父组件。

##### 示例：
1. 修改 `ChildComponent.vue` 触发事件：

```html
<!-- src/components/ChildComponent.vue -->
<template>
  <div>
    <p>来自父组件的数据：{{ parentMessage }}</p>
    <button @click="sendMessage">发送消息给父组件</button>
  </div>
</template>

<script>
export default {
  name: 'ChildComponent',
  props: {
    parentMessage: String
  },
  setup(props, { emit }) { // 使用 setup 语法，解构 emit
    function sendMessage() {
      emit('child-event', 'Message from Child!') // 触发自定义事件
    }
    return { sendMessage }
  }
}
</script>
```

2. 在 `App.vue` 中监听事件：

```html
<!-- src/App.vue -->
<template>
  <div id="app">
    <h1>根组件</h1>
    <p>子组件发送的消息：{{ childMessage }}</p>
    <ChildComponent parentMessage="Hello from Parent!" @child-event="handleChildEvent" />
  </div>
</template>

<script>
import { ref } from 'vue'
import ChildComponent from './components/ChildComponent.vue'

export default {
  name: 'App',
  components: {
    ChildComponent
  },
  setup() {
    const childMessage = ref('')

    // 处理子组件事件
    function handleChildEvent(message) {
      childMessage.value = message
    }

    return { childMessage, handleChildEvent }
  }
}
</script>
```

**说明**：
- 子组件通过 `emit('child-event', payload)` 触发自定义事件，携带数据。
- 父组件通过 `@child-event` 监听事件，并调用处理函数（如 `handleChildEvent`）。
- 使用 `ref` 存储子组件传递的数据，保持响应式。

---

### 6. ✅ Composition API 基础

Composition API 是 Vue3 的推荐方式，相比 Options API 更灵活，代码组织更清晰。

#### setup()
`setup` 是 Composition API 的入口函数，定义组件的逻辑。

##### 示例：
```html
<!-- src/components/HelloWorld.vue -->
<template>
  <div>
    <h2>{{ message }}</h2>
    <button @click="changeMessage">Change Message</button>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'HelloWorld',
  setup() {
    const message = ref('Hello, Vue3!')

    function changeMessage() {
      message.value = 'Changed!'
    }

    return { message, changeMessage }
  }
}
</script>
```

**说明**：
- `setup` 是组件的核心函数，执行在组件创建时。
- 返回的对象中的属性和方法可直接在模板中使用。
- `setup` 不使用 `this`，避免 Options API 的 `this` 混淆。

#### ref() 与 reactive()
- `ref`：用于创建单一的响应式变量（如字符串、数字）。
- `reactive`：用于创建复杂的响应式对象。

##### 示例：
```html
<!-- src/components/ReactiveDemo.vue -->
<template>
  <div>
    <p>计数器：{{ count }}</p>
    <p>用户信息：{{ user.name }} - {{ user.age }}</p>
    <button @click="increment">加 1</button>
    <button @click="updateUser">更新用户</button>
  </div>
</template>

<script>
import { ref, reactive } from 'vue'

export default {
  name: 'ReactiveDemo',
  setup() {
    // ref 创建单一响应式变量
    const count = ref(0)

    // reactive 创建响应式对象
    const user = reactive({
      name: '张三',
      age: 20
    })

    // 方法
    function increment() {
      count.value++ // ref 需要 .value 修改
    }

    function updateUser() {
      user.name = '李四' // reactive 直接修改属性
      user.age = 21
    }

    return { count, user, increment, updateUser }
  }
}
</script>
```

**说明**：
- `ref` 变量在 JS 中通过 `.value` 访问和修改，在模板中直接用变量名。
- `reactive` 对象的属性可以直接修改，Vue 会自动追踪变化。
- 选择建议：简单数据用 `ref`，复杂对象用 `reactive`。

#### computed() 与 watch()
- `computed`：创建计算属性，基于响应式数据计算结果。
- `watch`：监听响应式数据的变化，执行副作用。

##### 示例：
```html
<!-- src/components/ComputedWatch.vue -->
<template>
  <div>
    <p>输入名字：<input v-model="name" /></p>
    <p>名字长度：{{ nameLength }}</p>
    <p>监听到的名字：{{ watchedName }}</p>
  </div>
</template>

<script>
import { ref, computed, watch } from 'vue'

export default {
  name: 'ComputedWatch',
  setup() {
    const name = ref('')
    const watchedName = ref('')

    // 计算属性：名字长度
    const nameLength = computed(() => {
      return name.value.length
    })

    // 监听 name 变化
    watch(name, (newValue, oldValue) => {
      watchedName.value = `新名字: ${newValue}，旧名字: ${oldValue}`
    })

    return { name, nameLength, watchedName }
  }
}
</script>
```

**说明**：
- `computed` 返回一个只读的响应式值，适合基于其他数据计算结果。
- `watch` 适合执行异步操作或复杂逻辑（如发送请求）。
- `v-model` 用于双向绑定输入框和 `name`。

---

### 7. 🚨 Vue 2 的 Options API：了解即可

Vue2 主要使用 Options API，代码组织基于 `data`、`methods`、`computed` 等选项。

#### 示例（Options API）：
```html
<!-- Vue2 风格 -->
<template>
  <div>
    <p>{{ count }}</p>
    <button @click="increment">加 1</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  }
}
</script>
```

**说明**：
- Options API 使用 `data` 定义数据，`methods` 定义方法，`this` 指向组件实例。
- Composition API 更灵活，推荐在 Vue3 中使用。
- 了解 Options API 有助于阅读旧项目代码，但新项目优先用 Composition API。

---

## 📝 实践任务：Todo List

我们将创建一个简单的 Todo List 应用，包含 `TodoList.vue` 和 `TodoItem.vue`，实现添加和删除任务功能，使用 `ref` 和 `computed` 管理响应式数据。

### 任务要求：
1. 拆分为 `TodoList.vue`（父组件）和 `TodoItem.vue`（子组件）。
2. 支持添加新任务。
3. 支持删除任务。
4. 使用 `ref` 和 `computed` 管理数据。

#### 1. 创建 TodoItem.vue
`TodoItem.vue` 表示单个任务项，接收任务数据并触发删除事件。

```html
<!-- src/components/TodoItem.vue -->
<template>
  <div class="todo-item">
    <span>{{ todo.text }}</span>
    <button @click="removeTodo">删除</button>
  </div>
</template>

<script>
export default {
  name: 'TodoItem',
  props: {
    todo: Object // 接收任务对象
  },
  setup(props, { emit }) {
    function removeTodo() {
      emit('remove', props.todo.id) // 触发删除事件，传递任务 ID
    }
    return { removeTodo }
  }
}
</script>

<style scoped>
.todo-item {
  display: flex;
  justify-content: space-between;
  padding: 8px;
  border-bottom: 1px solid #eee;
}
button {
  background: #ff4d4f;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
```

#### 2. 创建 TodoList.vue
`TodoList.vue` 管理任务列表，处理添加和删除逻辑。

```html
<!-- src/components/TodoList.vue -->
<template>
  <div class="todo-list">
    <h2>Todo List</h2>
    <div>
      <input v-model="newTodo" placeholder="输入新任务" @keyup.enter="addTodo" />
      <button @click="addTodo">添加</button>
    </div>
    <p>任务总数：{{ totalTodos }}</p>
    <TodoItem
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @remove="removeTodo"
    />
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import TodoItem from './TodoItem.vue'

export default {
  name: 'TodoList',
  components: {
    TodoItem
  },
  setup() {
    // 响应式任务列表
    const todos = ref([
      { id: 1, text: '学习 Vue3' },
      { id: 2, text: '完成 Todo List' }
    ])

    // 新任务输入框
    const newTodo = ref('')

    // 计算属性：任务总数
    const totalTodos = computed(() => todos.value.length)

    // 添加任务
    function addTodo() {
      if (newTodo.value.trim()) {
        todos.value.push({
          id: Date.now(), // 使用时间戳作为唯一 ID
          text: newTodo.value
        })
        newTodo.value = '' // 清空输入框
      }
    }

    // 删除任务
    function removeTodo(id) {
      todos.value = todos.value.filter(todo => todo.id !== id)
    }

    return { todos, newTodo, totalTodos, addTodo, removeTodo }
  }
}
</script>

<style scoped>
.todo-list {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
}
input {
  padding: 5px;
  margin-right: 10px;
}
button {
  background: #42b983;
  color: white;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
}
</style>
```

#### 3. 在 App.vue 中使用 TodoList
```html
<!-- src/App.vue -->
<template>
  <div id="app">
    <TodoList />
  </div>
</template>

<script>
import TodoList from './components/TodoList.vue'

export default {
  name: 'App',
  components: {
    TodoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
```

#### 运行结果：
- 打开浏览器，访问 `http://localhost:5173`。
- 你会看到一个 Todo List 页面：
  - 显示初始的两个任务（“学习 Vue3”和“完成 Todo List”）。
  - 输入框支持输入新任务，按回车或点击“添加”按钮添加。
  - 每个任务项右侧有“删除”按钮，点击可删除任务。
  - 显示任务总数，自动更新。

---

## 📚 总结

1. **Vite 初始化**：使用 Vite 创建 Vue3 项目，了解 `main.js` 和 `App.vue`。
2. **单文件组件**：掌握 `.vue` 文件的结构（模板、脚本、样式）。
3. **组件嵌套与注册**：通过 `components` 注册子组件并在父组件中使用。
4. **父子通信**：
   - 使用 `props` 实现父传子。
   - 使用 `emit` 实现子传父。
5. **Composition API**：
   - 使用 `setup` 组织逻辑。
   - 使用 `ref` 和 `reactive` 创建响应式数据。
   - 使用 `computed` 和 `watch` 处理计算和监听。
6. **实践任务**：完成了一个简单的 Todo List 应用，包含组件拆分、数据管理和交互功能。

