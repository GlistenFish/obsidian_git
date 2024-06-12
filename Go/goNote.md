# Basic Grammer  
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
  
  
  
# Function  
  
## 匿名函数  
  
### 将匿名函数赋值给变量  
```go  
func main() {  
    functionA := func(str1 string) {  
       fmt.Println(str1)  
    }  
  
    functionA("Hello World")  
    functionA("I'm Glisten")  
}
```    

```result  
func main() {  
    functionA := func(str1 string) {  
       fmt.Println(str1)  
    }  
  
    functionA("Hello World")  
    functionA("I'm Glisten")  
}
```  
  
### 案例：“下载神器”  
```go  
func main() {  
    download(func(progress int) {  
       fmt.Printf("Current progress: %d%%\n", progress)  
    })  
}  
  
func download(output func(progress int)) {  
    value := 0  
    for {  
       output(value)  
       value++  
       if value > 100 {  
          break  
       }  
       time.Sleep(1 * time.Second)  
    }  
}
```

## 闭包    
  
在 go 语言中闭包是指函数体内使用管理自由变量的函数，被使用的自由变量和函数一同存在。即使已经离开了自由变量的环境，自由变量也不会被释放或删除，且在闭包中可以继续使用这个变量。因此，可以说闭包为函数带来了 “记忆效应”。
```go  
func main() {  
    accumulator := accumulate(1)  
    fmt.Println(accumulator())  
    fmt.Println(accumulator())  
    fmt.Println(accumulator())  
    accumulator2 := accumulate(10)  
    fmt.Println(accumulator2())  
    fmt.Println(accumulator2())  
    fmt.Println(accumulator2())  
    accumulator3 := accumulate(100)  
    fmt.Println(accumulator3())  
    fmt.Println(accumulator3())  
    fmt.Println(accumulator3())  
    // 再次通过每个变量调用各自的函数  
    fmt.Println(accumulator())  
    fmt.Println(accumulator2())  
    fmt.Println(accumulator3())  
}  
  
func accumulate(value int) func() int {  
    return func() int {  
       value++  
       return value  
    }  
}
```  
  
```result  
2
3
4
11
12
13
101
102
103
5
14
104
```  
  
## 函数的延迟调用  
key: defer  
当有多个 defer 行为时，这些行为将以逆序的方式执行  
```go  
func main() {  
    fmt.Println("defer start")  
    defer fmt.Println("opration01")  
    defer fmt.Println("opration02")  
    defer fmt.Println("opration03")  
    fmt.Println("defer end")  
}
```  
  
```result  
defer start
defer end
opration03
opration02
opration01
```  
  
Features:    
- defer 行为的实际执行顺序与代码定义的顺序是相反的
- 所有的 defer 行为将在整个**函数体**执行结束后执行（即使发生宕机也会执行）  
### 案例  
1. defer 表达式与函数返回  
```go  
func main() {  
    i := 0  
    defer fmt.Println(i)  
    i++  
    fmt.Println(i)  
    return  
}
```  
  
```result  
1  
0
```  
  
2. derfer 表达式与闭包  
```go  
func main() {  
    fmt.Println(funcA())  
}  
  
func funcA() (numA int) {  
    defer func() {  
       numA++  
    }()  
    return 0  
}
```  
  
```result    
1
```  
  
3. 在循环体中的 defer 表达式  
```go  
func main() {  
    numArr := []int{1, 2, 3, 4, 5}  
    for _, value := range numArr {  
       defer fmt.Println(value)  
    }  
    fmt.Println("function start")  
}
```  
  
```result  
function start  
5
4
3
2
1
```

4. 在循环体中的 defer 表达式与闭包  
```go  
func main() {  
    numArr := []int{1, 2, 3, 4, 5}  
    for _, value := range numArr {  
       defer func() {  
          fmt.Println(value)  
       }()  
    }  
    fmt.Println("function start") 
}
```  
  
## 异常  
### 宕机时恢复  
下面演示如何捕获手动触发的异常，并从异常中恢复程序的运行  
```go  
func main() {  
    fmt.Println("Start")  
    defer func() {  
       err := recover()  
       if err == "设备拔出" {  
          fmt.Println("设备拔出，请重新插入")  
       }  
    }()  
    panic("设备拔出")  
}
```  
  
```result  
Start
设备拔出，请重新插入
```  
  
```go  
func main() {  
    fmt.Println("Start")  
    defer func() {  
       err := recover()  
       fmt.Println(err)  
    }()  
    numA := []int{}  
    fmt.Println(numA[5])  
}
```  
  
```result  
Start
runtime error: index out of range [5] with length 0  

Process finished with the exit code 0
```  
  
### 案例：面积计算器    
计算面积，同时，需要使用函数封装具体的计算逻辑，并最终返回结果。当用户输入错误的数据（如负数）时，应当能够避免程序崩毁斌够给出提示（手动触发宕机和恢复）
```go  
func main() {  
    var width float64 = 12  
    var height float64 = 14  
    defer func() {  
       err := recover()  
       if err != nil {  
          fmt.Println(err)  
       }  
    }()  
    if width < 0 || height < 0 {  
       panic("should be positive number")  
    }  
    fmt.Println("area: ", width*height)  
}
```  
  
# Structure  
## 类型  
- 自定义类型：  
```go  
func main() {  
    type NewInt int  
    var intNum NewInt = 10  
    fmt.Println("intNum:", intNum, "Type:", reflect.TypeOf(intNum))  
}
```  
  
```result  

```  
  
- 自定义别名    
>在 go 语言中，除了可以自定义类型，还可以自定义某个自带类型的别名。这种通过“起别名”的方式实现的自定义类型，其本质还是自带类型，这个别名仅存在与代码中，一旦完成编译，别名就不再存在
```go  
func main() {  
    type NewInt = int  
    var intNum NewInt = 10  
    fmt.Println("intNum:", intNum, "Type:", reflect.TypeOf(intNum))  
}
```  
  
```result  
intNum: 10 Type: main.NewInt
```  
  
### 匿名结构体  
```go  
func main() {  
    book01 := struct {  
       title   string  
       author  string  
       subject string  
    }{  
       title:   "Let's Go",  
       author:  "Alex",  
       subject: "Go is xxx",  
    }  
    fmt.Println(book01)  
    fmt.Println(reflect.TypeOf(book01))  
}
```  
  
```result  
{Let's Go Alex Go is xxx}
struct { title string; author string; subject string }
```  
  
## 构造函数与方法    
  
某些其他面向对象的语言具有实体类及其构造函数与方法，但是 Go 语言没有。而借助结构体，开发者可以自己实现构造函数与方法。
### 使用结构体实现构造函数   
```go  
type Cat struct {  
    gender int  
    color  string  
    name   string  
}  
  
func newCat(gender int, color string, name string) *Cat {  
    return &Cat{  
       gender: gender,  
       color:  color,  
       name:   name}  
}  
func main() {  
    cat01 := newCat(0, "blue", "Kaka")  
    fmt.Println(cat01)  
    fmt.Println(reflect.TypeOf(cat01))  
}
```  
  
```result  
&{0 blue Kaka}
*main.Cat

```  
>tip:
>在 newCat()函数中构建函数体实例时，最好返回结构体指针。若返回整个实例，则会执行一次值传递。值传递的性能会随着结构体本身的复杂度发生变化，结构体越复杂，值传递的性能就越差。而直接返回实例的内存地址则跳过了实例的值传递，这对于运行性能的提升是很有帮助的。
  
### 方法与接受者    

在 go 语言中，也有方法（Method）的概念。它作用于结构体中特定字段的函数，这些字段变量称为接收者（Receiver）
```go  
type Cat struct {  
    gender int  
    color  string  
    name   string  
}  
  
func newCat(gender int, color string, name string) *Cat {  
    return &Cat{gender: gender, color: color, name: name}  
}  
  
func (catInstance *Cat) eat(food string) {  
    fmt.Println(catInstance.name, "eating:", food)  
}  
  
func (catInstance *Cat) dream() {  
    fmt.Println(catInstance.name, "dreaming...")  
}  
  
func (catInstance *Cat) mewing() {  
    fmt.Println(catInstance.name, "mewing~mewing~mewing~")  
}  
  
func (catInstance *Cat) reanme(newName string) {  
    catInstance.name = newName  
}  
  
func main() {  
    cat01 := newCat(0, "blue", "CoolCat")  
    fmt.Println(cat01)  
    fmt.Println(reflect.TypeOf(cat01))  
  
    cat01.eat("fish")  
    cat01.dream()  
    cat01.mewing()  
    cat01.reanme("Kaka")  
    fmt.Println(cat01.name)  
}
```  
  
```result  
*main.Cat
CoolCat eating: fish
CoolCat dreaming...
CoolCat mewing~mewing~mewing~
```  
  
tip：  
这里  
```  
func (catInstance *Cat) reanme(newName string) {  
    catInstance.name = newName  
}  
```  
Cat 为什么要用指针的方式呢？如果不用指针的方式，rename()方法中的变量与实例中的变量就不是同一个变量，在方法中改 name 属性就不会更改实例的 name 属性  
  
ps：  
在 Go 语言中，开发者还可以为任意类型添加方法，不限于结构体。如  
```go  
type MyString string  
	func (name MyString)A whoAmI() {  
	fmt.Println("My name is: ", name)  
}  
func main() {  
	var me MyString="Kaka"
	me.whoAmI()
}
```  
  
  
## 结构体嵌套  
  
### 嵌套结构体  
```go  
type Cat struct {  
    name     string  
    bodyInfo BodyInfo  
}  
  
type BodyInfo struct {  
    weight float64  
    color  string  
}  
  
func main() {  
    cat01 := Cat{"Kaka", BodyInfo{60, "red"}}  
    fmt.Println("My name is", cat01.name, ", weight is", cat01.bodyInfo.weight, ", color is", cat01.bodyInfo.color)  
}
```
  
### 嵌套匿名结构体  
```go    
type Cat struct {  
    name     string  
    bodyInfo BodyInfo  
}  
  
type BodyInfo struct {  
    weight float64  
    color  string  
}  
  
func main() {  
    var cat01 Cat  
    cat01.name = "Kaka"  
    cat01.bodyInfo.weight = 10  
    cat01.bodyInfo.color = "green"  
    fmt.Println("My name is", cat01.name, ", weight is", cat01.bodyInfo.weight, ", color is", cat01.bodyInfo.color)  
}
```
  
### 使用结构体实现继承  
Go 语言中没有类的概念，自然也就没有继承的概念。但是开发者通过对结构体的合理嵌套，可以实现继承的效果。  
```go  
type Cat struct {  
    eyeColor string  
    animal   *Animal  
}  
  
func (catInstance Cat) mewing() {  
    fmt.Println(catInstance.animal.name, "miaomiao")  
}  
  
type Dog struct {  
    bodyColor string  
    animal    *Animal  
}  
  
func (dogInstance Dog) bowwow() {  
    fmt.Println(dogInstance.animal.name, "wangwang")  
}  
  
type Animal struct {  
    name string  
}  
  
func main() {  
    dog01 := &Dog{bodyColor: "blue", animal: &Animal{"LittleB"}}  
    fmt.Println(dog01.animal.name, "body color is", dog01.bodyColor)  
    dog01.bowwow()  
    cat01 := &Cat{eyeColor: "red", animal: &Animal{"LittleR"}}  
    fmt.Println(cat01.animal.name, "eyes color are", cat01.eyeColor)  
    cat01.mewing()  
}
```  

  ```result
LittleB body color is blue
LittleB wangwang
LittleR eyes color are red
LittleR miaomiao
  ```

## 案例：Kaka 开银行  
```go  
package main  
  
import "fmt"  
  
var totalBalance float64 = 10000  
  
type Customer struct {  
    Name    string  
    Balance float64  
}  
  
func (customerInstance *Customer) deposit(money float64) {  
    customerInstance.Balance += money  
    totalBalance += money  
    fmt.Println(customerInstance.Name, "deposits", money)  
    fmt.Println(customerInstance.Name, "Customer Balance:", customerInstance.Balance)  
    fmt.Println("Bank savings:", totalBalance)  
}  
  
func (customerInstance *Customer) withdraw(money float64) {  
    fmt.Println(customerInstance.Name, "wants to withdraws", money)  
    if customerInstance.Balance < money {  
       fmt.Println("Insufficient account balance")  
    } else if totalBalance < money {  
       fmt.Println("Insufficient bank savings")  
    } else {  
       customerInstance.Balance -= money  
       totalBalance -= money  
       fmt.Println(customerInstance.Name, "withdraw", money)  
       fmt.Println(customerInstance.Name, "Current account balance is", customerInstance.Balance)  
       fmt.Println("Current bank savings is", totalBalance)  
    }  
}  
  
func main() {  
    var customerA Customer  
    customerA.Name = "DepositorA"  
    customerA.Balance = 2000  
    var customerB Customer  
    customerB.Name = "DepositorB"  
    customerB.Balance = 3000  
    var customerC Customer  
    customerC.Name = "DepositorC"  
    customerC.Balance = 5000  
  
    customerA.deposit(5000)  
    customerC.withdraw(3000)  
    customerB.withdraw(4000)  
    customerA.deposit(6000)  
    customerB.deposit(2000)  
    customerC.deposit(500)  
}
```  
  
```result  
DepositorA deposits 5000
DepositorA Customer Balance: 7000
Bank savings: 15000
DepositorC wants to withdraws 3000
DepositorC withdraw 3000
DepositorC Current account balance is 2000
Current bank savings is 12000
DepositorB wants to withdraws 4000
Insufficient account balance
DepositorA deposits 6000
DepositorA Customer Balance: 13000
Bank savings: 18000
DepositorB deposits 2000
DepositorB Customer Balance: 5000
Bank savings: 20000
DepositorC deposits 500
DepositorC Customer Balance: 2500
Bank savings: 20500
```  
  
# Interface  
  
