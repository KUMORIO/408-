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

