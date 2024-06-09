# basic gramma  
### 常量生成器 iota  
使用关键字 `iota` 可以为批量常量进行连续增1赋值，iota 初始值为0
keyword `iota`    
```go  
const(  
	 spring=iota
	 summer
	 autumn
	 winter 
)  
fmt.Println("Four seasons: ", sprint,summer,autumn,winter)
```  
> Four seasons:  0 1 2 3
  
### 用 Printf()的 "%T" 获取变量类型  
```go  
var number int  
number = 3  
fmt.Printf("data type: %T", number)
```  
> data type: int
  
### 单字符数据类型为uint  
```go  
var text string  
text = "哈哈"  
fmt.Printf("data type: %T", text)
```  
> data type: string
```go  
var text string  
text = "哈哈"  
fmt.Printf("data type: %T", text[0])
```  
> data type: uint8
  
### 中文字符长度为3  
```go  
var text string  
text = "哈哈"  
fmt.Println(len(text))
```  
> 6
  
### pointer  
```go  
package main  
  
import "fmt"  
  
func main() {  
    var num1 int = 5  
    var pointer *int = &num1  
    fmt.Println(&num1)  
    fmt.Println(*pointer)  
}
```  
>0xc0000120b8
 5
  

### array

```go
var arr0 = [4]bool{}  
arr0[0] = true  
fmt.Println(arr0)  
  
var arr1 = [...]int{}  
fmt.Println(arr1)  
  
var arr2 = [...]int{1, 2, 3}  
fmt.Println(arr2)  
//arr2[4] = 1   error
```
>[true false false false]
 []
 [1 2 3]
  
#### 使用 new 关键字来声明一个 pointer 类型的数组  
```go  
func main() {  
    var arrPointer = new([20]int)  
    fmt.Println("arrPointer:", arrPointer)  
    fmt.Println("arrPointer的第一个元素值为:", arrPointer[0])  
    fmt.Println("arrPointer的长度为:", len(arrPointer))  
    //通过go语言标准库的reflect包中的TypeOf()函数获取arrPointer的数据类型  
    fmt.Println("arrPointer的数据类型为:", reflect.TypeOf(arrPointer))  
}
```
>arrPointer: \&\[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0\]
 arrPointer 的第一个元素值为: 0
 arrPointer 的长度为: 20
 arrPointer 的数据类型为: \*\[20\]int

  
### slice
切片类型类似 `python` 里的列表类型，切片是对数组的抽象。Go 数组的长度不可改变，在特定场景中这样的集合就不太适用，Go 中提供了一种灵活，功能强悍的内置类型切片("动态数组")，与数组相比切片的长度是不固定的，可以追加元素，在追加时可能使切片的容量增大。  
  
format:  
```  
make([]T, length,capacity)
```
  capacity must larger than length

```go
func main() {  
    var a = make([]int, 3)       // 初始化  
    var b = []string{"aa", "bb"} // 初始化并赋值  
    a = append(a, 6)  
    b = append(b, "/api")  
    b = append(b, "/admin")  
    fmt.Println(a, b)  
  
    var c = make([]int, 3)  
    copy(c, a) // a长度大于c，只拷贝3个  
    fmt.Println(c)  
  
    var d = make([]int, len(a))  
    copy(d, a)  
    fmt.Println(d)  
  
}
```
结果：
```
[0 0 0 6] [aa bb /api /admin]
[0 0 0]
[0 0 0 6]
```

切片加切片：  
```go  
func main() {  
    var slicenInt []int  
    slicenInt = append(slicenInt, 1, 2, 3, 4)  //后插
    fmt.Println(slicenInt)  
    slicenInt = append(slicenInt, []int{5, 6, 7}...) //后插  
    fmt.Println(slicenInt)  
    slicenInt = append([]int{-2, -1, 0}, slicenInt...) //前插  
    fmt.Println(slicenInt)  
}
```
>\[1 2 3 4]
 \[1 2 3 4 5 6 7]
 \[-2 -1 0 1 2 3 4 5 6 7]
  
⚠attention:  
不要忘记末尾三个点  
在切片开头添加元素时，无论添加多少个元素，都应将被添加的元素存放在一个切片中  
  
还可以用以下方法在切片的任意位置插入元素：  
```go  
func main() {  
    var slicenInt []int  
    slicenInt = append(slicenInt, 1, 2, 3, 4)  
    fmt.Println(slicenInt)  
    slicenInt = append(slicenInt[:2], append([]int{666, 777}, slicenInt[2:]...)...)  
    fmt.Println(slicenInt)  
}
```
>\[1 2 3 4]
 \[1 2 666 777 3 4]  

切片截取同 `python`    
  
  
### set(map)  
```go
// 声明map集合变量  
var a map[string]string  
// 创建集合，前面只是声明并没有创建  
a = make(map[string]string)  
// 集合赋值  
a["name"] = "大师"  
a["birthday"] = "10/10"  
a["gender"] = "男"  
  
// 声明变量并且赋值  
var b = map[string]string{  
    "name":     "宗师",  
    "birthday": "10/10",  
    "gender":   "男",  
}  
  
// 删除键值  
delete(a, "gender")  
```
  
### structure
```go  
package main  
  
type people struct {  
    name string  
    age  int  
}  
  
func main() {  
    //定义时直接赋值  
    var a = people{  
       name: "Alice",  
       age:  13,  
    }  
  
    // 先定义后赋值  
    var b = people{}  
    b.name = "John"  
    b.age = 18  
}
```
  
### 案例：九九乘法表  
```go  
func main() {  
    for y := 1; y <= 9; y++ {  
       for x := 1; x <= y; x++ {  
          fmt.Printf("%d*%d=%2.d ", x, y, x*y)  
       }  
       fmt.Println()  
    }  
}
```  
  
```result  
1*1= 1 
1*2= 2 2*2= 4 
1*3= 3 2*3= 6 3*3= 9 
1*4= 4 2*4= 8 3*4=12 4*4=16 
1*5= 5 2*5=10 3*5=15 4*5=20 5*5=25 
1*6= 6 2*6=12 3*6=18 4*6=24 5*6=30 6*6=36 
1*7= 7 2*7=14 3*7=21 4*7=28 5*7=35 6*7=42 7*7=49 
1*8= 8 2*8=16 3*8=24 4*8=32 5*8=40 6*8=48 7*8=56 8*8=64 
1*9= 9 2*9=18 3*9=27 4*9=36 5*9=45 6*9=54 7*9=63 8*9=72 9*9=81
```  
  
### 案例：冒泡排序  
```go  
func main() {  
    arr := [...]int{100, 205, 113, 15, 6, 78, 24, -10, 45, 0}  
    var n = len(arr)  
    for i := 0; i < n-1; i++ {  
       for j := i + 1; j < n; j++ {  
          if arr[i] > arr[j] {  
             arr[i], arr[j] = arr[j], arr[i]  
          }  
       }  
    }  
    fmt.Println(arr)  
}
```  
  
```result  
[-10 0 6 15 24 45 78 100 113 205]
```  
  
