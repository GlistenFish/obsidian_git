# 基础部分

## 内部类

### 成员内部类

我们可以直接在类的内部定义成员内部类

```java
public class Test{
    public class Inner{
        public void test(){
            System.out.println("我是成员内部类");
        }
    }
}
```

成员内部类和成员方法、成员变量一样，是对象所有的，而不是类所有的，如果我们要使用成员内部类，那么久需要

```java
public static void main(String[] args){
    Test test = new Test();
    Test.Inner inner = test.new Inner();	//成员内部类的类型名就是 外层.内部类名称
}
```

同样可以使用成员内部类中的方法：

```java
public static void main(String[] args){
    Test test = new Test();
    Test.Inner inner = test.new Inner();
	inner.test();
}
```

ps:成员内部类可以访问到外部类的对象  外部类不能访问到内部类里的对象



同名变量的确定

```java
public class Test{
    public final String name;
    
    public class Inner{
        String name;
        public void test(String name){
            System.out.println(name);			//test的name
            System.out.println(this.name);		//Inner的name
            System.out.println(Test.this.name);	//外部类的name
            //super也同理
            //Test.super.toString();	//外部类父类的toString方法
        }
    }
}
```



### 静态内部类

静态内部类由于是静态的，所以相对于外部来说，整个内部类中都属于静态上下文（相对于外部来说）

无法访问到外部类的非静态内容，但内部的变量等内容是不受影响，可以使用



### 局部内部类

局部内部类就像局部变量一样，可以在方法中定义。

```java
public class Test{
    private final String name;
    
    public Test(String name){
        this.name = name;
    }
    
    public void hello(){
        class Inner{
            //直接在方法中创建局部内部类
        }
    }
}
```

既然是在方法中声明的累，那作用范围也只能在方法内部



### 匿名内部类

匿名内部类是我们使用频率非常高的一种内部类，它是局部内部类的简化版。

还记得我们在之前学习的抽象类和接口吗？在抽象类和接口中都会含有某些抽象方法需要子类去实现，我们当时已经很明确地说了不能直接通过new的方式去创建一个抽象类或是接口对象，但是我们可以使用匿名内部类。

```java
public abstract class Student {
    public abstract void test();
}
```

正常情况下，要创建一个抽象类的实例对象，只能对其进行继承，先实现未实现的方法，然后创建子类对象。

而我们可以在方法中使用匿名内部类，将其中的抽象方法实现，并直接创建实例对象：

```java
public static void main(String[] args) {
    Student student = new Student() {   //在new的时候，后面加上花括号，把未实现的方法实现了
        @Override
        public void test() {
            System.out.println("我是匿名内部类的实现!");
        }
    };
    student.test();
}
```

此时这里创建出来的Student对象，就是一个已经实现了抽象方法的对象，这个抽象类直接就定义好了，甚至连名字都没有，就可以直接就创出对象。

匿名内部类中同样可以使用类中的属性（因为它本质上就相当于是对应类型的子类）所以

```java
public static void main(String[] args){
    Student student = new Student(){
        int a;		//public stacic final a;
        @Override
        public void test(){
            System.out.println("我是匿名内部类的实现" + a);	//直接使用父类中的name
        }
    };
    student.test();
}
```

同样的，接口也可以通过这种匿名内部类的形式，直接创建一个匿名的接口实现类：

```java
public static void main(String[] args){
    Study study = new Study(){		/study是一个接口
        @Override
        public void study(){
            System.out.println("我是学习方法" + a);
        }
    };
    student.test();
}
```

### Lambda表达式

如果一个接口中有且只有一个待实现的抽象方法，那我们可以将匿名内部类简写为Lambda表达式：

```java
public static void main(String[] args){
	Study study = () -> System.out.println("我是学习方法:");
    study.study();
}
```

规范：

* 标准语法：([参数类型 参数名称，] ... ) -> { 代码语句，包括返回值 }
* 和匿名内部类不同， Lambda仅支持接口，不支持抽象类
* 接口内部必须有且仅有一个抽象方法（可以有多个方法，但是必须保证其他方法有默认实现，必须留一个抽象方法出来）



有参数的形式：

```java
public statci void main(String[] args){
    Study study = (int a) -> {
        Slystem.out.println("我是学习方法");
        return "a = " + a;
    };
    System.out.println(study.study(10));
}

//这是study接口
public interface Study{
    int study(int a);
}
```

ps:

如果只有一个参数，可以省去参数类型，甚至直接省去小括号:

```java
    Study study = a -> {
        Slystem.out.println("我是学习方法");
        return "a = " + a;
    };
```

如果方法体中只有一个返回语句，可以直接省去花括号和return关键字：

`Study study = a -> "a = " + a;`



如果一个方法的参数需要的是一个接口的实现：

```java
public static void main(String[] args){
    test(a -> "今天学会了" + a);	//参数直接写成lambda表达式
}
private static void test(Study study){	//Study是接口
    study.study(10);
}
```



### 方法引用

方法引用就是将一个已实现的方法，直接作为接口中抽象方法的实现（前提方法定义类型得一样）

```java
//接口
public interface Study{
    int sum(int a, int b);
}

//主类使用
public static void main(String[] args){
    //Study study = (a, b) -> a + b;
    //因为Integer类中已经有对应的实现了，所以可以替换为
    //Study study = (a, b) -> Integer.sum(a, b);
    //方法引用的方式：
    Study study = Integer::sum;
    System.out.println(study.sum(10, 20));
}
```

方法引用实质上就相当于将其他方法的实现，直接作为接口中抽象方法的实现
任何方法都可以用过方法引用作为实现



甚至构造方法也可以引用：

```java
//接口
public interface Study{
    String s();
}
//主类使用
public static void main(String[] args){
    Study study = String::new;	//引用String类中的构造方法
}
```



## 异常

### 抛出异常

```java
public static int test(int a, int b){
    if(b == 0){
        throw new ArithmeticException("除数不能为零");	//这是运行时异常，可以直接throw
    }
    return a/b;
}
```

如果是编译异常不处理的话会直接终止程序

可以抛到上一级去处理（但编译异常必须处理，否则异常时终止程序）

```java
public static int test(int a, int b) throws Exception {
    if(b == 0){
        throw new ArithmeticException("除数不能为零");	//这是运行时异常，可以直接throw
    }
    return a/b;
}
```



### 使用`try-catch`进行异常捕获

```java
public static void main(String[] args){
    try{
        Object object = null;
        object.toString();				//这里是空字符异常
    } catch (NullPointerException e){	//异常本身是一个对象//catch()中只能捕获throwable的子类
        e.printStachTrace();
    }
    System.out.println("程序继续正常运行");
}
```





例子：

```java
public static void main(String[] args){
	try{
        int[] arr = new int[10];
        arr[-1] = 10;
    } catch(NullPointerException e){
        e.printStachTrace();
    } catch(ArrayIndexOutOfBoundsException e){
        System.out.println("数组越界异常");
    } catch(RuntimeException e){
        System.out.println("运行时异常");
    }
}
//结果：
//数组越界异常
```

1.注意顺序问题，顺序不对会报错
2.上面的捕获了之后下面的就不会再捕获了

`finally`  是否发生异常都执行

```java
public static void main(String[] args){
	try{
        int[] arr = new int[10];
        arr[-1] = 10;
    } finally{
    	System.out.println("肯定会执行");
    }
}
```

## 常用工具类

### 数学工具类

#### Math

`Math.PI`

`Math.E`

`Math.pow(a, -1)`			// 2的-1次方

`Math.abs(n)`					// 3的绝对值

`Math.max(a, b)`			 // 取大值

`Math.min(a, b)`			 // 取小值

`Math.sqrt(a)`				 // a的绝对值

`Math.log(Math.E)`

`Math.log10(100)`

`Math.ceil(3.14)`			// 4.0	向上取整

`Math.ceil(-3.14)`		 // -3.0 

`Math.floor(3.14)`		  // 向上取整

三角函数：
`Math.sin(Math.PI / 2)`

`Math.cos(Math.PI)`

`Math.tan(Math.PI / 4)`

`Math.asin(a)`

`Math.acos(a)`

`Math.atan(a)`

可能遇到科学计数法
1.4727472574688726E-16
表示
1.4727472574688726 x 10^-16^

#### Random

网上用法多样

要import



### 数组工具类

Arrays.需导入

```java
import java.util.Arrays;
```



#### 数组转化为字符串

`Arrays.toString()`

```java
int[] arr = new int[]{3, 4, 5, 6, 0, 1, 2, 7, 8, 9};
System.out.println(Arrays.toString(arr));
// --> [3, 4, 5, 6, 0, 1, 2, 7, 8, 9]
```

PS:

多维数组转化为字符串

`Arrays.deepToString()`

```java
int[][] arr = new int[][]{{2, 8, 3, 1}, {9, 2, 0, 3}};
System.out.println(Arrays.deepToString(arr));
```



#### 数组元素排序

`Arrays.sort()`

```java
int[] arr = new int[]{3, 4, 5, 6, 0, 1, 2, 7, 8, 9};
Arrays.sort(arr);
//[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

#### 数组填充

`Arrays.fill()`

```java
int[] arr = new int[4];
Arrays.fill(arr, 2);
//[2, 2, 2, 2]
```

#### 数组拷贝

`Arrays.copyOf(arr, length)`

```java
int[] arr = new int[]{1, 2, 3, 4, 5};
int[] target = Arrays.copyOf(arr, 4);
System.out.println(Arrays.toString(target));
// --> [1, 2, 3, 4]
```

`Arrays.copyOfRange(arr, start, end)`

```java
int[] arr = new int[]{1, 2, 3, 4, 5};
int[] target = Arrays.copyOfRange(arr, 1, 3);
// [2, 3]
```

PS：

也可以用System类的拷贝

`System.arraycopy(arr, srcPos, target, destPos, length)`

```java
int[] arr = new int[]{1, 2, 3, 4, 5};
int[] target = new int[10];
Sytem.arraycopy(arr, 2, target, 5, 3);		//arr[2]开始 到target[5]，长度3
System.out.println(Arrays.toString(target));
// --> [0, 0, 0, 0, 0, 3, 4, 5, 0, 0]
```

#### 判断数组是否相等

`Arrays.equals()`

```java
int a = {0, 1, 2, 3};
int b = {0, 1, 2, 3};
System.out.println(Array.equals(a, b));
// --> true
```

多维数组：

`Arrays.deepEquals()`



## 泛型

### 泛型类

泛型就是在变量使用时才确定其变量类型

格式：

```java
public class Score<T, U> {		// T名字可以任取
    T value;
    U cont;
    public Score(T value, U cont){
        this.value = value;
        this.cont = cont;
    }
}
```

使用：

```java
public static void main(String[] args){
    Score<String, Integer> = new Score<>("hello", 3);
    Score<Integer, Integer> = new Score<>(5, 6);
}
```

使用`?`代表任意类型

`Score<?>`



PS: 

1.需要注意，泛型变量因为并不确定具体是什么类型，那么默认会认为这个变量是一个Object类型的变量，因为无论据类型是什么，一定是Object类的子类

![](E:\writedown\photo\java_note\java_note01.png)

2. \# 静态内容无法使用

3.不能为基本数据类型 (如int)  只能使用引用类型 (Integer)



接口和继承都可以使用

### 泛型方法

```java
public static void main(String[] args){
    String s1 = test("hello");
    Integer s2 = test(10);
}

public static <T> T test(T t){
    return t;
}
```



### 泛型界限

限定泛型只能是某些指定的类型

```java
public class Score<T extends Number> {	//extends定义上界，super定义下界
// T只能是Number类或其子类或者间接子类
    T value;
    public Score(T value, U cont){
        this.value = value;
    }
}
```



### 函数式接口

学习了泛型，我们来介绍一下再JDK 1.8中新增的函数式接口。

函数式接口就是JDK1.8专门为我们提供好的用于Lambda表达式的接口，这些接口都可以直接使用Lambda表达式，非常方便，这里我们主要介绍一下四个主要的函数式接口：

**Supplier供给型函数式接口：**这个接口是专门用于供给使用的，其中只有一个get方法用于获取需要的对象。

```java
@FunctionalInterface   //函数式接口都会打上这样一个注解
public interface Supplier<T> {
    T get();   //实现此方法，实现供给功能
}
```

比如我们要实现一个专门供给Student对象Supplier，就可以使用：

```java
public class Student {
    public void hello(){
        System.out.println("我是学生！");
    }
}
```

```java
//专门供给Student对象的Supplier
private static final Supplier<Student> STUDENT_SUPPLIER = Student::new;
public static void main(String[] args) {
    Student student = STUDENT_SUPPLIER.get();
    student.hello();
}
```

**Consumer消费型函数式接口：**这个接口专门用于消费某个对象的。

```java
@FunctionalInterface
public interface Consumer<T> {
    void accept(T t);    //这个方法就是用于消费的，没有返回值

    default Consumer<T> andThen(Consumer<? super T> after) {   //这个方法便于我们连续使用此消费接口
        Objects.requireNonNull(after);
        return (T t) -> { accept(t); after.accept(t); };
    }
}
```

使用起来也是很简单的：

```java
//专门消费Student对象的Consumer
private static final Consumer<Student> STUDENT_CONSUMER = student -> System.out.println(student+" 真好吃！");
public static void main(String[] args) {
    Student student = new Student();
    STUDENT_CONSUMER.accept(student);
}
```

当然，我们也可以使用`andThen`方法继续调用：

```java
public static void main(String[] args) {
    Student student = new Student();
    STUDENT_CONSUMER   //我们可以提前将消费之后的操作以同样的方式预定好
            .andThen(stu -> System.out.println("我是吃完之后的操作！")) 
            .andThen(stu -> System.out.println("好了好了，吃饱了！"))
            .accept(student);   //预定好之后，再执行
}
```

这样，就可以在消费之后进行一些其他的处理了，使用很简洁的代码就可以实现：

![image-20220927181706365](https://s2.loli.net/2022/09/27/Pu1jGzKNSvnV9YZ.png)

**Function函数型函数式接口：**这个接口消费一个对象，然后会向外供给一个对象（前两个的融合体）

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);   //这里一共有两个类型参数，其中一个是接受的参数类型，还有一个是返回的结果类型

    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) {
        Objects.requireNonNull(before);
        return (V v) -> apply(before.apply(v));
    }

    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) {
        Objects.requireNonNull(after);
        return (T t) -> after.apply(apply(t));
    }

    static <T> Function<T, T> identity() {
        return t -> t;
    }
}
```

这个接口方法有点多，我们一个一个来看，首先还是最基本的`apply`方法，这个是我们需要实现的：

```java
//这里实现了一个简单的功能，将传入的int参数转换为字符串的形式
private static final Function<Integer, String> INTEGER_STRING_FUNCTION = Object::toString;
public static void main(String[] args) {
    String str = INTEGER_STRING_FUNCTION.apply(10);
    System.out.println(str);
}
```

我们可以使用`compose`将指定函数式的结果作为当前函数式的实参：

```java
public static void main(String[] args) {
    String str = INTEGER_STRING_FUNCTION
            .compose((String s) -> s.length())   //将此函数式的返回值作为当前实现的实参
            .apply("lbwnb");   //传入上面函数式需要的参数
    System.out.println(str);
}
```

相反的，`andThen`可以将当前实现的返回值进行进一步的处理，得到其他类型的值：

```java
public static void main(String[] args) {
    Boolean str = INTEGER_STRING_FUNCTION
            .andThen(String::isEmpty)   //在执行完后，返回值作为参数执行andThen内的函数式，最后得到的结果就是最终的结果了
            .apply(10);
    System.out.println(str);
}
```

compose相当于前面的操作，andThen相当于后置操作



比较有趣的是，Function中还提供了一个将传入参数原样返回的实现：

```java
public static void main(String[] args) {
    Function<String, String> function = Function.identity();   //原样返回
    System.out.println(function.apply("不会吧不会吧，不会有人听到现在还是懵逼的吧"));
}
```

**Predicate断言型函数式接口：**接收一个参数，然后进行自定义判断并返回一个boolean结果。

```java
@FunctionalInterface
public interface Predicate<T> {
    boolean test(T t);    //这个方法就是我们要实现的

    default Predicate<T> and(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) && other.test(t);
    }

    default Predicate<T> negate() {
        return (t) -> !test(t);
    }

    default Predicate<T> or(Predicate<? super T> other) {
        Objects.requireNonNull(other);
        return (t) -> test(t) || other.test(t);
    }

    static <T> Predicate<T> isEqual(Object targetRef) {
        return (null == targetRef)
                ? Objects::isNull
                : object -> targetRef.equals(object);
    }
}
```

我们可以来编写一个简单的例子：

```java
public class Student {
    public int score;
}
```

```java
private static final Predicate<Student> STUDENT_PREDICATE = student -> student.score >= 60;
public static void main(String[] args) {
    Student student = new Student();
    student.score = 80;
    if(STUDENT_PREDICATE.test(student)) {  //test方法的返回值是一个boolean结果
        System.out.println("及格了，真不错，今晚奖励自己一次");
    } else {
        System.out.println("不是，Java都考不及格？隔壁初中生都在打ACM了");
    }
}
```

我们也可以使用组合条件判断：

```java
public static void main(String[] args) {
    Student student = new Student();
    student.score = 80;
    boolean b = STUDENT_PREDICATE
            .and(stu -> stu.score > 90)   //需要同时满足这里的条件，才能返回true
            .test(student);
    if(!b) System.out.println("Java到现在都没考到90分？你的室友都拿国家奖学金了");
}
```

同样的，这个类型提供了一个对应的实现，用于判断两个对象是否相等：

```java
public static void main(String[] args) {
    Predicate<String> predicate = Predicate.isEqual("Hello World");   //这里传入的对象会和之后的进行比较
    System.out.println(predicate.test("Hello World"));
}
```

通过使用这四个核心的函数式接口，我们就可以使得代码更加简洁。

### 判空包装

Java8还新增了一个非常重要的判空包装类Optional，这个类可以很有效的处理空指针问题。

比如对于下面这样一个很简单的方法：

```java
private static void test(String str){   //传入字符串，如果不是空串，那么就打印长度
    if(!str.isEmpty()) {
        System.out.println("字符串长度为："+str.length());
    }
}
```

但是如果我们在传入参数时，丢个null进去，直接原地爆炸：

```java
public static void main(String[] args) {
    test(null);
}

private static void test(String str){ 
    if(!str.isEmpty()) {   //此时传入的值为null，调用方法马上得到空指针异常
        System.out.println("字符串长度为："+str.length());
    }
}
```

因此我们还需要在使用之前进行判空操作：

```java
private static void test(String str){
    if(str == null) return;   //这样就可以防止null导致的异常了
    if(!str.isEmpty()) {
        System.out.println("字符串长度为："+str.length());
    }
}
```

虽然这种方式很好，但是在Java8之后，有了Optional类，它可以更加优雅地处理这种问题，我们来看看如何使用：

```java
private static void test(String str){
    Optional
            .ofNullable(str)   //将传入的对象包装进Optional中
            .ifPresent(s -> System.out.println("字符串长度为："+s.length()));  
  					//如果不为空，则执行这里的Consumer实现
}
```

并且，包装之后，我们再获取时可以优雅地处理为空的情况：

```java
private static void test(String str){
    String s = Optional.ofNullable(str).get();   //get方法可以获取被包装的对象引用，但是如果为空的话，会抛出异常
    System.out.println(s);
}
```

我们可以对于这种有可能为空的情况进行处理，如果为空，那么就返回另一个备选方案：

```java
private static void test(String str){
    String s = Optional.ofNullable(str).orElse("我是为null的情况备选方案");
    System.out.println(s);
}
```

是不是感觉很方便？我们还可以将包装的类型直接转换为另一种类型：

```java
private static void test(String str){
    Integer i = Optional
            .ofNullable(str)
            .map(String::length)   //使用map来进行映射，将当前类型转换为其他类型，或者是进行处理
            .orElse(-1);
    System.out.println(i);
}
```



## 集合类

### 见作者笔记



# 高级部分

## JAVA I/O

### 文件字节流

```java
package filestream;

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class Main {
	public static void main(String[] args) {
		try (FileInputStream stream = new FileInputStream("C:\\Users\\kkk\\Desktop\\test.txt")){
//  		//文本：HelloWorld
//			int i = stream.read();
//			System.out.println((char) i);
//			//H
//			int a = 0;
//			while((a = stream.read()) != -1) {
//				System.out.print((char) a);
//			}	//elloWorld
			
//			//文本：HelloWorld你好
//			byte[] s = new byte[stream.available()];
//			stream.read(s);
//			System.out.println(new String(s));
//			//HelloWorld你好
			
//			stream.skip(4);
//			System.out.println((char) stream.read());
//			//o

		}catch(IOException e) {
			e.printStackTrace();
		}
		
		try (FileOutputStream stream = new FileOutputStream("C:\\Users\\kkk\\Desktop\\test.txt", true)){
			stream.write("test".getBytes());
			stream.flush();

		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
		
	}
}

```

利用输入流和输出流，就可以轻松实现文件的拷贝了：

```java
public static void main(String[] args) {
    try(FileOutputStream outputStream = new FileOutputStream("output.txt");
        FileInputStream inputStream = new FileInputStream("test.txt")) {   //可以写入多个
        byte[] bytes = new byte[10];    //使用长度为10的byte[]做传输媒介
        int len;   //存储本地读取字节数
        while ((tmp = inputStream.read(bytes)) != -1){   //直到读取完成为止
            outputStream.write(bytes, 0, len);    //写入对应长度的数据到输出流
        }
    }catch (IOException e){
        e.printStackTrace();
    }
}
```

### 文件字符流

字符流不同于字节，字符流是以一个具体的字符进行读取，因此它只适合读纯文本的文件，如果是其他类型的文件不适用



```java
public static void main(String[] args) {
    
		//文本：对xx对
		try (FileReader reader = new FileReader("C:\\Users\\kkk\\Desktop\\test.txt")){
			System.out.println(reader.getEncoding());
			System.out.println(reader.read());	// 对
			System.out.println(reader.read());	// x
            
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	
	}
```

FileWriter 同理



拷贝案例：

```java
public static void main(String[] args) {
        try (FileReader reader = new FileReader("test.txt");
            FileWriter writer = new FileWriter("xxx.txt")){
                char[] chars = new char[3];
                int len;
                while ((len = reader.rea(char)) != -1){
                    writer.write(chars, 0, len);
                } 
		} catch (FileNotFoundException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	
	}
```





这里需要额外介绍一下File类，它是专门用于表示一个文件或文件夹，只不过它只是代表这个文件，但并不是这个文件本身。通过File对象，可以更好地管理和操作硬盘上的文件。

```java
public static void main(String[] args) {
    File file = new File("test.txt");   //直接创建文件对象，可以是相对路径，也可以是绝对路径
    System.out.println(file.exists());   //此文件是否存在
    System.out.println(file.length());   //获取文件的大小
    System.out.println(file.createNewFile());   //创建一个文件，返回布尔类型
    System.out.println（file.mkdir());		//创建文件夹(File file = new File(folder);)
    System.out.println(file.isDirectory());   //是否为一个文件夹
    System.out.println(file.canRead());   //是否可读
    System.out.println(file.canWrite());   //是否可写
    System.out.println(file.canExecute());   //是否可执行
}
```

通过File对象，我们就能快速得到文件的所有信息，如果是文件夹，还可以获取文件夹内部的文件列表等内容：

```java
File file = new File("/");
System.out.println(Arrays.toString(file.list()));   //快速获取文件夹下的文件名称列表
for (File f : file.listFiles()){   //所有子文件的File对象
    System.out.println(f.getAbsolutePath());   //获取文件的绝对路径
}
```

如果我们希望读取某个文件的内容，可以直接将File作为参数传入字节流或是字符流：

```java
File file = new File("test.txt");
try (FileInputStream inputStream = new FileInputStream(file)){   //直接做参数
    System.out.println(inputStream.available());
}catch (IOException e){
    e.printStackTrace();
}
```





# ps

### Lombok

```xml
<dependency>
<groupId>org.projectlombok</groupId>
<artifactId>lombok</artifactId>
<version>1.18.24</version>
<scope>provided</scope>
</dependency>
```

### JUnit

```xml
<dependency>
<groupId>org.junit.jupiter</groupId>
<artifactId>junit-jupiter-api</artifactId>
<version>5.9.1</version>
<scope>test</scope>
</dependency>
```

### mysql (jdbc)

```xml
<dependency>
<groupId>mysql</groupId>
<artifactId>mysql-connector-java</artifactId>
<version>8.0.31</version>
</dependency>
```

### Mybatis

```xml
<dependency>
<groupId>org.mybatis</groupId>
<artifactId>mybatis</artifactId>
<version>3.5.11</version>
</dependency>
```

### Thymeleaf

```xml
<dependency>
    <groupId>org.thymeleaf</groupId>
    <artifactId>thymeleaf</artifactId>
    <version>3.1.1.RELEASE</version>
</dependency>
```

### Spring

#### spring-context

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context</artifactId>
    <version>6.0.3</version>
</dependency>
```

#### spring-aspects

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-aspects</artifactId>
    <version>6.0.3</version>
</dependency>
```

#### spring-webmvc

```xml
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>6.0.3</version>
</dependency>
```





### AspectJ Weaver

```xml
<dependency>
    <groupId>org.aspectj</groupId>
    <artifactId>aspectjweaver</artifactId>
    <version>1.9.19</version>

</dependency>
```

### jakarta.servlet-api

```xml
<dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>5.0.0</version>
    <scope>provided</scope>
</dependency>
```

### javax.servlet-api

```xml
<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>4.0.1</version>
    <scope>provided</scope>
</dependency>
```

### jackson-databind

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.14.1</version>
</dependency>
```





## 获取依赖网址

https://mvnrepository.com/



## mybatis-config.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
  PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
  "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
  <environments default="development">
    <environment id="development">
      <transactionManager type="JDBC"/>
      <dataSource type="POOLED">
        <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/database_name"/>
        <property name="username" value="${用户名}"/>
        <property name="password" value="${密码}"/>
      </dataSource>
    </environment>
  </environments>
</configuration>
```

