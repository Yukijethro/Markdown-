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

  `v-on:click="event"`可以简写成`@click="event" //推荐写法`

  #### 1.2 事件对象
  - 包含事件相关信息，如事件源、事件类型等

  #### 1.3 事件冒泡
  - 概念：当一个元素上的事件被触发时，事件会从事件源开始，往上冒泡，知道事件的根元素，这一过程称为事件的冒泡。
  - 阻止冒泡：
    - a) 原生JS方式：依赖事件对象

        `e.stopPropagation()`

        `e.canceBubble = true`

    - b) Vue实现

        `@click.stop ="" `(推荐)

  #### 1.4 默认行为

  - 概念：触发某些事件时会默认执行的行为，如：点击链接是默认会跳转，右击时默认会引出菜单
  - 阻止默认行为
    - a) 原生JS方式：依赖事件对象

        `e.preventDefault()`

    - b) vue方式：不依赖事件对象

        `@click.prevent=""`(推荐)

  #### 1.5 键盘事件
  - `@keydown` `@keypress` `@keyup`

  - `@keydown.enter=""` `@keydown.left=""` `@keydown.up=""` `@keydown.right=""`

  - 默认没有`@keydown.ctrl`事件，可以自定义键盘事件`Vue.directive('on').keyCodes.ctrl=17`

  ### 2. 属性

  #### 2.1 属性绑定和属性缩写
  - `v-bind`主要用于属性绑定，如`v-bind:属性名=""`
  - 属性的简写：
    `v-bind:src=""`简写`:src=""`(推荐)

  #### 2.2 class和style属性
  - `v-bind:class=""`简写`:class=""`
  - `v-bind:style=""`简写`:style=""`

 ## 五.模板
 - 模板就是`{{}}`，用来进行数据绑定
 - 数据绑定的方式
    - 双向数据绑定

        `v-model="msg"`

    - 单向数据绑定

        `{{ msg }}"`

        `v-html="msg"`

 ## 六.过滤器

 ### 1. 基本用法
 - 用来过滤数据模型，在显示之前进行数据处理和筛选
 - 语法：

    `{{ data | filter1 参数1 参数2 | filter2 参数1 参数2 }}`

  ### 2. 自定义过滤器
  - 使用全局方法`Vue.filter()`注册一个自定义过滤器，接受两个参数：过滤器ID和过滤器函数

  #### 2.1 语法

  ```html
      <div id="app">
          <h3>{{ 9 | addZero }}</h3>
          <h3>{{ num | number(3,1) }}</h3>
      </div>
  ```
  ```js
      filters:{
          addZero:function(data){
              return data<10?'0'+data:data;
          },
          number:function(data,n,m){
              return Number(data.toFixed(n))+m
          }
      }
  ```

  #### 2.2 双向过滤器
  - 前面的过滤器都是单向的，由数据model--->视图view，即把来自模型的数据在视图中显示之前进行过滤处理
  - 双向过滤器是两个方向，由视图view<--->数据model，即也可以把来自视图的数据在绑定到模型中之前进行过滤处理
    ```js
    currentNumber:{
        read:function(data){ //model--->view
            return "$"+data.toFixed(2)
        },
        write:function(newValue,oldValue){//view--->model
            return +newValue.replace(/[^\d.]/g,'')
        }
    }
    ```
