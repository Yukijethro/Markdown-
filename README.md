# Vue.js笔记

## 一. Vue.js简介

### Vue.js是什么
Vue.js也称为vue，读音/vju:/，类似 view，错误读音v-u-e
版本 v1.x v2.x

+ 是一个构建用户界面的框架，数据驱动的
+ 通过简单的API实现响应的数据绑定和组合的视图组件
+ 是一个mvvm框架，和angular、react类似
+ 更容易上手、小巧

参考：[Vue.js官网](https://cn.vuejs.org/)

## 二. Vue.js起步

### 1. 下载核心版本库

- 初始化一个配置文件

    `npm init --vue_demo //初始化一个package.json文件`

- 下载vue文件

    `cnpm install vue --save //核心文件在dist文件夹内`

### 2. 第一个Vue.js程序——Hello World

#### 2.1 vue代码实现

- html部分
```html
<div id="app">
    {{msg}}
</div>
```

- js部分
    ```js
    <script>
        new Vue({
            el:"#app",
            data:{
                msg:"Hello World!"
            }
        })
    </script>
    ```

 #### 2.2 调用vue-devtools插件，在chrome中调试vue

 步骤：
 1. 从github上克隆插件

    `git clone https://github.com/vuejs/vue-devtools.git`

 2. 安装插件

    `cd vue-devtools //进入插件所在目录`

    `cnpm install //安装插件`

  3. 运行插件

    `npm run dev //运行插件`

  4. 在chrome浏览器安装对应插件

    - 方法一：在chrome商店搜索vue-devtools下载安装
    - 方法二：在插件根目录->shells->chrome文件夹拖到浏览器安装

  5. 插件使用注意
    - vue-devtools默认情况下只能识别vue工程，对引用的vue.js文件无法起作用，因此，在此类项目中，需加入`Vue.config.devtools = true;`

  ## 三. Vue指令

  ### Vue常用指令

  #### 1. `v-model`
  - 双向数据绑定，一般用于表单元素
  ```html
  <div id="app">
    <p>{{msg}}</p>
    <input type="text" v-model="msg">
  </div>
  <script type="text/javascript">
    new Vue({
      el:"#app",
      data:{
        msg:'Hello Worldw'
      }
    })
  </script>
  ```

  #### 2. `v-for`
  - 对数组或对象进行循环操作
  - 提供多个参数
    `v-for="(value,key,index) in object"`
  #### 3. `v-on`
  - 用户绑定事件
  #### 4. `v-show`
  - 显示隐藏元素
  - 没有`v-hide`指令

  ## 四.事件和属性

  ### 1.事件

  #### 1.1 事件简写

  `v-on:click="event"`可以简写成`@click="event"`

  #### 1.2事件对象
  - 包含事件相关信息，如事件源、事件类型等
  - 
