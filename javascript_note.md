## 列表属性

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
let todoList = [];
function remember(task) {		//在末尾添加task
  todoList.push(task);
}
function getTask() {			//gettask
  return todoList.shift();
}
function rememberUrgently(task) {	//在开头添加task
  todoList.unshift(task);
}
remember("eat");
remember("drink");
remember("push");
remember("pull");
console.log(todoList);
console.log(getTask());
console.log(todoList);
rememberUrgently("push");
console.log(todoList);
```

***

["eat", "drink", "push", "pull"]
eat
["drink", "push", "pull"]
["push", "drink", "push", "pull"]

***

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



## 字符串属性

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





***



未知个数的函数参数 
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



## some fuctions

`Math.random()`

产生一个0到1的随机数

```js
console.log(Math.random());
// → 0.36993729369714856
console.log(Math.random()*10);
// → 7.27367032552138
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





