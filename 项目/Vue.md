## 网课链接

[09_列表渲染_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Rs4y127j8?p=9&vd_source=81d07727a431bd6b2d07b94e67a294fc)

## 初始化

### 清除npm

```cmd
npm cache verify
```

### npm换源

```c
   // 查询源
    npm config get registry

    // 更换国内源
    npm config set registry https://registry.npmmirror.com

    // 恢复官方源
    npm config set registry https://registry.npmjs.org

    // 删除注册表
    npm config delete registry
```

### 创建Vue项目

```c
npm init vue@latest
```

### 常用命令

```c  
cd vue-base  
npm install
npm run dev//运行这个项目
```

>  VITE v5.2.11  ready in 1571 ms
>
>  ➜  Local:   http://localhost:5173/
>  ➜  Network: use --host to expose
>  ➜  press h + enter to show help

### 创建命令

```c
npm create-vue project
npm cerate vue project
npm create-react project
npm init vue@latest
```

### 创建文件目录

>.vscode vscode工具的配置文件
>node_modules Vue项目的运行依赖文件 ---npm install
>public 资源文件夹(浏览器图标)
>src 源码文件夹
>.gitignore git忽略文件
>
>index .html 入口HTML文件
>
>package.json 信息描述文件
>README .md 注释文件
>vite.config.js vue配置文件

### Vue终端命令

>  Shortcuts
>  press r + enter to restart the server
>  press u + enter to show server url
>  press o + enter to open in browser
>  press c + enter to clear console
>  press q + enter to quit

## Vue基本知识

### 文本插值

```vue
<script>
export default{
  data(){
    return{
      msg:"神奇的语法"
    }
  }
}
//以上为文本插值的固定使用格式
</script>

<template>
 <h3>模版语法</h3>
 <p>{{msg}}</p>
</template>
```

### 属性绑定

```vue
<div id="app">
  <img v-bind:src="imgUrl" alt="">
  <a v-bind:href="url">百度一下</a>
</div>
<script src="../vue.js"></script>
<script>
    const app = new Vue({
        el: "#app",
        data: {
          imgUrl:'https://cn.vuejs.org/images/logo.svg',
          url:'http://www.baidu.com'
        },
        methods: {

        }
    })
</script>
```

删除vbind，null，unddefined

或者只用：

### 条件渲染

```vue
<template>
    <h3>
        条件渲染
    </h3>
    <div v-if="flag">
        ninengkanjianwoma
    </div>
    <div v-else>
        ssss
    </div>
</template>
<script>
export default{
    data(){
        return{
            flag:true
        }
    }
}
</script>
```

>v-if
>
>v-else
>
>v-if-else
>
>v-show:只能判断自己,频繁切换

```vue
<template>
<h3>条件渲染</h3>
    <div v-if="flag">你能看见我么</div>
    <div v-else>那你还是看看我吧</div>
    <div v-if="type === 'A'">A</div>
    <div v-else-if="type === 'B'">B</div>
    <div v-else-if="type === 'C'">C</div>
    <div v-else>Not A/B/C</div></template>
<script>
export default 
{
    data(){return{
	flag:true.
	"D"type:}
</script>
```

### script setup

在 Vue 3.2 及以上版本中，`<script setup>` 提供了一种更简洁的方式来定义组件的逻辑。所有的响应式状态、计算属性、方法、生命周期钩子等都可以直接写在 `<script setup>` 块中。下面是一些示例，展示如何在 `<script setup>` 中编写各种类型的函数和逻辑

#### 2.使用计算属性

`computed` 的功能正是将 `fullName` 这个计算属性与 `firstName` 和 `lastName` 这两个响应式数据绑定在一起。当 `firstName` 或 `lastName` 的值发生变化时，`fullName` 也会自动更新。

```vue
<template>
  <div>
    <p>Full Name: {{ fullName }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

const firstName = ref('John');
const lastName = ref('Doe');

const fullName = computed(() => `${firstName.value} ${lastName.value}`);
</script>

```

#### 3. 使用生命周期钩子

```vue
<template>
  <div>
    <p>Check the console for lifecycle hook messages.</p>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted } from 'vue';

onMounted(() => {
  console.log('Component mounted');
});

onUnmounted(() => {
  console.log('Component unmounted');
});
</script>

```

#### 4. 使用异步函数

```vue
<template>
  <div>
    <button @click="fetchData">Fetch Data</button>
    <p>Data: {{ data }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const data = ref(null);

const fetchData = async () => {
  const response = await fetch('https://api.example.com/data');
  data.value = await response.json();
};
</script>

```

#### 5. 引用外部组件

```vue
<template>
  <div>
    <MyComponent />
  </div>
</template>

<script setup>
import MyComponent from './MyComponent.vue';
</script>

```

#### 6. 使用模板引用

```vue
<template>
  <div>
    <input ref="inputRef" type="text" />
    <button @click="focusInput">Focus Input</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const inputRef = ref(null);

const focusInput = () => {
  inputRef.value.focus();
};
</script>

```

#### 7. 使用 `watch`

```vue
<template>
  <div>
    <input v-model="message" type="text" />
  </div>
</template>

<script setup>
import { ref, watch } from 'vue';

const message = ref('');

watch(message, (newValue, oldValue) => {
  console.log(`Message changed from ${oldValue} to ${newValue}`);
});
</script>
```

### 父组件和子组件传参

prop $emit

#### 子组件

```vue
<template>
  <div>
    <h2>Child Component</h2>
    <p>{{ message }}</p>
    <button @click="sendMessageToParent">Send Message to Parent</button>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      required: true
    }
  },
  methods: {
    sendMessageToParent() {
      this.$emit('childEvent', 'Hello from Child');
    }
  }
};
</script>

```

#### 父组件

```vue
<template>
  <div>
    <h1>Parent Component</h1>
    <ChildComponent :message="parentMessage" @childEvent="handleChildEvent" />
    <p>Message from Child: {{ messageFromChild }}</p>
  </div>
</template>

<script>
import ChildComponent from './ChildComponent.vue';

export default {
  components: {
    ChildComponent
  },
  data() {
    return {
      parentMessage: 'Hello from Parent',
      messageFromChild: ''
    };
  },
  methods: {
    handleChildEvent(message) {
      this.messageFromChild = message;
    }
  }
};
</script>

```

## VUE小案例-黑马记事本

>目录结构
>
>--xxx.html
>
>--css--index.css
>
>--js--example.js
>
>文件地址："E:\Vue\heima_note"

index.css来渲染页面的组件，xxx.html是基本框架

```html
<html>

<head>
  <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
  <title>小黑记事本</title>
  <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
  <meta name="robots" content="noindex, nofollow" />
  <meta name="googlebot" content="noindex, nofollow" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <link rel="stylesheet" type="text/css" href="./css/index.css" />
</head>

<body>
  <!-- 主体区域 -->
  <section id="todoapp">
    <!-- 输入框 -->
    <header class="header">
      <h1>sss</h1>
      <input v-model="inputValue" @keyup.enter="add" autofocus="autofocus" autocomplete="off" placeholder="请输入任务"
        class="new-todo" />
    </header>
    <!-- 列表区域 -->
    <section class="main">
      <ul class="todo-list">
        <li class="todo" v-for="(item,index) in list">
          <div class="view">
            <span class="index">{{ index+1 }}.</span>
            <label>{{ item }}</label>
            <button class="destroy" @click="remove(index)"></button>
          </div>
        </li>
      </ul>
    </section>
    <!-- 统计和清空 -->
    <footer class="footer" v-show="list.length!=0">
      <span class="todo-count" v-if="list.length!=0">
        <strong>{{ list.length }}</strong> items left
      </span>
      <button v-show="list.length!=0" class="clear-completed" @click="clear">
       Clear
      </button>
    </footer>
  </section>
  <!-- 底部 -->
  <footer class="info">
    <p>
      <a href="http://www.itheima.com/"><img src="./img/black.png" alt="" /></a>
    </p>
  </footer>
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el: "#todoapp",
      data: {
        list: ["写代码", "吃饭饭", "睡觉觉"],
        inputValue: "好好学习,天天向上"
      },
      methods: {
        add: function () {
          this.list.push(this.inputValue);
        },
        remove: function (index) {
          console.log("删除");
          console.log(index+1);
          this.list.splice(index, 1);
        },
        clear: function () {
          this.list = [];
        }
      },
    })
  </script>
</body>

</html>
```

### 解释代码

```html
list.value.splice(index, 1)
```

按index序号0，1，2等等，从数组lsit删去一个值，1表示index开始删去几个元素

```html
<style scoped>
```

就是把css文件，迁移到vue了

```html
<template>
<script>
```

- `<template>` 标签用于定义组件的模板，包含了组件的 HTML 结构和布局。它定义了组件渲染到 DOM 上的具体样式和内容。
  - **HTML 语法**：可以使用标准的 HTML 语法。
  - **数据绑定**：可以通过 Vue 的模板语法（如 `{{ message }}`）进行数据绑定。
  - **指令**：可以使用 Vue 的指令（如 `v-for`, `v-if`, `v-bind`, `v-on`）来实现数据的动态展示和行为控制。
- `<script>` 标签用于定义组件的 JavaScript 逻辑，包括数据、方法、生命周期钩子、计算属性等。
  - **组件选项**：通过 `export default` 导出一个对象，包含组件的各种选项，如 `data`, `methods`, `computed`, `props` 等。
  - **逻辑封装**：可以在脚本中定义数据、方法和其他逻辑，来控制组件的行为。

### 以下代码。展示如何在html中使用vue

- 第一部分表示，在你的 HTML 文件中引入 Vue.js 库

- 第二部分表示，在 `<script>` 标签中，定义一个新的 Vue 实例，并关联到特定的 DOM 元素上。
- el: "#todoapp",的作用是，让id="todoapp"的区域才能使用，data，methods

```html
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script>
    var app = new Vue({
      el: "#todoapp",
      data: {
        list: ["写代码", "吃饭饭", "睡觉觉"],
        inputValue: "好好学习,天天向上"
      },
      methods: {
        add: function () {
          this.list.push(this.inputValue);
        },
        remove: function (index) {
          console.log("删除");
          console.log(index+1);
          this.list.splice(index, 1);
        },
        clear: function () {
          this.list = [];
        }
      },
    })
  </script>
```



### 什么是DOM

DOM（Document Object Model）元素是网页中所有可见和不可见部分的节点表示。它是浏览器将 HTML、XML 文档结构化为对象的模型。每个 DOM 元素代表文档中的一个部分，如一个标签、文本节点、属性等。

#### 关键点

1. **文档结构**：
   - 在网页中，HTML 文件被解析为一个树形结构，称为 DOM 树。
   - 每个 HTML 标签（如 `<div>`, `<p>`, `<a>`）在 DOM 中被表示为一个对象或节点。

2. **节点类型**：
   - **元素节点**：代表一个 HTML 元素。例如，`<div>`, `<p>`, `<a>`。
   - **文本节点**：包含在元素中的文本内容。例如，`<p>Hello, World!</p>` 中的 "Hello, World!"。
   - **属性节点**：包含在元素中的属性，如 `class`, `id`, `href`。

3. **DOM 操作**：
   - 你可以通过 JavaScript 访问和修改 DOM 元素。
   - 例如，改变一个元素的内容、添加或删除元素、修改属性等。

#### 示例

考虑以下 HTML 代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DOM Example</title>
</head>
<body>
  <div id="todoapp">
    <h1>My To-Do List</h1>
    <ul>
      <li class="todo-item">Buy groceries</li>
      <li class="todo-item">Clean the house</li>
      <li class="todo-item">Finish homework</li>
    </ul>
  </div>
</body>
</html>
```

在这个例子中，以下是一些 DOM 元素的说明：

- **元素节点**：
  - `<div id="todoapp">`: 代表一个 `div` 元素，包含 `id` 属性。
  - `<h1>My To-Do List</h1>`: 代表一个 `h1` 元素，包含文本内容 "My To-Do List"。
  - `<ul>`: 代表一个无序列表元素。
  - `<li class="todo-item">Buy groceries</li>`: 代表一个列表项元素，包含类 `todo-item` 和文本内容 "Buy groceries"。

- **文本节点**：
  - 在 `<h1>` 元素内的文本 "My To-Do List" 是一个文本节点。
  - 在 `<li>` 元素内的 "Buy groceries", "Clean the house", 和 "Finish homework" 是文本节点。

#### 操作 DOM

你可以通过 JavaScript 操作这些 DOM 元素，例如：

```javascript
// 获取 DOM 元素
var todoApp = document.getElementById('todoapp');
var todos = document.getElementsByClassName('todo-item');

// 修改文本内容
todoApp.querySelector('h1').textContent = 'Updated To-Do List';
todos[0].textContent = 'Go shopping';

// 添加新元素
var newItem = document.createElement('li');
newItem.className = 'todo-item';
newItem.textContent = 'Read a book';
todoApp.querySelector('ul').appendChild(newItem);
```

在这个例子中：

- **获取元素**：
  - `document.getElementById('todoapp')` 获取 `id` 为 `todoapp` 的元素。
  - `document.getElementsByClassName('todo-item')` 获取所有 `class` 为 `todo-item` 的元素。

- **修改内容**：
  - 修改 `h1` 元素的文本内容。
  - 修改第一个 `li` 元素的文本内容。

- **添加新元素**：
  - 创建一个新的 `li` 元素，设置类名和文本内容，并将其添加到 `ul` 元素中。

#### 总结

DOM 元素是网页的组成部分，表示文档的结构。你可以通过 JavaScript 操作这些元素，动态地修改网页内容和结构。

































