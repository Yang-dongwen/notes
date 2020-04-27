# **Vue快速学习01**

## 起步：下载使用

![image-20200426113602979](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue01.assets\image-20200426113602979.png)

也可以将js文件下载下来通过文件路径的方式指明vue.js路径

```js
<script src="../js/vue.js"></script>
```

## 计数器实现

**基本语法：**

```js
var vue = new Vue({
    el: "#id",
    data: {
        xx: xx,
        ....
    },
    methods: {
        xx : function(){
        
    	},
        ....
    }
})
```



```js
<div id="jishu">
    <h2 >当前计数：{{count}}</h2>
    <!--<button v-on:click="count++">+</button>
    <button v-on:click="count&#45;&#45;">-</button>-->
    <button v-on:click="add">++</button>
    <button v-on:click="sub">--</button>
</div>
</body>
<script type="text/javascript">
    var vue = new Vue({
        el : '#jishu',
        data : {
            count : 0
        },
        methods:{
            add: function () {
                this.count++
            },
            sub : function () {
                this.count--
            }
        }
    })
</script>
```

> 实现方式两种:
>
> 1.将data数据直接放到click事件的引用上进行操作
>
> 2.将定义在function的函数放到click事件的引用上进行操作

## Vue中的MVVM

**全写：Model ViewModel View**

**什么是MVVM：**

> MVVM（Model–view–viewmodel）是一种软件架构模式。
>
> MVVM有助于将图形用户界面的开发与业务逻辑或后端逻辑（数据模型）的开发分离开来，这是通过置标语言或GUI代码实现的。MVVM的视图模型是一个值转换器，[1] 这意味着视图模型负责从模型中暴露（转换）数据对象，以便轻松管理和呈现对象。在这方面，视图模型比视图做得更多，并且处理大部分视图的显示逻辑。[1] 视图模型可以实现中介者模式，组织对视图所支持的用例集的后端逻辑的访问。
>
> MVVM是马丁·福勒的PM（Presentation Model）设计模式的变体。[2][3] MVVM以相同的方式抽象出视图的状态和行为，[3] 但PM以不依赖于特定用户界面平台的方式抽象出视图（创建了视图模型）。
> MVVM和PM都来自MVC模式。

**MVVM模式的组成部分**

>  模型
> 模型是指代表真实状态内容的领域模型（面向对象），或指代表内容的数据访问层（以数据为中心）。
> 		视图
> 就像在MVC和MVP模式中一样，视图是用户在屏幕上看到的结构、布局和外观（UI）。[6]
> 		视图模型
> 视图模型是暴露公共属性和命令的视图的抽象。MVVM没有MVC模式的控制器，也没有MVP模式的presenter，有的是一个绑定器。在视图模型中，绑定器在视图和数据绑定器之间进行通信。[7]
> 		绑定器
> 声明性数据和命令绑定隐含在MVVM模式中。在Microsoft解决方案堆中，绑定器是一种名为XAML的标记语言。[8] 绑定器使开发人员免于被迫编写样板式逻辑来同步视图模型和视图。在微软的堆之外实现时，声明性数据绑定技术的出现是实现该模式的一个关键因素。

![image-20200426115035154](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue01.assets\image-20200426115035154.png)



## Mustache语法

**显示格式：{{message}}**

**基础用法：**

```html
<div id="count">

  <h1>{{lastname + "   " + name}}</h1>
  <h1>{{lastname}} {{name}}</h1>
  <h1>{{count * 10}} {{name}}</h1>
</div>
<script>
  const vue = new Vue({
          el : '#count',
          data : {
            lastname : "kb",
            name : "bt",
            count : 10
          },
          methods:{
          }
  })
</script>
```

## 其它指令使用

### v-once指令

```html
<h2 v-once>{{message}} </h2>
```

<!--使用了该指令，之后修改该属性页面也不会发生改变-->

### v-html指令

```html
<h3 v-html="url"></h3>
```

当url是一段html代码的时候，可以在标签使用v-html=“url”进行解析

例如：

```js
data:{url : "<a href='www.baidu.com'>百度</a>"}
```

### v-text指令

该指令使用较少，指令不够灵活

用来渲染普通文本信息

```html
<h2 v-text="message">不要</h2>
```

会将标签体中的信息覆盖掉

### v-pre指令

将标签体中的信息元丰不懂的打出来，不做任何渲染

```html
<h2 v-pre>{{message}}</h2>
```

### v-cloak指令

在代码没有执行到后面的语句之前，可以通过设置该属性让客户无法看到未解析出来的页面

```js
setTimeout(function () {
  const app = new Vue({
    el : "#app",
    data :{
      message : "威武"
    }
  })
}, 1000)
```

```html
<style>
    [v-cloak]{
      display: none;
    }
  </style>
<div id="app" v-cloak>
  {{message}}
</div>
```

**clock（斗篷），不用的时候把它遮住，用的使用把它放出来**

### v-bind指令(重要)

> 用以动态绑定属性，前面的指令主要是将值插入到**模板的内容**当中，但是出来内容需要动态来决定外，某些属性也希望动态来绑定。

错误的做法，这里不可以使用**mustache**语法

```html
<img src="{{imgURL}}" alt="#"/>
```

正确的做法：使用**v-bind**指令

```html
<img v-bind:src="imgURL" alt="#"/>
<a v-bind:href="ahref">百度</a>
```

语法糖的写法：**去掉前面的v-bind即可**

```html
<img :src="imgURL" alt="#"/>
<a :href="ahref">百度</a>
```

#### 动态绑定class(对象语法)

基本语法：

```html
<h2 :class="{类名1:boolean, 类名2:boolean}">{{message}}</h2>
```

点击按钮动态切换class

![image-20200426162552344](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue01.assets\image-20200426162552344-1587889562735.png)

也可以通过methods获取class

```js
getClass : function () {
  return {active:this.isLine, line: this.isActive}
}
```

#### 动态绑定class(数组语法)

用的比较少，不常用

语法格式

```html
<h2 :class="['active', 'line']">{{message}}</h2>
```

同样也支持

```html
<h2 :class="getClass2()">{{message}}</h2>
```

#### 动态绑定style(对象语法)

伪代码：

```html
<h2 :style="{key(属性名): value(属性值)}">{{message}}</h2>
```

代码示例：

```html
<h2 v-bind:style="{fontSize:'100px', backgroundColor: finalColor}">{{message}}</h2>
<!-- 也可以采用拼接的方式将数字和像素分隔 -->
<script>
  const vue = new Vue({
          el : '#count',
          data : {
            message : "hello",
            finalColor : 'red'
          },
          methods:{
          }
  })
</script>
```

当然，也可以通过**方法**来获取

#### 动态绑定style(数组语法)

略....（用的较少）

### 计算属性

**代码格式：**

```js
computed : {
            FullName : function () {
              return this.firstName + " " + this.lastName
            }
          }
//定义起来和方法一样，却可以当成属性一样来使用
 <h2>{{FullName}}</h2>
// 这里不用带括号
```

> 计算属性，其对应的就是一个属性

复杂操作**

![image-20200426205643987](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue01.assets\image-20200426205643987.png)

<!--要求：计算数组中所有price属性相加的值-->

**代码：**

```html
<div id="count">
  <h2>{{total}}</h2>

</div>
<script>
  const vue = new Vue({
          el : '#count',
          data : {
            games :[
              {id: 1, name: 'LOL', price: 10},
              {id: 2, name: 'CF', price: 21},
              {id: 3, name: 'DNF', price: 13},
              {id: 4, name: 'DATO', price: 14}
            ]
          },
          methods:{
          },
    computed: {
            total: function () {
              let result = 0
              for (let i = 0; i < this.games.length; i++)
              {
                result += this.games[i].price
              }
              return result
            }
        // 第二种语法
        total1: function () {
              let result = 0
              for(let i in this.games){
                result += this.games[i].price
              }
              return result
            },
    }
  })
</script>
```

#### getter，setter方法

> 一般情况下，我们99%是不用去写`set`方法，只是把它当成一个属性来调用

```js
computed: {
    fullName: {
      set:  function (newValue) {
        console.log("==========" + newValue)
        this.lastName = "kebi"
        this.firstName = "brint"
      },
      get: function () {
        return this.lastName + " " + this.firstName
      }
    }
},
```

### 计算属性对比methods

> 一般情况下，我们不要采用直接拼接的方法使用数据拼接，代码会过于繁琐
>
> computed使用性能会更高，因为他的内部会有一个缓存，当调用过一次后，以后再拿出将直接从缓存拿，不用再执行方法
>
> methods每次使用都会重新再执行一次，所以效率相对比较高
>
> 所以我们更多的情况下都会使用计算属性computed