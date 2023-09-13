# JSON与Python数据类型转换

<img src="C:\Users\kkk\Pictures\Typora_poto\json-python数据转换.png" style="zoom:67%;" />

将字符串转化成json


```python
import json

str1 = [{'user_name': '张三', 'user_age': 18}, (3, 6), 1]
json_str = json.dumps(str1, ensure_ascii=False)
print(json_str, type(json_str))

with open('content.txt', 'w') as f:
    json.dump(str1, f, ensure_ascii=False)
```

常用参数分析：

​	`skipkeys`——默认值为 False。如果 dict 的 keys 内的数据不是 python 的基本类型 (str/unicode/int/long/float/bool/None), 设置为 False ，则会报 TypeError 错误；设置成 True，则会跳过这类key

​	`ensure_ascii`——默认值为 True 。若 dict 内含有非 ASCII 的字符，则会以类似 "\uXXX" 的格式显示数据，设置成 False 可以正常显示。

​	`indent`——非负整数。若为0或为空，则一行显示所有的的 JSON 数据，否则会换行且按照 indent 的数量显示前面的空白，将 JSON 的内容格式化显示。

​	`separators`——分隔符。默认的就是 (',', ':')，这表示 dict 内 keys 之间用 “，” 隔开，而 key 和 value 之间用 “：” 隔开。

​	`sort_keys`——将数据根据 keys 的值进行排序。



json转字符串

```python
import json

str2 = json.loads(json_str)
print(str2, type(str2))
with open('content.txt','r')as f:
    data = json.load(f)
    print(data, type(data))
```

常用参数分主席：

​	`parse_float`——将每一个 JSON 字符串按照 float 解码调，默认情况下相当于 float(num_str)

​	`parse_int`——将每一个 JSON 字符串按照 int 解码调，默认情况下相当于 int(num_str)





JSON 与 Python 对象的具体转化规则如表

|      Python      |  JSON  |
| :--------------: | :----: |
|       dict       | object |
|   list, tuple    | array  |
|   str, unicode   | string |
| int, long, float | number |
|       True       |  true  |
|      False       | false  |
|       None       |  null  |





# MongoDB

MongoDB基本操作：

[菜鸟教程]: https://www.runoob.com/mongodb/mongodb-tutorial.html



Python操作MongoDB示例：

```python
import pymongo

# 创建连接
connection = pymongo.MongoClient()

# 创建/连接 数据库
db = connection.school

# 创建/连接 集合
collection = db.students

# 添加数据
stu = {
    'name': 'zhangsan',
    'age': 19,
    'gender': '男'
}
result = collection.insert_one(stu)
print('添加成功')

# 查询数据
stus = collection.find()
print(stus)
for stu in stus:
    print(stu)

# 修改数据
collection.update_one({'_id': ObjectId('62ef471f15c1e2cf2e6f47e4')}, {'$set': {'name': 'sansan', 'age': 18}})

# 删除数据
collection.delete_one({'age': {'$lt': 19}})

# 关闭连接
connection.close()
```



# Redis

### 数据类型

#### string 类型

​	string 是 Redis 最基本的类型，一个 key 对应一个 value。 string 类型可以包含任何类型，比如 .jpg 或者序列化的对象。

```
127.0.0.1:6379> set name zhangsan
OK
127.0.0.1:6379> get name
"zhangsan"
127.0.0.1:6379> set age 18
OK
127.0.0.1:6379> get age
"18"
```

#### hash 类型

​	Redis 中 hash 类型是一个 string 类型 field 与 value 的映射表，适合用于存储对象。相比于将对象的每个字段存成单个 string 类型，将一个对象存储在 hash 类型中会占用更少的内存，且存取对象时更方便。

```
127.0.0.1:6379> hset person name zhangsan
(integer) 1
127.0.0.1:6379> hset person age 18
(integer) 1
127.0.0.1:6379> hget person name
"zhangsan"
127.0.0.1:6379> hget person age
"18"
127.0.0.1:6379> hset person gender male
(integer) 1
127.0.0.1:6379> hset person addr beijing
(integer) 1
127.0.0.1:6379> hget person addr
"beijing"
127.0.0.1:6379> hmset person1 name lisi age 18 addr beijing gender female
OK
127.0.0.1:6379> hget person1 gender
"female"
127.0.0.1:6379> hmget person1 name age gender
1) "lisi"
2) "18"
3) "female"
```

#### list 类型

​	list 类型是一个双向键表，其每个元素都是 string 类型，可使用 push、pop操作从链表的头部或尾部添加删除元素，其中 key 值可使用链表的名称。

```
127.0.0.1:6379> lpush goods apple pear
(integer) 2
127.0.0.1:6379> lpush goods banana
(integer) 3
127.0.0.1:6379> lrange goods 0 4
1) "banana"
2) "pear"
3) "apple"
127.0.0.1:6379> lrange goods 0 2
1) "banana"
2) "pear"
```

#### set 类型

​	set 类型是 string 类型的无序结合，对集合的操作可添加删除元素，也可对多个集合求交并差，操作中的 key 可以为集合的名称。set 通过  hash 他变了 实现，hash table 会随着对数据的添加或删除自动调整大小。

```
127.0.0.1:6379> sadd classes zhangsan lisi
(integer) 2
127.0.0.1:6379> sadd classes zhangsan lisi
(integer) 0
127.0.0.1:6379> smembers classes
1) "zhangsan"
2) "lisi"
127.0.0.1:6379> sadd classes wangwu zhangsan
(integer) 1
127.0.0.1:6379> smembers classes
1) "zhangsan"
2) "lisi"
3) "wangwu"
127.0.0.1:6379>
```

因为是集合，所以重复添加的数据将会被忽略，无法添加重复数据

`sadd`添加数据	`smember`获取数据值

#### sorted set 类型（zset 类型）	

ps: 有序的集合

​	zset 类型与 set 类型相似，也是 string 类型的集合，且不允许又重复的成员，但区别是 zset 类型是有序的， 它会关联一个 double 类型的 score 属性，该属性在添加和修改元素时可以指定，但每次指定后，zset 会自动重新按新的值调整在顺序。zset 成员是唯一的，但 score 却可以重复。zset 中使用 zadd 命令添加元素到集合中，若元素在集合中已存在则更新对应的 score。

```
127.0.0.1:6379> zadd score 1 100
(integer) 1
127.0.0.1:6379> zadd score 2 110
(integer) 1
127.0.0.1:6379> zadd score 3 99
(integer) 1
127.0.0.1:6379> zadd score 3 101
(integer) 1
127.0.0.1:6379> zrange score 0 5
1) "100"
2) "101"
3) "99"
127.0.0.1:6379> zadd score 4 120
(integer) 1
127.0.0.1:6379> zrange score 0 5
1) "100"
2) "101"
3) "99"
4) "120"
127.0.0.1:6379> zadd score 0 1000
(integer) 1
1) "1000"
2) "100"
3) "101"
4) "99"
5) "120"
127.0.0.1:6379> zadd score 1 1000
(integer) 0
```

0,1,2,3,4 表示权重

