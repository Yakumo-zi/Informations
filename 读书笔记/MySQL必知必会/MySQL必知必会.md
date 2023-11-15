#MYSQL #数据库 #中间件 

目的：学习SQL语言和MySQL操作
# Ch1.了解SQL

SQL是结构化查询语言（Structured Query Language）的缩写，是一种专门用来与数据库统信的语言，它具有如下优点：
+ 几乎所有DBMS都支持SQL。
+ SQL简单易学。
+ SQL是一种强有力的语言，可以进行非常复杂和高级的数据库操作。

# Ch2.MySQL简介

MySQL是一种DBMS，是一种数据库软件，它具有如下优点：
+ MySQL是开放源代码的，可以免费使用
+ MySQL执行很快
+ MySQL是值得信赖的，有大量的公司都使用MySQL来处理自己的数据
+ MySQL安装和使用非常简单

MySQL是基于CS架构的数据库，它由客户端和服务端两个部分组成，其中服务端部分是负责所有数据访问和处理的软件，**通常运行在数据库服务器上**作为一个单独的服务，而客户端部分是用于连接和操作数据库服务端的软件，用于编写SQL发送给服务器执行，并接收服务器的响应。

客户端可以使MySQL提供的CLI，也可以是其他语言实现的MySQL驱动，例如JDBC，ODBC等可以通过程序设计语言操作数据库的，都可以叫做客户端。

使用MySQL CLI连接服务端端:

```shell
mysql -u <user> -p <port> -h <host>
# mysql -u root -p 3306 -h 127.0.0.1
# 如果有密码则会要求输入密码
```

进入MySQL 客户端后，每条SQL语句使用 `;` 结束，如果没有以这字符结束，那么客户端会报错。

进入客户端后使用`help;`，即可获取MySQL帮助指南：

![[help.png]]

使用 `quit;`或者`exit;`来退出MySQL客户端：

![[quit.png]]

# Ch3.使用MySQL

在最初连接到MySQL时，没有任何数据库打开。**在执行任何数据库操作前，需要选择一个数据库**。使用`USE`关键字选择数据库。语法如下：

```sql
USE <database name>;
-- USE mydatabase
```

![[use.png]]

如果不知道有那些数据库，可以使用`SHOW`命令来展示当前有那些数据库，语法如下：

```SQL
SHOW DATABASES;
```

![[show databases.png]]

`SHOW`命令还可以获得一个数据库内部有那些表，语法如下：

```SQL
SHOW TABLES;
```

要注意的是，使用该命令的前提是，已经使用`USE`关键字打开了一个数据库，否则会报错。

还可以使用`SHOW`命令查看一个表中有那些列，以及该列的类型和约束，语法如下：
```SQL
SHOW COLUMNS FROM <TABLENAME>;
-- SHOW COLUMNS FROM user;
```

![[show columns.png]]

`SHOW`命令还有以下几种常用的用法：

```SQL
SHOW STATUS; -- 显示服务器状态信息
SHOW CREATE <dtabase name>; -- 用于显示创建指定数据库的SQL语句
SHOW CREATE <table name>; -- 用于显示创建指定表的SQL语句
SHOW GRANTS; -- 用于显示授予用户的权限
SHOW ERRORS; -- 显示服务器的错误消息
SHOW WARNINGS; -- 显示服务器的警告信息
```

关于`SHOW`的更多信息，可以在MySQL CLI中使用 `HELP SHOW;`来显示`SHOW`的所有用法。

# Ch4.检索数据

在MySQL中，使用`SELECT`语句来检索数据，该语句可以检索数据库中一个表或者多个表的数据，一个简单的语法实例：

```SQL
SELECT prod_name FROM products;
```

该语句从products表中查询一个名为prod_name的列，结果是该列的所有数据。

注意：
+ SQL语句不区分大小写。
+ 如果有多条SQL语句，那么每条SQL语句必须以`;`结尾。

上面的示例中只检索了表中一个列，`SELECT`也可以检索表中的多个列，语法格式如下：

```SQL
SELECT column1,column2 FROM tablename;
```

每个列需要以`,`分隔开来，并且最后一个列之后不需要加`,`，否则会报错。

如果想检索所有的列，那么可以使用通配符`*`，语法格式如下：

```SQL
SELECT * FROM tablename;
```

这条语句就可以检索一个表中的**所有列**。

如果查询出来的记录有重复值，而我们不需要重复值，或者不想看到重复值，那么可以在`SELECT`语句后加上`DISTINCT`来表示要**消除重复的记录**，语法格式如下：

```SQL
SELECT DISTINCT * FROM tablename;
SELECT DISTINCT column1,column2 FROM tablename;
```

这样查询出来的记录就不会有重复值了。

如果查询出来的结果太多，不想要这么多，只想要其中的一条或者几条，那么可以使用`LIMIT`子句来限制查询出来的记录数，语法格式如下：

```SQL
SELECT * FROM tablename LIMIT 5; --表示返回的记录不多与5行
```

`LIMIT` 子句还有以下格式：

```SQL
SELECT * FROM tablename LIMIT 5,5; --表示从返回记录的第5行开始取不多于5行的数据。
```

# Ch5.排序检索数据

使用`SELECT`语句查询出来的记录默认是没有特定顺序的，插入的顺序是怎样，查询出来的顺序就是怎样的，如果想得到指定顺序的记录，那么可以给`SELECT` 语句加上一个`ORDER BY`子句来指定按那个列进行排序，语法格式如下：

```SQL
SELECT * FROM tablename ORDER BY column;
```

默认没排序的结果是这样的：

![[unordered.png]]

按照`s_score` 排序的结果是这样的：

![[ordered.png]]

`ORDER BY`默认是升序排序，如果想降序排序，那么还需要再`ORDER BY`子句后面跟一个 `DESC` 关键字。

```SQL
SELECT * FROM tablename ORDER BY column DESC;
```

降序排序的结果是这样的：

![[desc ordered.png]]

`ORDER BY`子句还可以指定多个列作为排序的依据，它的排序规则是这样的，首先对第一个列进行排序，如果第一个列相等，那么再依据第二个列进行排序，如果第二个列相等再对第三个列进行排序，以此类推。

使用`ORDER BY`子句和`LIMIT`子句，可以达到查询某一列的最高值或者某一列的最低值的效果，以下是两个示例，一个是查询最高成绩，一个是查询最低成绩。

![[highest and lowest.png]]

**注意：**
`ORDER BY`子句进行排序时，默认是不区分大小写的，但是可以通过设置进行改变。

# Ch6. 过滤数据

数据库表中一般包含大量的数据，很少需要检索表中所有行。通常只会根据特定需求提取其中一部分数据。

在`SELECT`，可以使用`WHERE`子句来指定搜索的条件，语法格式如下：

```SQL
SELECT * FROM tablename WHERE <condition>;
```

其中`condition`，可以有以下几种逻辑关系：
1. 等于 `=`
2. 大于 `>`
3. 小于 `<`
4. 大于等于 `<=`
5. 小于等于 `>=`
6. 不等于 `<>`或者`!=`
7. 两个值之间 `BETWEEN lower AND HIGH`

以下是使用上述条件的示例：

等于，小于，大于

![[eq lt gt.png]]

大于等于，小于等于

![[let get.png]]

不等于

![[not eq.png]]

`BETWEEN AND`

![[between and.png]]