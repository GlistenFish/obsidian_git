## 基础
### 变量
#### 数组类型
示例：
```go
fmt.Println("HelloWorld")  
  
var arr0 = [4]bool{}  
arr0[0] = true  
fmt.Println(arr0)  
  
var arr1 = [...]int{}  
fmt.Println(arr1)  
  
var arr2 = [...]int{1, 2, 3}  
fmt.Println(arr2)  
//arr2[4] = 1   error
```

#### 切片类型
切片类型类似`python`里的列表类型，切片是对数组的抽象。Go 数组的长度不可改变，在特定场景中这样的集合就不太适用，Go 中提供了一种灵活，功能强悍的内置类型切片("动态数组")，与数组相比切片的长度是不固定的，可以追加元素，在追加时可能使切片的容量增大。

```go
package main  
  
import "fmt"  
  
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


切片截取同`python`


#### 结构体
定义：
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

#### Map类型（集合）
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
```

### 常量

常量用`const`关键字声明


#### 常量规则

- 常量名称与变量遵循相同的命名规则
    
- 常量名称_通常_用大写字母书写（便于识别和区分变量）
    
- 常量可以在函数内部和外部声明
    

#### 枚举类型

枚举型是四种基本数据类型之一。常量、字符型、布尔型可以用来表达数，字符，真假的描述。但我们还是觉得有点缺欠：它们不能方便地进行一些标识符的描述，如：红，橙，黄，绿，青，蓝，紫七种颜色，要在数据类型中要把它们直接表达出来，我们觉得有障碍。而在计算机内有没有这种数据类型，能够很方便地将它们表示出来？有，枚举型能办到。用四种基本数据类型不便表示的标识符，而且这些标识符的数量是有限的，我们可以用枚举的方法来表达它，把要用的所有标识符全部枚举出来。这种方法比较接近自然语言的表达。

```go
package main

import "fmt"

const (
    RED    = 1
    ORANGE = 2
    YELLOW = 3
    GREEN  = 4
    BLUE   = 5
    PURPLE = 6
)

func main() {
    fmt.Println(RED)
}

```

#### iota

`iota`特殊常量，可以认为是一个可以被**编译器**修改的常量。

`iota` 在 `const`关键字出现时将被重置为 0，`const` 中每新增一行常量声明将使 `iota` 计数一次。可理解为`const` 语句块中的行索引。

iota 可以被用作枚举值：

```go
package main

import "fmt"

const (
    RED    = 1
    ORANGE = 2
    YELLOW = 3
    GREEN  = iota
    BLUE
    PURPLE
)

func main() {
    fmt.Println(BLUE)
}
```
结果是4
因为 iota 可以认为是行索引，BLUE是4，GREEN是3

## 面向对象

```go
package main

import (
    "crypto/md5"
    "crypto/sha256"
    "crypto/sha512"
    "fmt"
)

// 面向过程

//func MD5(str string) string {
//  return fmt.Sprintf("%x", md5.Sum([]byte(str)))
//}
//
//func SHA256(str string) string {
//  h := sha256.New()
//  h.Write([]byte(str))
//  bs := h.Sum(nil)
//  // 函数作用是江十六进制bs变量转换成字符串
//  return fmt.Sprintf("%x", bs)
//}
//
//func SHA512(str string) string {
//  h := sha512.New()
//  h.Write([]byte(str))
//  bs := h.Sum(nil)
//  return fmt.Sprintf("%x", bs)
//}
//
//func main() {
//  fmt.Println(MD5("123456"))
//  fmt.Println(SHA256("123456"))
//  fmt.Println(SHA512("123456"))
//}

// 面向对象

type Hash struct {
    Str string
}

func (hash Hash) MD5() string {
    return fmt.Sprintf("%x", md5.Sum([]byte(hash.Str)))
}

func (hash Hash) SHA256() string {
    h := sha256.New()
    h.Write([]byte(hash.Str))
    bs := h.Sum(nil)

    return fmt.Sprintf("%x", bs)
}

func (hash Hash) SHA512() string {
    h := sha512.New()
    h.Write([]byte(hash.Str))
    bs := h.Sum(nil)

    return fmt.Sprintf("%x", bs)
}

func main() {
    hash := Hash{Str: "123456"}
    fmt.Println(hash.MD5())
    fmt.Println(hash.SHA256())
    fmt.Println(hash.SHA512())
}
```



Go语言的协程是一种轻量级的线程，不需要操作系统抢占式调度，由Go语言自己的调度器完成协程的调度。协程的作用是实现并发编程，提高程序的性能。

Go语言的协程通过 go 关键字来创建，例如 `go func() `，可以在单独的协程中异步执行函数。通过 `select` 语句可以协程之间进行通信，类似于管道。

协程能够轻松实现高并发，但是也需要注意避免竞态条件等问题。在使用协程时需要对锁、共享变量等进行仔细的设计和管理。

```go
package main

import (
    "fmt"
    "time"
)

func worker(count int) {
    for i := 1; i < count; i++ {
        time.Sleep(500) // 暂停一秒
        fmt.Print(" ", i)
    }
    fmt.Println()
}

func main() {
    // 不使用协程
    now1 := time.Now()
    worker(10)
    worker(10)
    worker(10)
    fmt.Println(time.Now().Sub(now1))

    // 开启三个协程同时执行
    //now2 := time.Now()
    go worker(10)
    go worker(10)
    go worker(10)
    //now3 := time.Now()
    time.Sleep(time.Second * 5)
    //fmt.Println(now3.Sub(now2))
}
```

#### 通道

Go语言通道是一种用于在不同`goroutine` 之间传递数据和同步执行的重要机制。它可以使得多个` goroutine` 之间实现高效、安全的通信，并能够防止竞态条件的发生。

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    channel := make(chan string)

    go func() {
        time.Sleep(3 * time.Second)
        channel <- "Hello from goroutine!"	//放入通道
    }()

    fmt.Println("Waiting for channel...")
    message := <-channel					//从通道中取出
    fmt.Println(message)
}
```

使用通道使得不同的协程之间传递消息变得容易且安全，从而提高了并发程序的效率和可靠性。