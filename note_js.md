# 基础

### 基本

#### 模板字符串和反引号的使用

```js
//模板字符串
let age = 81;
document.write(`我今年${age - 20}岁了`);		//注意这里是反引号而不是单引号，下同
document.write(`
	<div>123</div>
	<p>abc</p>
`);
document.write(`你好我<span>${age}</span>岁`)；//模板字符串里可以加标签
```



#### typeof

`typeof` 返回数据类型

```js
console.log(typeof '123')
// -> string
```

​		*exercise:*

```js
let num = 10;
console.log(typeof num + '11');
console.log(typeof (num + '11'));
console.log(typeof (num + + '11'));
console.log(typeof +'10');		//字符串前加'+' 会将字符串转换为数值型
// -> number11
// -> string
// -> number
// -> number
```



#### 数据类型转换

##### 隐式转换

字符型 + 其他类型		转换为字符串

`-`   `*`   `/`   等运算符会把数字转换成数字型

##### 强制转换

`Number()`
`parseInt()`
`parseFloat()`
`String()`

ps: Number()与parseFloat()的区别

```js
console.log(Number('10.01abc'));
console.log(parseFloat('10.01abc'));
// -> NaN
// -> 10.01
```

ps: `toString()`用法

```js
let num = 10;
console.log(num.toString());
console.log(num.toString(2));
// -> 10	# 字符型
// -> 1010	# 转换成二进制字符串
```

##### 逻辑或短路的应用

```js
function fun(x, y){
    x = x || 0;
    y = y || 0;
    return x + y;
}
fun()
// -> 0
```



##### 运算符优先级

| 优先级 | 运算符类型 | 运算符          |
| ------ | ---------- | --------------- |
| 1      | 小括号     | ()              |
| 2      | 一元运算符 | ++ -- !         |
| 3      | 算数运算符 | 先 * / % 后 + - |
| 4      | 关系运算符 | >  >=  <  <=    |
| 5      | 相等运算符 | ==  !=  \===  !\== |
| 6      | 逻辑运算符 | 先 && 后 \|\| |
| 7      | 赋值运算符 | = |
| 8      | 逗号运算符 | , |



#### 列表操作

`push()`

```js
let sequence = [1, 2, 3];
sequence.push(4);
sequence.push(5);
console.log(sequence);
// → [1, 2, 3, 4, 5]
console.log(sequence.pop());
// → 5
console.log(sequence);
// → [1, 2, 3, 4]
```



`shift()`   `unshift()`

```js
let list1 = [];
function remember(task) {		//push:在末尾添加task
  list1.push(task);
}
function getTask() {			//shift:弹出第一个元素
  return list1.shift();
}
function rememberUrgently(task) {	//unshift:在开头添加task
  todoList.unshift(task);
}
remember("eat");
remember("drink");
remember("push");
remember("pull");
console.log(list1);
console.log(getTask());
console.log(list1);
rememberUrgently("push");
console.log(list1);
```

***

["eat", "drink", "push", "pull"]
eat
["drink", "push", "pull"]
["push", "drink", "push", "pull"]

***



`pop()`	弹出最后一个元素

```js
console.log(list1.pop());
```



`splice(start, deletecount, iteml)`

从索引start开始删除deletecount个元素，插入iteml

```js
let list2 = ['one', 'two', 'three', 'four'];
list2.splice(1, 2, 'aaa', 'bbb');
console.log(lsit2);
// -> Array(4) [ "one", "aaa", "bbb", "four" ]
```



`indexOf()`  `lastIndexOf()`

```js
console.log([1, 2, 3, 2, 1].indexOf(2));
// → 1
console.log([1, 2, 3, 2, 2, 1].lastIndexOf(2));
// → 4
console.log([1, 2, 3, 2, 1].indexOf(9));
// → -1
```

`slice()`

```js
console.log([0, 1, 2, 3, 4].slice(2, 4));
// → [2, 3]
console.log([0, 1, 2, 3, 4].slice(2));
// → [2, 3, 4]
console.log([0, 1, 2, 3, 4].slice());
// → [0, 1, 2, 3, 4]
```

`concat()`

```js
function remove(array, index) {
  return array.slice(0, index).concat(array.slice(index + 1));
}
console.log(remove(["a", "b", "c", "d", "e"], 2));
// → ["a", "b", "d", "e"]
```

If you pass `concat` an argument that is not an array, that value will be added to the new array as if it were a one-element array.



`filter()`

把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定是否丢弃该元素

```js
let arr = [1, 2, 4, 5, 6, 9, 10, 15];
let r = arr.filter(
  function(x){return x % 2 == 0;}
  );
console.log(r);
// → [2, 4, 6, 10]
```



`map()`

将数组中的元素按定义的函数执行

```js
let arr = [1, 4, 9, 16];
let r = arr.map(
  Math.sqrt
  );
console.log(r);
// → [1, 2, 3, 4]
let r = arr.map(
  function(x){return x *= 2;}
  );
console.log(r);
// → [2, 8, 18, 32]
```



***

```js
["A", "B"].forEach(l => console.log(l));
// → A
// → B
```

#### 字符串操作

```js
console.log("coconuts".slice(4, 7));
// → nut
console.log("coconut".indexOf("u"));
// → 5
console.log("one two threeaee".indexOf("ee"));
// → 11
```

```js
console.log("  okay \n ".trim());
// → okay
```

```js
console.log(String(6).padStart(3, "0"));
// → 006
```

```js
let sentence = "Secretarybirds specialize in stomping";
let words = sentence.split(" ");
console.log(words);
// → ["Secretarybirds", "specialize", "in", "stomping"]
console.log(words.join(". "));
// → Secretarybirds. specialize. in. stomping
```

```js
console.log("LA".repeat(3));
// → LALALA
```

```js
let string = "abc";
console.log(string.length);
// → 3
console.log(string[1]);
// → b
```



#### 函数

##### 匿名函数

```js
let fn = function(x, y){
    console.log(x + y);
}
fn(1, 2);
// -> 3
```

##### 立即执行函数

```js
// (function(){})() （function fn(){})()
(function(x, y){
    console.log(x, y);
})(1, 2);

function fn(){
    //arguments 接收所有参数 函数内部有效 伪数组
    let sum = 0;
    for(let i = 0; i < arguments.length; ++i){
        sum += arguments[i];
    }
    console.log(sum);
    //ps: 伪数组 比真数组少了一些pop() push()等方法
}
fn(1, 2, 3);
// -> 6
```

作用：函数里的变量都是局部变量，你的函数中的变量不会和别人的变量发生冲突，防止变量污染，封装

##### 未知个数的函数参数 
使用`...`
会将其转化为数组

```js
function max(...numbers) {
  let result = -Infinity;
  for (let number of numbers) {
    if (number > result) result = number;
  }
  return result;
}
console.log(max(4, 1, 9, -2));
// → 9
```

也可：

```js
let numbers = [5, 1, 7];
console.log(max(...numbers));
// → 7
```



### 对象

#### 基本操作

demo:

```js
let person = {
    name: Jay,
    age: 18,
    sex: male,
    say: function(content){
        console.log(content);
    }
};
console.log(person.name);
console.log(person['sex']);
person.sayHi('Hi~~~');
```

`for (let k in obj){}`遍历对象

```js
let obj = {
    uname: 'ming',
    age: 18,
    sex: 'male'
}
for (let k in obj){
	console.log(k);	//k是属性名
    console.log(obj[k]);	//这样输出属性值
}
```

#### 内置对象

##### Math对象常用方法

`Math.random()`

产生一个0到1的随机数  [0, 1)

```js
console.log(Math.random());
// → 0.36993729369714856
console.log(Math.random()*10);
// → 7.27367032552138

console.log(Math.floor(Math.random() * (M - N + 1) + N));
// 随机生成 N~M 的整数  [N, M]
```

`Math.floor()`

向下取整

```js
console.log(Math.floor(2.3));
console.log(Math.floor(2.7));
// → 2
// → 2
```

`Math.ceil()`

向上取整

```js
console.log(Math.ceil(2.3));
console.log(Math.ceil(2.7));
// → 3
// → 3
```

`Math.round()`

四舍五入

```js
console.log(Math.round(2.4));
console.log(Math.round(2.5));
// → 2
// → 3
```

`Math.abs()`

取绝对值

`Math.min` `Math.max`找最小最大数

`Math.pow()`幂运算

ps: `Math.PI`		(属性)





# webAPI

### DOM对象

CSS选择器

#### 选择标签

`querySelector()`选择第一个

```html
<script>
    let btn = document.querySelector('button');	  //选择第一个button
	console.dir(btn);
</script>
```

`querySelectorAll()`选择所有的该标签，返回一个伪数组

```html
<ul class="nav">
    <li>我的首页</li>
    <li>产品介绍</li>
    <li>联系方式</li>
</ul>
<script>
    let a = document.querySelectorAll('ul li');
    for (let b of a){
        console.log(b);
}
</script>
```



#### 设置/修改DOM

`innerText`属性	(不解析标签)
`innerHTML`属性	(解析标签)

```html
<div>
    pink memory
        </div>
<script>
        let box = document.querySelector('div');
box.innerHTML = '<strong>changed</strong>';
</script>
```

修改css样式：

```html
<div></div>
<script>
    let box = document.querySelector('div');
box.style.backgroundColor = 'hotpink';
box.style.width = '400px';
box.style.marginTop = '100px';
</script>
```

如果修改i的样式比较多，直接通过style属性修改比较繁琐，我们可以通过借助css类名的形式

```html
<head>
    ...
	<style>
    	div {
            ...
        }
        .active {
            width: 300px;
            background-color:hotpink;
        }
	</style>
</head>
<body>
    <script>
        let box = document.querySelector('div');
        box.className = 'active';
	</script>	
</body>
```

为了解决className容易覆盖以前的类名，我们可以同故宫classList方式追加和删除类名

```
//追加一个类
元素.classList.add('类名');
//删除一个类
元素.classList.remove('类');
//切换一个类(如果存在该类名则删除，如果不存在则添加)
元素.classList.toggle('类名');
```

#### 定时器

`setInterval(函数，时间间隔)`		返回值为计时器的序号(第几个计时器)

```js
setInterval(fn, 1000);
```

关闭定时器

`clearInterval()`

```js
let 变量名 = setInterval(*,*);
clearInterval(变量名);
```



#### 事件

##### 事件类型

`element.addEventListener('事件', 函数)`  事件监听

~~~js
let btn = document.querySelector('button');
btn.addEventListener('click', function(){});
~~~

| 事件       | 事件     |
| ---------- | -------- |
| click      | 鼠标点击 |
| mouseenter | 鼠标经过 |
| mouseleave | 鼠标离开 |
| focus      | 获得焦点 |
| blur       | 失去焦点 |
| Keydown    | 键盘按下 |
| Keyup      | 键盘抬起 |
| input      | 用户输入 |

##### 事件对象

是一个存储了事件触发时的相关信息的对象

在事件绑定的回调函数的第一个参数就是事件对象，一般命名为event、ev、e

`元素.addEventListener('click', function(e){...})`

部分常用属性：

​	`tyep`获取当前的事件类型

​	`clientX`/`clientY`获取光标相对于浏览器可见窗口左上角的位置

​	`offsetX`/`offsetY`获取光标相对于当前DOM元素左上角的位置

​	`key`用户按下的键盘键的值

##### 是否使用事件捕获机制

`DOM.addEventListener(事件类型，事件处理机制，是否使用捕获机制)`

传入`true`代表捕获阶段触发（很少使用）

传入`false`代表冒泡阶段触发

若是用L0事件监听，则只有冒泡阶段，没有捕获





#### 节点操作

##### 获取节点

`this`

`parentNode`最近一级的父节点

`childNodes`获取所有的子节点（不常用）

`children`仅获取所有的元素节点	返回一个伪数组

`nextElementSibling`下一个兄弟节点

`previousElementSibiling`上一个兄弟节点

##### 创建节点

`document.createElement()`

`父.appendChild()`

```js
let lii = document.createElement('li');	//创建一个li标签
lii.innerHTML = 'I am li';	//添加内容
ul.appendChild(lii);		//追加节点
```

插入节点

`ul.insetBefore()`

```html
<ul>
    <li>one</li>
    <li>two</li>
</ul>
<script>
	let ull = document.querySelector('ul');
    let lii = document.createElement('li');
    
    lii.innerHTML = 'one point five';
    ul.insertBefore(lii, ull.children[0]);	//插入到one和two之间
</script>
```

##### 克隆节点

`元素.cloneNode(布尔值)`

布尔值：
若为`true`，则代表克隆时会包含后代节点一起克隆
若为`false`，则代表克隆时不包含后代节点
默认为`false`

##### 删除节点

`父元素.removeChild()`

```html
<button>click</button>
<ul>
    <li>I am content</li>
</ul>

<script>
    let btn = document.querySelector('button');
    let ul = document.querySelector('ul');
    btn.addEventListener('click', function(){
        ul.removeChild(ul.children[0]);
    });
</script>
```





### 高阶函数

#### 回调函数

将函数A作为参数传递给函数B，则A为回调函数  

例：

`setInterval(fn, 1000);` fn就是回调函数

`box.addEventListener('click', function(){});`



### 时间对象方法

| 方法          | 作用               | 说明                  |
| ------------- | ------------------ | --------------------- |
| getFullYear() | 获得年份           | 获取四位年份          |
| getMonth()    | 获得月份           | 取值为0~11            |
| getDate()     | 获取月份中的每一天 | 不同月份取值也不同    |
| getDay()      | 获取星期           | 取值为0~6             |
| getHours()    | 获取小时           | 取值为0~23            |
| getMinutes()  | 获取分钟           | 取值为0~59            |
| getSeconds()  | 获取秒             | 取值为0~59            |
| getTime()     | 获取时间戳         | 可以用+new Date()表示 |

```js
let date = new Date();		//先要实例化时间对象
//获取的时间是实例化对象的时间
let year = date.getFullYear();
let month = date.getMonth();
...
```


### 事件流动
#### 捕获和冒泡机制

![](C:\Users\kkk\Pictures\Typora_poto\捕获和冒泡机制.png)

#### 阻止事件流动

`e.stopPropagation()`

##### ps:

`mouseove`r 和 `mouseout` 会有冒泡效果

`mouseenter` 和`mouseleave` 没有冒泡效果(推荐)

#### 阻止默认行为

`e.preventDefault()`

可以阻止默认的行为，比如连接点击不跳转，表单域的跳转



### BOM对象

![](C:\Users\kkk\Pictures\Typora_poto\BOM.png)

window是浏览器内置中的全局对象，我们所学习的所有webAPIs的只是内容都是基于window对象实现的

window对象包含了navigator、location、document、history、screen 5个属性，即所谓的BOM（浏览器对象模型）

document是实现DOM的基础，它其实是依附于window的属性

ps：依附于window对象的所有属性和方法，使用时可以省略window，比如window.fn();window.alert();window.prompt()





















# PS：

```
console.log(5 == '5');
// -> true	# == 只要值一样就是true 不管数据类型
console.log(5 === '5');
// -> false # 强比较  开发常用===
console.log(NaN === NaN)
// -> false
conosole.log(0.1 + 0.2 === 0.3)
// -> false
```

***

