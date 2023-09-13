# XML
## 语法基础
### XML文档声明
XML声明必须作为XML文档的第一行，前面不能有其他东西

`<?xml version="1.0" encoding="编码" standalone="yes/no"?> `
### 示例
```xml
<?xml version="1.0" encoding="GB2312"?>
<!--这是注释-->
<学生名单>
    <学生>
        <姓名>张三</姓名>
        <学号>21</学号>
        <性别>男</性别>
    </学生>
    <学生>
        <姓名>李四</姓名>
        <学号>22</学号>
        <性别>女</性别>
    </学生>
</学生名单>
```
### 实体引用
`<`---->`&lt;`
`>`---->`&gt;`
`&`---->`&amp;`
`'`---->`&apos;`
`"`---->`&qout;`

### XML命名空间
XML 命名空间提供避免元素命名冲突的方法。
#### 命名冲突
在 XML 中，元素名称是由开发者定义的，当两个不同的文档使用相同的元素名时，就会发生命名冲突。
这个 XML 文档携带着某个表格中的信息：
```xml
<table>
   <tr>
   <td>Apples</td>
   <td>Bananas</td>
   </tr>
</table>
```
这个 XML 文档携带有关桌子的信息（一件家具）：
```xml
<table>
   <name>African Coffee Table</name>
   <width>80</width>
   <length>120</length>
</table>
```
假如这两个 XML 文档被一起使用，由于两个文档都包含带有不同内容和定义的 <table> 元素，就会发生命名冲突。
XML 解析器无法确定如何处理这类冲突。

#### 使用前缀来避免命名冲突
此文档带有某个表格中的信息：
```xml
<h:table>
   <h:tr>
   <h:td>Apples</h:td>
   <h:td>Bananas</h:td>
   </h:tr>
</h:table>
```
此 XML 文档携带着有关一件家具的信息：
```xml
<f:table>
   <f:name>African Coffee Table</f:name>
   <f:width>80</f:width>
   <f:length>120</f:length>
</f:table>
```

#### 使用命名空间
这个 XML 文档携带着某个表格中的信息：
```xml
<h:table xmlns:h="http://www.w3.org/TR/html4/">
   <h:tr>
   <h:td>Apples</h:td>
   <h:td>Bananas</h:td>
   </h:tr>
</h:table>
```
此 XML 文档携带着有关一件家具的信息：
```xml
<f:table xmlns:f="http://www.w3school.com.cn/furniture">
   <f:name>African Coffee Table</f:name>
   <f:width>80</f:width>
   <f:length>120</f:length>
</f:table>
```
与仅仅使用前缀不同，我们为 <table> 标签添加了一个 xmlns 属性，这样就为前缀赋予了一个与某个命名空间相关联的限定名称。 
#### XML Namespace (xmlns) 属性
XML 命名空间属性被放置于元素的开始标签之中，并使用以下的语法：

`xmlns:namespace-prefix="namespaceURI"`

当命名空间被定义在元素的开始标签中时，所有带有相同前缀的子元素都会与同一个命名空间相关联。
**注释**：用于标示命名空间的地址不会被解析器用于查找信息。其惟一的作用是赋予命名空间一个惟一的名称。不过，很多公司常常会作为指针来使用命名空间指向实际存在的网页，这个网页包含关于命名空间的信息。

### XML DTD
XML一定要按照一定的语法形式书写。为了验证合法性，可以通过DTD文档进行验证

示例：
```xml dtd
<?xml version="1.0"?>
<!DOCTYPE note [
  <!ELEMENT note (to,from,heading,body)>
  <!ELEMENT to      (#PCDATA)>
  <!ELEMENT from    (#PCDATA)>
  <!ELEMENT heading (#PCDATA)>
  <!ELEMENT body    (#PCDATA)>
]>
<note>
  <to>George</to>
  <from>John</from>
  <heading>Reminder</heading>
  <body>Don't forget the meeting!</body>
</note>
```

