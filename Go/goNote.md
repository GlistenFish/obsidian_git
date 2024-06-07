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
  

### 数组

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

  
#### 切片类型
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

```
  

切片截取同 `python`  
  
  
