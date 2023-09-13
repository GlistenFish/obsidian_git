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

### 