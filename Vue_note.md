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


 ## 七.Ajax通信

 ### 1. vue-resource基本用法
 - 引入`vue-resource`文件
 - 使用

    1. `this.$http().then(doneCallbacks,failCallbacks)`

    2. `this.$http.get().then(doneCallbacks,failCallbacks)`

    3. `this.$http.post().then(doneCallbacks,failCallbacks)`

    4. `this.$http.jsonp().then(doneCallbacks,failCallbacks)`

 - 发送异步的Ajax请求，`doneCallbacks`为请求成功的回调;`failCallbacks`为请求失败回调。

 - 如果是要传入带参数的,参数部分设置如下
 `this.$http.get('server.php',{params:{json数据}}).then(doneCallbacks,failCallbacks)`

 ### 2. axios基本用法
 - 引入`axios`文件
 - 使用

    1. `axios().then(doneCallbacks).catch(failCallbacks)`

    2. `axios.get().then(doneCallbacks).catch(failCallbacks)`

    3. `axios.post().then(doneCallbacks).catch(failCallbacks)`

 - 发送异步的Ajax请求，`doneCallbacks`为请求成功的回调;`failCallbacks`为请求失败回调。
 - 如果是要传入带参数的,参数部分设置如下
 `axios.get('server.php',{params:{json数据}}).then(doneCallbacks,failCallbacks)`

 - ## **还不完善，不推荐使用**

 ## 八.Vue生命周期

 - vue实例从创建到销毁的过程，就是生命周期
 ![生命周期](https://github.com/Yukijethro/Markdown_note/blob/master/Screenshots/lifecycle.png)


 | vue1.0+ | vue2.0+ | description |
 | :----: | :----: | :----: |
 | init | beforeCreate | 组件实例开始初始化 |
 | created | created |组件实例创建完成，属性已绑定 |
 | beforeCompile | beforeMount | 模板编译/挂载之前 |
 | compile | mounted | 模板编译/挂载之后 |
 |  ready | mounted | 模板编译/挂载之前(不保证组件已经在document中) |
 | - | beforeUpdate | 组件更新之前 |
 | - | updated | 组件更新之后 |
 | - | activated | for`keep-alive`,组件被激活时调用 |
 | - | deactivated | for`keep-alive`,组件被移除时调用 |
 | beforeDestroy | beforeDestroy | 组件销毁前调用 |
 | destroyed | destroyed | 组件销毁后调用 |

 - 每个阶段都提供了相应的钩子函数，用来控制整个生命周期
 - 可以使用`this.$destroy()`来查看销毁状态

 ## 九.计算属性

 ### 1.基本用法
 计算属性也是用来存储属性数据的，但具有以下特点：
     - 计算属性的数据是可以进行逻辑处理操作的
     - 可以对计算属性中的数据进行监视的

 ### 2.计算属性（computed）VS方法（methods）
 将计算属性的get函数定义为一个方法也是可以实现功能

 **区别：**
 - 计算属性是基于它的依赖进行更新的，只有相关依赖发生改变时才会更新变化
 - 计算属性是有缓存的，只要相关依赖没有改变，多次访问计算属性时返回的值始终是相同的

### 3.get和set
计算属性有两部分组成：get和set,分别用来获取计算属性和设置计算属性

**注：**默认计算属性只有get,如果需要对计算属性进行赋值,可自己添加,通过set方法

## 十.vue实例的属性与方法

```html
<div id="app">
    {{msg}}
</div>
```
```javascript
<script>
    var vm = new Vue({
        el:'#app',
        data:{
            msg:'welcome',
            wbs:'12138'
        }
    })
</script>
```

- `vm.属性名`  直接获取属性
    - `console.log(vm.msg)`

    ![vm.属性名](https://github.com/Yukijethro/Markdown_note/blob/master/Screenshots/vm.属性.png)
- `vm.$el`  获取元素
    - `console.log(vm.$el)`

    ![vm.$el](https://github.com/Yukijethro/Markdown_note/blob/master/Screenshots/vm.$el.png)
- `vm.$data`  获取数据对象data
    - `console.log(vm.$data)`

    ![vm.$data](https://github.com/Yukijethro/Markdown_note/blob/master/Screenshots/vm.$data.png)
    - `console.log(vm.$data.wbs)`

    ![vm.$data.wbs](https://github.com/Yukijethro/Markdown_note/blob/master/Screenshots/vm.$data.wbs.png)
- `vm.$options`  获取自定义属性
    - `console.log()`
