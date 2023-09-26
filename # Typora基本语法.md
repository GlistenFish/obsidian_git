# Typora基本语法

### 删除线
```markdown
这是~~删除线~~(使用波浪号)
```
这是~~删除线~~


### 斜体
```markdown
这是*斜体*文本
```
这是*斜体*文本


### 加粗
```markdown
这是**加粗**文本
```
这是**加粗**文本


### 斜体+加粗
```markdown
这是***斜体+加粗***
```
这是***斜体+加粗***


### 下划线
```markdown
下划线<u>下划线</u>
```
这是<u>下划线</u>
`HTML语法`


### 高亮
```markdown
这是==高亮==文本
```
这是==高亮==文本


### 下标
```markdown
水H~2~O
```
H~2~O

### 上标

```
10^16^
```

10^16^

### 表情
```markdown
:smile: :laughing: :cry:
```
:smile::laughing::cry:


### 引用
```markdown
>用右尖括号引用
```
>引用
>>引用里嵌套引用
>>emmm


## 列表
### 无序列表--符号 空格
```markdown
* 可以使用`*`作为标记
+ 也可以使用`+`
- 或者`-`
```
* 可以使用`*`
+ 也可以`+`
- 或者`-`

### 有序列表--数字`.`空格
```markdown
1. 有序列表以数字和`.`开始
2. 数字的序列并不会影响生成的列表序列
3. 但仍然按照自然顺序（1.2.3...）编写。
```
1. 有序列表以数字和`.`开始
2. 数字的序列并不会影响生成的列表序列
3. 但仍然按照自然顺序（1.2.3...）编写。

## 代码
### 代码块
```java
This is Java
```
### 行内代码
`啦啦啦`
### 分隔线
在一行中使用三个或多个`*`或`_`来添加分隔线
____
```markdown
***
____
```

## 跳转

### 外部跳转--超链接
格式为 `[link text](link)`
```markdown
[帮助文档](https://www.bilibili.com/)
```
[帮助文档](https://www.bilibili.com/)

### 内部跳转--本文件内跳
格式为`[link text](#要去的标题)`
```markdown
[我想跳转到](#代码)
```
[我想跳转到](#代码)

### 自动链接
使用`<>`包括的URL或邮箱地址会被自动转换为超链接：
```autolink
<https://www.bilibili.com/>
```
<https://www.bilibili.com/>

### 图片
```markdown
![自己起的图片名字](地址：网页地址或者本地地址都可以)
```
![网页地址](https://iphoto.macsc.com/icon/icon/256/20210423/116275/4661099.png)
![本地地址](C:\Users\kkk\Pictures\bp.ICO)   


### 高级

#### 公式
$x^2 + 2x + 5 + \sqrt x = 0$

$\ce{CO2 + C -> 2 CO}$

$\ce{2Mg + O2 ->[燃烧] 2 MgO}$

#### 流程图

```mermaid
graph TB
	%% s=start e=end f=fork n=normal

	s([开始])-->f1{{if条件}};

	%% f1
	f1--true-->n1[if]-->e([end]);
	f1--false-->f2{{else if}};

	%% f2
	f2--true-->n2[else if]-->e;
	f2--false-->n3[else]-->e;
```

```mermaid
graph TB
	n1[分解原问题]-->n2[解决子问题]-->n3[合并问题解];
	
```

```mermaid
graph LR
	n1[分解原问题]-->n2[解决子问题]-->n3[合并问题解];
	
```



#### 饼状图
```mermaid
pie
    title 为什么总是宅在家里？
    "喜欢宅" : 45
    "天气太热" : 70
    "穷" : 500
	"关你屁事" : 95
```
```mermaid
gantt
    title A Gantt Diagram
    dateFormat  YYYY-MM-DD
    section Section
    A task           :a1, 2014-01-01, 30d
    Another task     :after a1  , 20d
    section Another
    Task in sec      :2014-01-12  , 12d
    another task      : 24d
```


这里有&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;6个空格分隔








