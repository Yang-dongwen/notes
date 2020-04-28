# **Vue快速学习02**

## let/var

![image-20200427083700872](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427083700872.png)



> **所以我们再以后的代码编写中，要尽可能的使用的let和const**
>
> **let作用于块级变量， const为不可修改变量**

### 没有块级作用域可能会引起的问题

> if和for的var变量在外部都能使用，会造成代码极度不安全，外部可随意修改内部变量，但我们的本质是不允许外部修改代码块中的代码。

![image-20200427085534285](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427085534285.png)

## const的使用

![image-20200427091611907](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427091611907.png)

> **注意一： 一旦给const修饰的标识符赋值之后，不能修改**
>
> **注意二： 在使用const定义标识符，必须进行赋值**
>
> **注意三： 常量的含义是指向的对象不能修改，但是可以改变对象内的属性**

## 对象的增强写法

es5写法

```js
const name = 'why';
const age = 19
const height = 190
const obj ={
  name: name,
  age: age,
  height: height
}
```

es6写法：会默认将属性当作key，值当作value

```js
const obj1 ={
  name,
  age,
  height
}
```

## 事件监听

![image-20200427115845309](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427115845309.png)

### v-on的基本使用

#### v-on参数传递

最基本的使用以及语法糖的写法

```html
<div id="count">
  <h2>{{counter}}</h2>
  <button v-on:click="increment">+</button>
  <button v-on:click="decrement">-</button>
    <!-- 语法糖写法 -->
  <button @click="increment">+.</button>
  <button @click="decrement">-.</button>
</div>
<script>
  const vue = new Vue({
          el : '#count',
    data : {
            counter: 0
          },
    methods:{
      increment(){
        return this.counter++
      },

      decrement(){
        return this.counter--
      }
    }
  })
</script>
```

<!--若目标方法没有参数，在v-on:click中的方法名可以不用带小括号，带了也不会错-->

![image-20200427122115740](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427122115740.png)

> **方法定义时，我们需要event对象，又需要使用其它参数时应该用带参方法写，尽量写全参数**
>
> **当只有一个event参数时，我们可以在v-on中不带括号，vue会自动识别并解析该参数**
>
> **多个参数带event对象，可以在方法定义时带上`$event`该符号**

```html
<div id="count">
  <button v-on:click="btnClick">按钮1</button>
  <button v-on:click="btnClick1">按钮2</button>
  <button v-on:click="btnClick2('aa')">按钮3</button>
  <button>按钮4</button>
</div>
<script>
  const vue = new Vue({
          el : '#count',
          data : {

          },
          methods:{
            btnClick(){
              console.log("------" + event)
            },
            btnClick1(event){
              console.log("------" + event)
            },
            btnClick2(a,$event){
              console.log("------" + a + " " + event)
            },
          }
  })
</script>
```

#### v-on修饰符

- .stop修饰符的使用

```html
<div id="count" @click="divClick">
  aaaaaaaa<button @click.stop="btnClick">按钮</button>
</div>
```

- .prevent的使用

可以取消默认的提交方式

```html
<form action="baidu">
  <button type="submit" @click.stop.prevent="subClick">
    提交
  </button>
</form>
```

- 监听键盘的某个键的点击事件

```html
<!--监听某个键盘的键帽-->
<input type="text" @keyup="keyup">
```

## v-if、v-else-if、v-else的使用



简单使用实例

```html
<div id="count">
  <h2 v-if="isShow">
    {{message}}
    <div>1</div>
    <div>2</div>
    <div>3</div>
  </h2>
  <h1 v-else>isShow为false时，显示我</h1>

</div>
<script>
  const vue = new Vue({
          el : '#count',
          data : {
            message : "buyao",
            isShow: true
          },
          methods:{
          }
  })
```

<!--v-else-if不推荐使用，一般逻辑性比较复杂的最好放在compuetd中去实现，代码看起来也会更优雅-->

例如：

```html
<div id="count">
  <h2>{{result}}</h2>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="../js/vue.js"></script>
<script>
  const vue = new Vue({
    el : '#count',
    data : {
      score : 81
    },
    computed:{
      result(){
        let showMessage = ''
        if (this.score > 90){
          showMessage = '优秀'
        }else if (this.score > 80){
          showMessage = '良好'
        }else{
          showMessage = '--'
        }
        return showMessage
      }
    },
    methods:{
    }
  })
</script>
```

像这种也算是比较简单的语法，意思就是难点的结构最好放在计算属性中

## 登录切换的小案例

要求：通过点击button按钮实现用户名和邮箱登录的切换

```html
<div id="count">
  <span v-if="isUser">
    <label>用户账号</label>
    <input type="text" placeholder="用户账号"/>
  </span>
  <span v-else>
    <label>用户邮箱</label>
    <input type="text" placeholder="用户邮箱"/>
  </span>
  <button @click="isUser = !isUser">切换按钮</button>
</div>
<!-- 开发环境版本，包含了有帮助的命令行警告 -->
<script src="../js/vue.js"></script>
<script>
  const vue = new Vue({
    el : '#count',
    data : {
      isUser: true
    },
    methods:{
    }
  })
</script>
```

登录切换的input复用解决办法：

​	可以在<input>标签中添加key属性，只需要保证他们的key不同就可以。

实现效果

![image-20200427163922881](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427163922881.png)

## v-show对比v-if

> v-if：当我们条件为false时，包含v-if指令的元素根本就不会存在我们的dom中
>
> v-show：当条件为false时，v-show只是给我们的元素增加了一个行内样式，如图：

![image-20200427164543268](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427164543268.png)

开发中选择：

- ​	当需要在显示和隐藏之间切片频率非常高的时候，使用v-show
- ​	当只有一次切换时，使用v-if

项目中一般会大量使用v-if

## v-for遍历数组和对象

### 遍历数组

- 获取元素和下标值

```html
<ul>
  <li v-for="(item,index) in names">{{item}}---{{index}}</li>
</ul>

data : {
      message : "你好",
      names: ['why','kebi', 'James', 'zhangsan']
    }
```

### 遍历对象

- 在遍历对象的过程中， 如果只是获取一个值， 那么获取到的时value

```html
<li v-for="item in info">{{item}}</li>

 info: {
        name: 'lisi',
        age : 20,
        tail : 1.90
      }
```

```html
<li v-for="(value,key) in info">{{key}}:{{value}}</li>
```

- 获取key和value格式：(value,key)，第一个参数时值，第二个key

也有index的用法，不过非常少用，这里略。

## v-for绑定和和非绑定key的区别

![image-20200427211459280](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427211459280.png)

![image-20200427212005539](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427212005539.png)

## 数组中哪些方法是响应式的

```html
<ul>
  <li v-for="item in letters">{{item}}</li>
</ul>
<button @click="btnClick()">按钮</button>
```

```js
const vue = new Vue({
  el : '#count',
  data : {
    message : "你好",
    letters : ['a','b','c','d','e']
  },
  methods:{
    btnClick(){
      // 在最后添加元素  响应式
      // this.letters.push('aaa')
      // 非响应式
      // this.letters[0] = 'bbb'
      // 在数组前面删除元素   响应式
      // this.letters.shift()
      // 在数组后面删除元素   响应式
      // this.letters.pop()
      // 在数组前面添加元素 可变参数 可同时添加多个元素   响应式
      this.letters.unshift('avb','ccc', 'ddd')
    }
  }
})
```

splice作用：该函数可以添加、删除、替换元素。例如

```js
this.letters.splice(1,0,'a') // 从第二个位置添加字符a
```

该函数功能比较多，可慢理解

![image-20200427214139714](C:\Users\DW\Desktop\学习笔记\notes\vue速成\vue02.assets\image-20200427214139714.png)

this.letters[0] = 'bbb'这种方式是不能页面刷新的，谨慎使用，可以用splice()函数进行替换

## 作业回顾

作业要求：点击哪个哪个颜色变红色，默认第一个红色。

```js
<div id="count">
  <ul>
    <li v-for="(m, index) in games" :class="{games: currentIndex == index}" @click="getClass(index)">
       {{index}}--{{m}}
    </li>
  </ul>
</div>
<script>
  const vue = new Vue({
          el : '#count',
          data : {
            games : ["绝地求成","影响联盟","qq飞车","穿越火线"],
            currentIndex: 0
          },
          methods:{
            getClass : function (index) {
              this.currentIndex = index
            }
          }
  })
</script>
```

> 注意这里有个变量currentIndex，用来和index作比较，相等为true即可变色，默认是0，第一个红色

## 图书购物车

要点：

- 当购物车清零时，显示购物车为空，即books.length<=0时，使用v-if配合v-else实现
- 减少商品数量时，当商品数量少于1时，减少按钮为不可选状态使用:disabled="item.count <= 1"来实现
- 商品总价格使用**计算属性**来实现，即返回商品数量 * 单价 然后进行相加
- 使用过滤器对商品的价格进行处理，{{item.price | showPrice}}就是把前面的值当参数传给后面的过滤器
- 每个按钮通过@click点击事件进行处理

html代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script src="../js/vue.js"></script>
  <link rel="stylesheet" href="style.css">

</head>
<body>
<div id="app">
  <div v-if="books.length > 0">
  <table>
    <thead>
    <tr>
      <th></th>
      <th>书籍名称</th>
      <th>出版日期</th>
      <th>价格</th>
      <th>购买数量</th>
      <th>操作</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="(item,index) in books">
      <td>{{item.id}}</td>
      <td>{{item.name}}</td>
      <td>{{item.date}}</td>
<!--      <td>{{getFinalPrice(item.price)}}</td>-->
      <td>{{item.price | showPrice}}</td>
      <td>
        <button @click="decrement(index)" :disabled="item.count <= 1">-</button>
        {{item.count}}
        <button @click="increment(index)">+</button>
      </td>
      <td><button @click="removeHandler(index)">移除</button></td>
    </tr>
    </tbody>
  </table>
    <h2>总价格：{{totalPrice}}</h2>
  </div>
  <h2 v-else>购物车为空</h2>

</div>
</body>
<script src="index.js"></script>
</html>
```

css代码

```css
table{
  border: 1px solid #e9e9e9;
  border-collapse: collapse;
  border-spacing: 0;
}
th, td{
  padding: 8px 16px;
  border: 1px solid #e9e9e9;
  text-align: left;
}
th{
  background-color: #f7f7f7;
  color: #5c6b77;
  font-weight: 600;
}
```

js代码

```js
const app = new Vue({
  el: '#app',
  data: {
    books: [
      {
        id: 1,
        name: '算法导论',
        date: '2006-8',
        price: 81.00,
        count: 1
      },
      {
        id: 2,
        name: 'unix编程艺术',
        date: '2023-8',
        price: 82.00,
        count: 1
      },
      {
        id: 3,
        name: '编程思想',
        date: '2012-8',
        price: 83.00,
        count: 1
      },
      {
        id: 4,
        name: 'python爬虫',
        date: '2003-8',
        price: 84.00,
        count: 1
      },
      {
        id: 5,
        name: '学海无涯',
        date: '2006-2',
        price: 85.00,
        count: 1
      }
    ]
  },
  methods: {
    getFinalPrice(price){
      return '￥' + price.toFixed(2);
    },
    decrement: function (index) {
      console.info("--------")
      this.books[index].count--
    },
    increment: function (index) {
      console.info("++++++++++")
      this.books[index].count++
    },
    removeHandler(index){
      this.books.splice(index, 1)
    }
  },
  computed : {
    totalPrice(){
      let totalPrice = 0
      // 这也可以
      /*for (let booksKey in this.books) {
        totalPrice = totalPrice + (this.books[booksKey].price * this.books[booksKey].count)
      }*/
      //for (let i = 0; i < this.books.length; i++) {
      //  totalPrice += (this.books[i].price * this.books[i].count)
     // }
      //这种更好
      for (let i of this.books){
        totalPrice += (i.price * i.count)
      }
      return totalPrice
    }
  },
  //  过滤器技术
  filters :{
    showPrice(price){
      return '￥' + price.toFixed(2);
    }
  }
})
```

