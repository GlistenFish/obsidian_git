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
>s

  

