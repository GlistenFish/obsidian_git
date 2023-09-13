# PHP操作MYSQL数据库
### 连接数据库
使用`mysqli_connect()`函数连接数据库
```php
@$db = mysqli_connect('localhost','root','mysqlroot','demo1') or die("无法连接到服务器");
print("成功连接到服务器<br/>");
mysqli_close($db);
```
### 执行SQL语句
使用`mysqli_query()`函数执行SQL语句
```php
<?php
@$db = mysqli_connect('localhost','root','mysqlroot','demo1') or die("无法连接到服务器");
print("成功连接到服务器<br/>");
//========================================
$sq="insert into user(ID,Name,Age,Gender,Info)
values(4,'fangfang',18,'female','She is a 18 years lady')";
$result=mysqli_query($db,$sq);
if($result){
    echo "插入数据成功！";
}else{
    echo "插入数据失败！";
}
$sq="update user set Name='张芳' where Name='fangfang'";
$result=mysqli_query($db,$sq);
if($result){
    echo "更新数据成功！";
}else{
    echo "更新数据失败！";
}
$sq="select * from user";
$result=mysqli_query($db,$sq);
//========================================
mysqli_close($db);
?>
```
### 获取查询结果集中的记录数
使用`mysqli_num_rows()`获取查询结果包含的数据记录的条数
使用`mysqli_affected_rows()`获取查询、插入、更新和删除操作所影响的行数
```php
<?php
@$db = mysqli_connect('localhost','root','mysqlroot','demo1') or die("无法连接到服务器");
print("成功连接到服务器<br/>");
//========================================
$sq="select *from user";
$result = mysqli_query($db,$sq);    //如果查询成功，$result为资源类型，保存查询结果集
echo "查询结果有". mysqli_num_rows($result). "条记录<br/>";     //输出查询记录集的行数

$sq="update user set Name='wangfang' where Name='zhangfang'";
$result=mysqli_query($db,$sq);
echo "更新了". mysqli_affected_rows($db). "条记录";             //输出更新记录集的行数
//========================================
mysqli_close($db);
?>
```
### 获取结果集中的记录
#### 获取结果集中的一条记录作为枚举数组
使用`mysqli_fetch_rows()`函数可以从查询结果中取出数据
可以结合循环语句输出
```php
<?php
@$db = mysqli_connect('localhost','root','mysqlroot','demo1') or die("无法连接到服务器");
print("成功连接到服务器<br/>");
$sq="select * from user";
$result = mysqli_query($db,$sq);           //如果查询成功，$result为资源类型，保存查询结果集
?>

<table width="370" border="1" cellspacing="0" cellpadding="0">
        <tr>
            <th>编号</th>
            <th>姓名</th>
            <th>年龄</th>
            <th>性别</th>
            <th>个人信息</th>
        </tr>
<?php
    while($row=mysqli_fetch_row($result)){      //逐行获取结果集中的记录
?>
<tr>
    <td><?php echo $row[0] ?></td>
    <td><?php echo $row[1] ?></td>
    <td><?php echo $row[2] ?></td>
    <td><?php echo $row[3] ?></td>
    <td><?php echo $row[4] ?></td>
</tr>
<?php
    }
    mysqli_close($db);
?>
```
![mysqli_fetch_row()](C:\Users\kkk\Pictures\Typora_poto\1.png)
#### 获取结果集中的记录作为关联数组
使用`mysqli_fetch_assoc()`函数从数组结果集中获取信息
```php
<?php
    while($row=mysqli_fetch_assoc($result)){      //逐行获取结果集中的记录
?>
<tr>
    <td><?php echo $row["ID"] ?></td>
    <td><?php echo $row["Name"] ?></td>
    <td><?php echo $row["Age"] ?></td>
    <td><?php echo $row["Gender"] ?></td>
    <td><?php echo $row["Info"] ?></td>
</tr>
<?php
    }
?>
```
#### 获取结果集中的记录作为对象
使用`mysqli_fetch_object()`函数从结果集中获取一行记录作为对象
```php
<?php
    while($row=mysqli_fetch_object($result)){      //逐行获取结果集中的记录
?>
<tr>
    <td><?php echo $row->ID ?></td>
    <td><?php echo $row->Name ?></td>
    <td><?php echo $row->Age ?></td>
    <td><?php echo $row->Gender ?></td>
    <td><?php echo $row->Info ?></td>
</tr>
<?php
    }
?>
```
#### 使用mysqli_fetch_array()函数获取结果集记录
语法：
`mysqli_fetch_array (result[,resuilt_type])`
参数 resuilt_type 是可选参数，表示一个常量，可以选择
MYSQL_ASSOC（关联数组）
MYSQL_NUM（数字数组）
MYSQL_BOTH（二者兼有）     【默认】
```php
<?php
    while($row=mysqli_fetch_array($result)){      //逐行获取结果集中的记录
?>
<tr>
    <td><?php echo $row["ID"] ?></td>
    <td><?php echo $row["1"] ?></td>
    <td><?php echo $row["Age"] ?></td>
    <td><?php echo $row["3"] ?></td>
    <td><?php echo $row["Info"] ?></td>
</tr>
<?php
    }
?>
```
### 释放资源
`mysqli_free_result(SQL请求所返回的数据库对象)`


