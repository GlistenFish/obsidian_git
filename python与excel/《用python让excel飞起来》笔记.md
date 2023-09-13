# 模块的基操

## os 模块

​	`import os`

#### 获取当前文件路径

`os.getcwd()`

```
path = os.getcwd()
print(path)
```

```
结果：
E:\python3.10
```

#### 列出指定路径下的文件夹包含的文件和子文件夹名称

`os.listdir()`

```
path = 'e:/e-book'
file_list = os.listdir(path)
print(file_list)
```

```
结果：
['CTF安全竞赛入门.pdf', 'Primer c++ Chinese 5.pdf', '《平凡的世界》.pdf', '深入理解计算机系统(第3版).pdf', '超简单：用Python让Excel飞起来.pdf']
```

#### 分离文件主名和扩展名

`os.path.splitext`

```
path = 'demo.xlsx'
separate = os.path.splitext(path)
print(separate)
```

```
结果：
('demo', '.xlsx')
```

#### 重命名文件和文件夹

`rename(src, dst)`

```
oldname = 'e:/demo/demo01.txt'
newname = 'e:/demo/demo.txt'
os.rename(oldname, newname)
```

```
oldname = 'e:/demo'
newname = 'e:/demo01'
os.rename(oldname, newname)
```



## xlwings 模块

`import xlwings as xw`

#### 新建和保存

```
app = xw.App(visible=True, add_book=False)		# 启动excel程序并设为可见，不创建新工作簿
for i in range(1, 21):
    workbook = app.books.add()		# 创建工作簿
    workbook.save(f"C:\\Users\\kkk\\Desktop\\excel_fly_data\\demo{i}.xlsx")	# 保存
    workbook.close()				# 关闭
app.quit()		# 停止程序运行
```

#### 操控工作表和单元格

```
app = xw.App(visible=False)
workbook = app.books.open(r"C:\Users\kkk\Desktop\excel_fly_data\demo.xlsx")
worksheet1 = workbook.sheets['Sheet1']			# 选中工作表Sheet1
worksheet1.range('A1').value = 'test'			# 在单元格A1中输入"test"
worksheet2 = workbook.sheets.add('产品统计表')	 # 添加新工作表
worksheet2.range('A1').value = '编号'			   # 在单元格A1中输入"编号"
workbook.save()									# 保存
workbook.close()
app.quit()
```

## NumPy 模块

`import numpy as np`

#### 数组的创建

```
# 创建一维数组
a = np.array([1, 2, 3, 4,])
# 创建二维数组
b = np.array([[1, 2], [3, 4], [5, 6], [7, 8]])
```

```
a = np.arange(5)
b = np.arange(5, 10)
c = np.arange(5, 10, 2)
d = np.random.randn(3)
print(a)
print(b)
print(c)
print(d)

结果：
[0 1 2 3 4]
[5 6 7 8 9]
[5 7 9]
[-0.59243327 0.53587119 0.15330862]
```

```
e = np.arange(12).reshape(3, 4)
print(e)

结果：
[[ 0 1 2 3]
 [ 4 5 6 7]
 [ 8 9 10 11]]
```

```
# 创建二位随机数组
f = np.random.randint(0, 10, (4, 4))	# (0, 4)四行四列
print(f)

结果：
[[4 1 6 3]
 [3 0 4 8]
 [7 8 1 8]
 [4 6 3 6]]
```

## pandas 模块

数据导入和整理模块

pandas模块是基于NumPy模块的一个开源Python模块，广泛应用于完成数据快速分 析、数据清洗和准备等作，它的名字来源于“panel data”（面板数据）。pandas模块提供 了非常直观的数据结构及强大的数据管理和数据处理功能，某种程度上可以把pandas模块 看成Python版的Excel。

与NumPy模块相比，pandas模块更擅长处理二维数据，其主要有Series和DataFrame两种数据结构。

`import pandas as pd`

#### Series 结构

```Series
s = pd.Series(['丁一', '王二', '张三'])
print(s)

结果：
0    丁一
1    王二
2    张三
dtype: object
```

```Series
print(s[1])

结果：
王二
```

#### DataFrame 结构

##### DataFrame 的创建

1. 通过列表创建DataFrame

	 ```
   a = pd.DataFrame([[1, 2], [3, 4], [5, 6]])
   print(a)
   
   结果：
      0  1
   0  1  2
   1  3  4
   2  5  6
   ```

   ```
   a = pd.DataFrame([[1, 2], [3, 4], [5, 6]], columns=['date', 'score'], index=['A', 'B', 'C'])
   print(a)
   
   结果：
      date  score
   A     1      2
   B     3      4
   C     5      6
   ```

   通过列表创建DataFrame还有另一种方式

   ```
   a = pd.DataFrame()
   data = [1, 3, 5]
   score = [2, 4, 6]
   a['data'] = data
   a['sss'] = score
   print(a)
   
   结果：
      data  sss
   0     1    2
   1     3    4
   2     5    6
   ```

2. 通过字典创建DataFrame

	 ```
   b = pd.DataFrame({'a': [1, 3, 5], 'b': [2, 4, 6]}, index=['x', 'y', 'z'])
   print(b)
   
   结果：
      a  b
   x  1  2
   y  3  4
   z  5  6
   ```

   如果想以字典的键名作为行索引，可以用from_dict()函数将字典转换成DataFrame， 

   同时设置参数orient的值为'index'

   ```
   c = pd.DataFrame.from_dict({'a': [1, 3, 5], 'b': [2, 4, 6]}, orient= 'index')
   print(c)
   
   结果：
      0  1  2
   a  1  3  5
   b  2  4  6
   ```

   (参数orient用于指定以字典的键名作为列索引还是行索引，默认值为'columns'，即以 字典的键名作为列索引，	如果设置成'index'，则表示以字典的键名作为行索引。)

3. 通过二维数组创建DataFrame

	 ```
   import numpy as np
   import pandas as pd
   a = np.arange(12).reshape(3, 4)
   b = pd.DataFrame(a, index=[1, 2, 3], columns=['A', 'B', 'C', 'D'])
   print(b)
   
   结果：
      A  B   C   D
   1  0  1   2   3
   2  4  5   6   7
   3  8  9  10  11
   ```

##### DataFrame 索引的修改

```
a = pd.DataFrame([[1, 2], [3, 4], [5, 6]], columns = ['date', 'score'], index = ['A', 'B', 'C'])
print(a)

   date  score
A     1      2
B     3      4
C     5      6

a.index.name = '公司'
print(a)

    date  score
公司             
A      1      2
B      3      4
C      5      6

# 重命名索引
a = a.rename(index={'A':'万科', 'B':'阿里', 'C':'百度'}, columns= {'date':'日期', 'score':'分数'})
print(a)

    日期  分数
公司        
万科   1   2
阿里   3   4
百度   5   6
```

将索引转换为常规列

```
a = a.reset_index()
print(a)

   公司  日期  分数
0  万科   1   2
1  阿里   3   4
2  百度   5   6
```

如果想把常规列转换为行索引，例如，将“日期”列转换为行索引，可以使用如下代 码：

```
a = a.set_index('日期')
print(a)

    公司  分数
日期        
1   万科   2
3   阿里   4
5   百度   6
```

####  文件的读取和写入

1. 读取xlsx
   ```
   import pandas as pd
   data = pd.read_excel(r"C:\Users\kkk\Desktop\excel_fly_data\demo.xlsx")
   data = pd.read_excel('data.xlsx', sheetname=0, encoding='utf-8')
   ```

   参数：

   `sheetname`用于指定工作表，可以是工作表名称，也可以是数字（默认为0，即第1个 工作表）

   `encoding`用于指定文件的编码方式，一般设置为UTF-8或GBK编码，以避免中文乱码。

​		`index_col`用于设置索引列。

2. 读取csv
   ```
   data = pd.read_csv('data.csv')
   data = pd.read_csv('data.csv', delimiter=',', encoding='utf-8')
   ```

   参数：

   `delimiter`用于指定CSV文件的数据分隔符，默认为逗号。

   `encoding`用于指定文件的编码方式，一般设置为UTF-8或GBK编码，以避免中文乱码。

   `index_col`用于设置索引列。

3. 文件写入
   ```
   # 创建一个DataFrame
   data = pd.DataFrame([[1, 2], [3, 4],[5, 6]], columns=['A列', 'B 列'])
   # 写入excel
   data.to_excel(r"C:\Users\kkk\Desktop\excel_fly_data\demo.xlsx")
   ```

   ![](E:\writedown\photo\python与excel\1.png)

   参数：

   `sheetname`用于指定工作表名称。

   `index`用于指定是否写入行索引信息，默认为True，即将行索引信息存储在输出文件 的第1列；若设置为False，则忽略行索引信息。 

   `columns`用于指定要写入的列。

   `encoding`用于指定编码方式。 
   数据的选取和处理

#### 数据的选取和处理
```
# 首先创建一个3行3列的DataFrame用于演示
data = pd.DataFrame([[1, 2, 3], [4, 5, 6], [7, 8, 9]], index=['r1', 'r2', 'r3'], columns=['c1', 'c2', 'c3'])

    c1  c2  c3
r1   1   2   3
r2   4   5   6
r3   7   8   9
```



##### 数据的选取

按列选取

```
a = data['c1']
print(a)

r1    1
r2    4
r3    7
Name: c1, dtype: int64

b = data[['c1']]
print(b)

    c1
r1   1
r2   4
r3   7

# !!!这里的data[['c1','c3']]不能写成data['c1','c3']
c = data[['c1', 'c3']]
print(c)

    c1  c3
r1   1   3
r2   4   6
r3   7   9
```

按行选取

```
a = data.iloc[1:3]
print(a)
b = data.iloc[-1]
print(b)
c = data.loc[['r2', 'r3']]
print(c)

    c1  c2  c3
r2   4   5   6
r3   7   8   9

c1    7
c2    8
c3    9
Name: r3, dtype: int64

    c1  c2  c3
r2   4   5   6
r3   7   8   9
```

​	如果行数很多，可以用head()函数选取前5行数据

```
e = data.head()
# 或者以以下形式读取两行
e = data.head(2)
```

选取区块数据

用iloc方法  先选取行，再选取列

```
b = data.iloc[0:2][['c1', 'c3']]

    c1  c3
r1   1   3
r2   4   6
```

用iloc选取单个数据

```
a = data.iloc[0]['c3']
print(a)
结果：
3
```

##### 数据的筛选

筛选c1列中数字大于1的行

```
a = data[data['c1'] > 1]
print(a)

    c1  c2  c3
r2   4   5   6
r3   7   8   9
```

如果有多个筛选条件，可以用“&”（表示“且”）或“|”（表示“或”）连接起来。例如， 筛选c1列中数字大于1且c2列中数字等于5的行，代码如下。注意要用小括号将筛选条件括起来。

```
b = data[(data['c1'] > 1) & (data['c2'] == 5)]
print(b)

    c1  c2  c3
r2   4   5   6
```

##### 数据的排序

`sort_values()`  按列排序

将data按c2列进行降序排序

```
a = data.sort_values(by='c2', ascending=False)

    c1  c2  c3
r3   7   8   9
r2   4   5   6
r1   1   2   3
```

参数：

`by` 指定按哪一列排

`ascending` True为上升，False为下降



`sort_index()` 按索引排序

```
a = a.sort_index()
```



##### 数据的运算

通过数据运算可以基于已有的列生成新的一列

```
data['c4'] = data['c3'] - data['c1']

    c1  c2  c3  c4
r1   1   2   3   2
r2   4   5   6   2
r3   7   8   9   2
```

##### 数据的删除

`drop()` 函数

删除data中的c1列数据 

```
a = data.drop(columns='c1')

    c1  c2
r1   1   2
r2   4   5
r3   7   8
```

删除多列数据时，要以列表的形式给出列索引

```
b = data.drop(columns=['c1', 'c3'])
 
     c2
r1   2
r2   5
r3   8
```

删除多行数据时，同样要以列表的形式给出行索引

```
c = data.drop(index=['r1', 'r3'])

    c1  c2  c3
r2   4   5   6
```

参数：

`index`用于指定要删除的行。 

`columns`用于指定要删除的列。 

`inplace`默认值为False，表示该删除操作不改变原DataFrame，而是返回一个执行删除 

操作后的新DataFrame，如果设置为True，则会直接在原DataFrame中进行删除操作。



上述这些演示代码将删除数据后的新DataFrame赋给新的变量，并不会改变原 DataFrame（data）的结构，如果想改变原DataFrame（data）的结构，可以设置参数 inplace为True

```
data.drop(index=['r1', 'r3'], inplace=True)
```



#### 数据表的拼接

pandas模块还提供了一些高级功能，其中的数据合并与重塑功能为两个数据表的拼接提供了极大的便利，主要涉及merge()函数、concat()函数、append()函数。其中merge()函数用得较多。

假设用如下代码创建了两个DataFrame数据表，现在需要将它们合并：

```
import pandas as pd 
df1 = pd.DataFrame({'公司': ['恒盛', '创锐', '快学'], '分数': [90, 95, 85]}) 
df2 = pd.DataFrame({'公司': ['恒盛', '创锐', '京西'], '股价': [20, 180, 30]})
```

![](C:\Users\kkk\Pictures\Typora_poto\2.png)



1. **merge()** 函数

```
df3 = pd.merge(df1, df2)
```

![](C:\Users\kkk\Pictures\Typora_poto\3.png)

可以看到，merge()函数直接根据相同的列名（“公司”列）对两个数据表进行了合 并，而且默认选取的是两个表共有的列内容（'恒盛'、'创锐'）。如果同名的列不止一个， 可以通过设置参数on指定按照哪一列进行合并

```
df3 = pd.merge(df1, df2, on='公司')
```

默认的合并方式其实是取交集（inner连接），即选取两个表共有的内容。如果想取并集（outer连接），即选取两个表所有的内容，可以设置参数`how`

```
df3 = pd.merge(df1, df2, how='outer')
```

![](C:\Users\kkk\Pictures\Typora_poto\4.png)

如果想保留左表（df1）的全部内容，而对右表（df2）不太在意，可以将参数how设置为`left`

```
df3 = pd.merge(df1, df2, how='left')
```

![](C:\Users\kkk\Pictures\Typora_poto\5.png)

保留右表同理



如果想按照行索引进行合并，可以设置参数`left_index`和`right_index`

```
df3 = pd.merge(df1, df2, left_index=True, right_index=True)
```

![](C:\Users\kkk\Pictures\Typora_poto\6.png)



2. **concat()** 函数

concat()函数使用全连接（UNION ALL）方式完成拼接，它不需要对齐，而是直接进行合并，即不需要两个表有相同的列或索引，只是把数据整合到一起。因此，该函数没有参数how和on，而是用参数axis指定连接的轴向。该参数默认值为0，指按行方向连接（纵向拼接）

```
df3 = pd.concat([df1, df2])  # 或者写成df3 = pd.concat([df1, df2], axis=0)
```

![](C:\Users\kkk\Pictures\Typora_poto\7.png)

可以设置参数`ignore_index`为True来忽略原有索引，生成新的数字序列作为索引

```
df3 = pd.concat([df1, df2], ignore_index=True)

   公司    分数     股价
0  恒盛  90.0    NaN
1  创锐  95.0    NaN
2  快学  85.0    NaN
3  恒盛   NaN   20.0
4  创锐   NaN  180.0
5  京西   NaN   30.0
```



```
df3 = pd.concat([df1, df2], axis=1)
```

![](C:\Users\kkk\Pictures\Typora_poto\8-16562580236741.png)



## Matplotlib 模块

#### 折线图：

```
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]
plt.plot(x, y)
plt.show()
```

<img src="C:\Users\kkk\Pictures\Typora_poto\9.png" style="zoom: 50%;" />

#### 柱形图

```
import matplotlib.pyplot as plt

x = [1, 2, 3, 4, 5, 6]
y = [6, 5, 4, 3, 2, 1]
plt.bar(x, y)
plt.show()
```

<img src="C:\Users\kkk\Pictures\Typora_poto\10.png" style="zoom:50%;" />



## 模块的交互

#### xlwings 模块与pandas 模块的交互

```
import xlwings as xw
import pandas as pd

app = xw.App(visible=False)
workbook = app.books.add()
worksheet = workbook.sheets.add('新工作表')
df = pd.DataFrame([[1, 2], [3, 4]], columns=['a', 'b'])
worksheet.range('A1').value = df
workbook.save(r'e:\aatmp\demo01.xlsx')
workbook.close()
app.quit()
```

![](C:\Users\kkk\Pictures\Typora_poto\11.png)



#### xlwings 模块与Matplotlib 模块的交互

```
import xlwings as xw
import matplotlib.pyplot as plt

figure = plt.figure()
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]
plt.plot(x, y)
app = xw.App(visible=False)
workbook = app.books.add()
worksheet = workbook.sheets.add('test')
# 将绘制的图标写入工作簿
worksheet.pictures.add(figure, name='photo1', update=True,left=100, top=150)
workbook.save(r'e:\aatmp\demo02.xlsx')
workbook.close()
app.quit()
```

参数：

`figure` 为固定写法，代表之前用Matplotlib模块绘制的图表。

`name` 用于指定图表的名称，这个名称并不显示在图表上，它是在绘制多个图表时使用的，如果要在同一个工作表里绘制第二个图表，则需要把name设置成另一个名称

`update` 设置为True，则在后续通过pictures.add()函数调用具有相同名称（'photo1'）的图表时，可以只更新图表数据而不更改其位置或大小

`left` 用于设置图表与左侧边界的距离，这里设置left为100，表示让图表距离左侧边界100像素，同理可以设置参数`top`为400，表示让图表距离顶部边界400像素
