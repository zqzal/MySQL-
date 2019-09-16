# MySQL-Crash-Course
**MySQL必知必会读书记录**

**读《MySQL必知必会》遇到的问题一(环境问题以及数据源问题)**
**https://mp.weixin.qq.com/s/GhrZ3aq3bgX51ZT5kBA5Hg**




**一起学习**



![扫一扫](https://mp.weixin.qq.com/mp/qrcode?scene=10000004&size=102&__biz=MzI5NjY2Nzk1MQ==&mid=2247483654&idx=1&sn=59305dd60579cf8e10a6c11c3293a559&send_time= "你一关注我就更来劲了!")



**MySQL下载地址**
**https://www.mysql.com/downloads/**

**样例表下载地址**
**https://forta.com/books/0672327120/**

# 第4章 检索数据
## 4.1 selcet语句
## 4.2 检索单个列
`select prod_name from products;`
## 4.3 检索多个列
`select prod_id,prod_name,prod_price from products;`
## 4.4 检索所有的列
`select * from products;`
## 4.5 检索不同的行
`select vend_id from products;`

`select distinct vend_id from products; (检索出不同值的列表)`

## 4.6 限制结果
`select prod_name from products limit 5;`

`select prod_name from products limit 5,5;`

# 第5章 排序检索数据
## 5.1 排序数据
`select prod_name from products;`

`select prod_name from products order by prod_name;`
## 5.2 按多个列排序
`select prod_id,prod_price,prod_name from products order by prod_price,prod_name;`
## 5.3 指定排序方向
`select prod_id,prod_price,prod_name from products order by prod_price desc;`

`select prod_id,prod_price,prod_name from products order by prod_price desc, prod_name;`

`select prod_price from products order by prod_price desc limit 1;`

* order by字句的位置：在给出order by子句时，应该保证它位于from子句之后。如果使用limit，它必须位于order by
之后。使用子句的次序不对将产生错误信息。

# 第6章 过滤数据
## 6.1使用where子句

`select prod_name,prod_price from products where prod_price = 2.50;`

## 6.2 where子句操作符

`= 等于; <> 不等于; != 不等于; < 小于; <=小于等于; > 大于; >= 大于等于 ; between 在指定的两个值之间`

### 6.2.1 检查单个值
`select prod_name,prod_price from products where prod_name = 'fuses';`

`select prod_name,prod_price from products where prod_price < 10;`

`select prod_name,prod_price from products where prod_price <= 10;`

### 6.2.2 不匹配检查
`select vend_id,prod_name from products where vend_id <> 1003;`

`select vend_id,prod_name from products where vend_id != 1003;`

### 6.2.3 范围值检查
`select prod_name,prod_price from products where prod_price between 5 and 10;`

### 6.2.4 空值检查
`select prod_name from products where prod_price is null;`

`select cust_id from customers where cust_email is null;`

# 第7章 数据过滤
## 7.1 组合where子句
* 第6章中 介绍的所有where子句在过滤数据时使用的都是单一的条件。为了进行更强的过滤控制，Mysql允许给出多个where子句。
* 这些子句可以两种方式使用：以and子句的方式或or子句的方式使用。
### 7.1.1 and操作符
`select prod_id,prod_price,prod_name from products where vend_id = 1003 and prod_price <= 10;`
### 7.1.2 or操作符
`select prod_name,prod_price from products where vend_id = 1002 or vend_id =1003;`
### 7.1.3 计算次序
`select prod_name,prod_price from products where (vend_id = 1002 or vend_id =1003) and prod_price >= 10;`

## 7.2 in操作符
`select prod_name,prod_price from products where vend_id in (1002,1003) order by prod_name;`

`select prod_name,prod_price from products where vend_id = 1002 or vend_id = 1003 order by prod_name;`
* in where子句中用来指定要匹配值的清单的关键字，功能与or相当

## 7.3 not操作符
`select prod_name,prod_price from products where vend_id not in (1002,1003) order by prod_name;`
* mysql中的not  mysql支持使用not对in、between和exists子句中取反，这与多数其他DBMS允许使用NOT对各种各样取反右很大的差别

# 第8章 用通配符进行过滤

## 8.1 like操作符
### 8.1.1 百分号（%）通配符
`select prod_id,prod_name from products where prod_name like 'jet%';`

`select prod_id,prod_name from products where prod_name like '%anvil%';`

`select prod_name from products where prod_name like 's%e';`

### 8.1.2 下划线（_）通配符

`select prod_id,prod_name from products where prod_name like '_ ton anvil';`

`select prod_id,prod_name from products where prod_name like '% ton anvil';`

# 第9章 用正则表达式进行搜索
## 9.1 正则表达式介绍

## 9.2 使用MySQL正则表达式
### 9.2.1 基本字符匹配
`select prod_name from products where prod_name regexp '1000' order by prod_name;`

`select prod_name from products where prod_name regexp '.000' order by prod_name;`
### 9.2.2 进行OR匹配
`select prod_name from products where prod_name regexp '1000|2000' order by prod_name;`
### 9.2.3 匹配几个字符之一
`select prod_name from products where prod_name regexp '[123] Ton' order by prod_name;`
`select prod_name from products where prod_name regexp '[1|2|3] Ton' order by prod_name;`
### 9.2.4 匹配范围
`select prod_name from products where prod_name regexp '[1-5] Ton' order by prod_name;`
### 9.2.5 匹配特殊字符
`select vend_name from vendors where vend_name regexp '\\.' order by vend_name;`

### 9.2.6 匹配字符类

* [:alnum:] 任意字母和数字（同[a-z A-Z 0-9]）
* [:alpha:] 任意字符(同[a-z A-Z])
* [:blank:] 空格和制表(同[\\t])
* [:cntrl:] ASCII控制字符(ASCII 0到31和127)
* [:digit:] 任意数字(同[0-9])
* [:graph:] 与[:print:]相同，但不包括空格
* [:lower:] 任意小写字母 (同[a-z])
* [:print:] 任意可打印字符
* [:punct:] 既不在[:alunm:]又不在[:cntrl:]中的任意字符
* [:space:] 包括空格在内的任意空白字符 (同[\\f \\n \\r \\t \\v])
* [:xdight:] 任意十六进制数字 (同[a-f A-F 0-9])

### 9.2.7 匹配多个实例
`select prod_name from products where prod_name regexp '\\([0-9] sticks?\\)' order by prod_name;`

`select prod_name from products where prod_name regexp '[:digit:]' order by prod_name;`

`select prod_name from products where prod_name regexp '[:digit:]{4}' order by prod_name;`

`select prod_name from products where prod_name regexp '[0-9][0-9][0-9][0-9]' order by prod_name;`

### 9.2.8 定位符
* ^ 文本的开始  $ 文本的结尾  [[:<:]] 词的开始   [[:>:]] 词的结尾
`select prod_name from products where prod_name regexp '^[0-9\\.]' order by prod_name;`


like匹配整个串而regexp匹配子串

# 第10章  创建计算字段

## 10.1 计算字段(field)

## 10.2 拼接字段
`select Concat(vend_name,' (',vend_country,')') from vendors order by vend_name;`
* Concat()拼接串，即把多个串连接起来形成一个较长的串。
* Concat()需要一个或多个指定的串，各个串之间用逗号分隔。

`select Concat(vend_name,' (',vend_country,')') as vend_title from vendors order by vend_name;`

`select Concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`
使用别名
`select Concat(RTrim(vend_name),' (',RTrim(vend_country),')') as vend_title from vendors order by vend_name;`

## 10.3 执行算术计算
`select prod_id,quantity,item_price from orderitems where order_num = 20005;`

`select prod_id,quantity,item_price,quantity*item_price as expanded_price from orderitems where order_num = 20005;`


# 第11章 使用数据处理函数

## 11.1 函数

## 11.2 使用函数

### 11.2.1 文本处理函数

`select vend_name,Upper(vend_name) as vend_name_upcase from vendors order by vend_name;`

#### 常用的文本处理函数
* Left() 返回串左边的字符
* Length() 返回串的长度
* L ocate() 找出串的一个字串
* Lower() 将串转换为小写
* LTrim() 去掉串左边的空格
* Right() 返回串右边的字符
* RTrim() 去掉串右边的空格
* Soundex() 返回串的SOUNDEX值
* SubString() 返回字串的字符
* Upper() 将串转换为大写

`select cust_name,cust_contact from customers where soundex(cust_contact) = soundex('Y Lie');`

## 11.2.2 日期和时间处理函数

* AddDate() 增加一个日期（天、周等）
* AddTime() 增加一个时间（时、分等）
* CurDate() 返回当前日期
* CurTime() 返回当前时间
* Date()    返回日期时间的日期部分
* DateDiff() 计算两个日期之差
* Date_Add()高度灵活的日期运算函数
* Date_Format() 返回一个格式化的日期或时间串
* Day()     返回一个日期的天数部分
* Dayofweek() 对于一个日期，返回对应的星期几
* Hour()    返回一个小时的小部分
* Minute()  返回一个时间的分钟部分
* Month()   返回一个日期的月份部分
* Now()    返回当前日期的时间
* Second() 返回一个时间的秒部分
* Time()   返回一个时间的时间部分
* Year()   返回一个日期的年份部分




`select cust_id,order_num from orders where order_date = '2005-09-01';`

`select cust_id,order_num from orders where Date(order_date) = '2005-09-01';`

书中未写出的
`select cust_id,order_num from orders where Time(order_date) = '00:00:00';`

`select * from orders where Date(order_date) >= '2005-09-01';`

`select cust_id,order_num from orders where Date(order_date) between '2005-09-01' and '2005-09-30';`

`select cust_id,order_num from orders where year(order_date) = 2005 and month(order_date) = 9;`
## 11.2.3 数值处理函数

* Abs()  返回一个数的绝对值
* Cos()  返回一个角度的余弦
* Exp()  返回一个数的指数值
* Mod() 返回除操作的余数
* Pi()     返回圆周率
* Rand() 返回一个随机数
* Sin()  返回一个角度的正弦
* Sqrt() 返回一个数的平方根
* Tan()  返回一个角度的正切

# 第12章  汇总数据

## 12.1 聚集函数 (aggregate function) 运行在行组上，计算和返回单个值的函数

* AVG()  返回某个列的平均值
* COUNT() 返回某列的行数
* MAX() 返回某列的最大值
* MIN() 返回某列的最小值
* SUM() 返回某列值之和

## 12.1.1 AVG() 函数

`select AVG(prod_price) as avg_price from products;`

`select avg(prod_price) as avg_price from products where vend_id = 1003;`

## 12.1.2 COUNT()函数

`select count(*) as num_cust from customers;`

`select count(cust_email) as num_cust from customers;`


## 12.1.3 MAX()函数

`select max(prod_price) as max_price from products;`

## 12.1.4 MIIN()函数

`select min(prod_price) as min_price from products;`

## 12.1.5 SUM()函数

`select sum(quantity) as items_ordered from orderitems where order_num = 20005;`

`select sum(item_price*quantity) as total_price from orderitems where order_num = 20005;`

## 12.2 聚集不同值
`select avg(distinct prod_price) as avg_price from products where vend_id = 1003;`

## 12.3 组合聚集函数
(```)
select count(*) as num_items,
          min(prod_price) as price_min,
          max(prod_price) as price_max,
          avg(prod_price) as price_avg
from products;
(```)
# 第13章  分组数据

## 13.1 数据分组
`select count(*) as num_prods from products where vend_id = 1003;`

## 13.2 创建分组
`select vend_id,count(*) as num_prods from products group by vend_id;`

## 13.3 过滤分组

`select cust_id,count(*) as orders from orders group by cust_id having count(*) >= 2;`

`select vend_id,count(*) as num_prods from products where prod_price >= 10 group by vend_id having count(*) >= 2;`

`select vend_id,count(*) as num_prods from products group by vend_id having count(*) >= 2;`

## 13.4 分组和排序

        order by                            group by
       排序产生的输出                     分组行。但输出可能不是分组的顺序

      任意列都可以使用                    只可能使用选择列或表达式列，而且必须使用
    (甚至非选择的列也可以使用)            每个选择列表达式

        不一定需要                         如果与聚集函数一起使用列（或表达式），则必须使用

`select order_num,sum(quantity*item_price) as ordertotal from orderitems group by order_num having sum(quantity*item_price) >= 50;`

`select order_num,sum(quantity*item_price) as ordertotal from orderitems group by order_num having sum(quantity*item_price) >= 50 order by ordertotal;`

## 13.5  select子句顺序

        子句               说明               是否必须使用
       select        要返回的列或表达式             是
       from          从中检索数据的表              仅在从表选择数据时使用
       where         行级过滤                     否
       group by      分组说明                 仅在按组计算聚集时使用
       having        组级过滤                     否
       order by      输出排序顺序                  否
       limit         要检索的行数                  否

# 第14章  使用子查询

## 14.1 子查询
* select语句是sql的查询。迄今为止我们所看到的所有select语句都是简单的查询，即从单个数据库表中检索数据的单条语句
* 查询(query) 任何sql语句都是查询。但此术语一般指select语句。
## 14.2 利用子查询进行过滤

`select order_num from orderitems where prod_id = 'TNT2';`

`select cust_id from orders where order_num in (20005,20007);`

`select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2');`

`select cust_name,cust_contact from customers where cust_id in (10001,10004);`

`select cust_name,cust_contact from customers where cust_id in (select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2'));`

* 这里给出的代码有效并获得所需的结果。但是，使用子查询并不总是执行这种类型的数据检索的最有效的方法。更多的
论述，请参考第15章，其中将再次给出这个例子。

## 14.3 作为计算字段使用子查询
`select cust_name,cust_state,(select count(*) from orders where orders.cust_id = customers.cust_id) as orders  from customers order by cust_name;`

# 第15章 联结表

## 15.1 联结

### 15.1.1 关系表

* 外键(foreign key)  外键为某个表中的一列，它包含另一个表的主键值，定义了两个表之间的关系。
* 可伸缩行(scale) 能够适应不断增加的工作量而不失败。设计良好的数据库或应用程序称之为可伸缩性好(scale well)。

### 15.1.2 为什么使用联结

 * 联结是一种机制，用来在一条select语句中关联表，因此称之为联结。使用特殊的语法，可以联结多个表返回
 * 一组输出，联结在运行时关联表中正确的行。

## 15.2 创建联结
`select vend_name,prod_name,prod_price from vendors,products where vendors.vend_id = products.vend_id order by vend_name,prod_name;`

* 完全限定列名：在引用的列可能出现二义性时，必须使用完全限定列名（用一个点分隔的表明和列名）。如果
* 引用一个没有用表名限定的具有二义性的列名，Mysql将返回错误。

### 15.2.1 where子句的重要性

* 笛卡尔积(cartesian product) 由没有联结条件的表关系返回的结果为笛卡尔积。检索出的行的数目将是第一个表
* 中的行数乘以第二个表中的行数。

* 不要忘了where子句：应该保证所有联结都有where子句，否则mysql将返回比想要的数据多得多的数据。同理，
* 应该保证where子句的正确性。不正确的过滤条件将导致mysql返回不正确的数据。

### 15.2.2 内部联结

`select vend_name,prod_name,prod_price from vendors inner join products on vendors.vend_id = products.vend_id;`

### 15.2.3 联结多个表

`select prod_name,vend_name,prod_price,quantity from orderitems,products,vendors where products.vend_id = vendors.vend_id and orderitems.prod_id = products.prod_id and order_nmu = 20005;`

`select cust_name,cust_contact from customers where cust_id in (select cust_id from orders where order_num in (select order_num from orderitems where prod_id = 'TNT2'));`
* 子查询并不总是执行复杂select操作的最有效的方法，下面是使用联结的相同查询：

`select cust_name,cust_contact from customers,orders,orderitems where customers.cust_id = orders.cust_id and orderitems.order_num = orders.order_num and prod_id = 'TNT2';`


## 15.3 小结

* 联结是sql中最重要最强大的特性，有效地使用联结需要对关系数据库设计有基本的了解。本章随着对联结的介绍讲述
* 了关系数据库设计的一些基本知识，包括等值联结（也称为内部联结）这种最经常使用的联结形式。

# 第16章 创建高级联结

## 16.1 使用表别名
## 16.2 使用不同类型的联结
### 16.2.1 自联结
### 16.2.2 自然联结
### 16.2.3 外部联结

## 16.3 使用带聚集函数的联结
## 16.4 使用联结和联结条件

