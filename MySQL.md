## MySQL

### 启动 和 停止MySQL服务

- 通过Windows的运行，输入services.msc找到MySQL服务 

- net stop mysql    停止MySQL服务

  net start mysql   开启MySQL服务

### 登录数据库

`mysql -h localhost -P 3306 -u root -p`

-h：主机名

-P：端口

-u：用户名

-p：密码

mysql默认连接localhost和3306，所以可以省略-h和-P

`mysql -u root -p `

### 常用命令

| **命令** | **简写** | **具体含义**                               |
| -------- | -------- | ------------------------------------------ |
| ?        | \?       | 显示帮助信息                               |
| exit     | \q       | 退出MySQL                                  |
| help     | \h       | 显示帮助信息                               |
| quit     | \q       | 退出MySQL                                  |
| status   | \s       | 获取MySQL服务器状态信息                    |
| use      | \u       | 用来选择一个数据库，以一个数据库名作为参数 |

### 修改配置

1. `set character_set_client = gbk;`

2. 通过运行MySQLInstanceConfig.ext程序重新配置

3. 通过修改my.ini文件配置MySQL

   通过配置文件修改的方式记住要重启MySQL服务才能生效

### 数据库基础操作

1. 创建数据库

   `CREATE DATABASE [IF NOT EXISTS] db_name;`

2. 查看数据库

   `SHOW DATABASES;`

3. 删除数据库

   `DROP DATABASE [IF EXISTS] db_name;`

4. 选择数据库

   `USE db_name`

5. 查看当前数据库

   `select DATABASE()`

### 数据类型

| **类型**     | **大小**                                 | **范围（有符号）**                                           | 范围（无符号）                                               | 用途               |
| ------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------ |
| TINYINT      | 1 字节                                   | (-128，127)                                                  | (0，255)                                                     | 小整数值           |
| SMALLINT     | 2 字节                                   | (-32 768，32 767)                                            | (0，65 535)                                                  | 大整数值           |
| MEDIUMINT    | 3 字节                                   | (-8 388 608，8 388 607)                                      | (0，16 777 215)                                              | 大整数值           |
| INT或INTEGER | 4 字节                                   | (-2 147 483   648，2 147 483 647)                            | (0，4 294 967 295)                                           | 大整数值           |
| BIGINT       | 8 字节                                   | (-9 233 372   036 854 775 808，9 223 372 036 854 775 807)    | (0，18 446 744 073 709 551 615)                              | 极大整数值         |
| FLOAT        | 4 字节                                   | (-3.402 823   466 E+38，1.175 494 351 E-38)，0，(1.175 494 351   E-38，3.402 823 466 351 E+38) | 0，(1.175 494 351 E-38，3.402 823 466 E+38)                  | 单精度    浮点数值 |
| DOUBLE       | 8 字节                                   | (1.797 693 134   862 315 7 E+308，2.225 073 858 507 201 4 E-308)，0，(2.225 073 858   507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 0，(2.225 073 858 507 201 4 E-308，1.797 693 134 862 315 7 E+308) | 双精度    浮点数值 |
| DECIMAL      | 对DECIMAL(M,D) ，如果M>D，为M+2否则为D+2 | 依赖于M和D的值，M表示数据长度，D表示小数点后的长度。         | 依赖于M和D的值                                               | 小数值             |

| 类型      | 大小(字节) | 范围                                      | 格式                  | 用途                     |
| --------- | ---------- | ----------------------------------------- | --------------------- | ------------------------ |
| DATE      | 3          | 1000-01-01/9999-12-31                     | YYYY-MM-DD            | 日期值                   |
| TIME      | 3          | '-838:59:59'/'838:59:59'                  | HH:MM:SS              | 时间值或持续时间         |
| YEAR      | 1          | 1901/2155                                 | YYYY                  | 年份值                   |
| DATETIME  | 8          | 1000-01-01   00:00:00/9999-12-31 23:59:59 | YYYY-MM-DD   HH:MM:SS | 混合日期和时间值         |
| TIMESTAMP | 8          | 1970-01-01   00:00:00/2037 年某时         | YYYYMMDD   HHMMSS     | 混合日期和时间值，时间戳 |

如果插入的数值不合法，系统会自动将对应的零值插入到数据库中。

- YEAR

使用4位字符串或数字表示，范围为‘1901‘ ~ ‘2155’或1901~2155

例如，输入‘2016‘或者2016，插入到数据库的值均为2016

- DATE

DATE类型用来表示日期值，不包含时间部分。

可以使用“YYYY-MM-DD“或‘YYYYMMDD‘字符串表示

例如，输入‘2016-10-01‘或’20161001‘插入到数据库的日期都是2016-10-01

- TIME

TIME类型用于表示时间值，它的显示形式一般为HH:MM:SS,其中HH 表示小时，MM表示分，SS表示秒

可以使用下面三种方式指定时间的值：

1. 以“D HH：MM：SS“字符串格式表示。其中，D表示日，可以取0-34之间的值，插入数据时，小时的值等于（D*24+HH）

例如，输入‘2 11:30:50‘，插入数据库的日期为 59:30:50

1. 以‘HHMMSS‘字符串格式或者HHMMSS数字格式表示

例如：输入‘345454‘或345454，插入数据库的日期为34:54:54

1. 使用CURRENT_TIME或NOW()输入当前系统时间

- DATETIME

指定DATETIME类型的值：

1. 以‘YYYY-MM-DD HH:MM:SS‘或者’YYYYMMDDHHMMSS‘字符串或数字都可以。
2. 使用NOW来输入当前系统的日期和时间

- TIMESTAMP类型显示形式和DATETIME相同，但取值范围比DATETIME小。

1. 输入CURRENT_TIMESTAMP输入系统当前日期和时间
2. 输入NULL时，系统会自动输入当前日期和时间
3. 无任何输入时，系统会输入系统当前日期和时间

| CHAR       | 0-255字节             | 定长字符串                      |
| ---------- | --------------------- | ------------------------------- |
| VARCHAR    | 0-65535 字节          | 变长字符串                      |
| TINYBLOB   | 0-255字节             | 不超过 255 个字符的二进制字符串 |
| TINYTEXT   | 0-255字节             | 短文本字符串                    |
| BLOB       | 0-65 535字节          | 二进制形式的长文本数据          |
| TEXT       | 0-65 535字节          | 长文本数据                      |
| MEDIUMBLOB | 0-16 777 215字节      | 二进制形式的中等长度文本数据    |
| MEDIUMTEXT | 0-16 777 215字节      | 中等长度文本数据                |
| LONGBLOB   | 0-4 294 967   295字节 | 二进制形式的极大文本数据        |
| LONGTEXT   | 0-4 294 967   295字节 | 极大文本数据                    |
| BIT        | 1~64位                | 二进制数据                      |

##### CHAR和VARCHAR

| 插入值  | CHAR(4) | 存储需求 | VARCHAR(4) | 存储需求 |
| ------- | ------- | -------- | ---------- | -------- |
| ‘‘      | ‘‘      | 4个字节  | ‘‘         | 1个字节  |
| ‘ab‘    | ‘ab‘    | 4个字节  | ‘ab‘       | 3个字节  |
| ‘abc‘   | ‘abc‘   | 4个字节  | ‘abc‘      | 4个字节  |
| ‘abcd‘  | ‘abcd‘  | 4个字节  | ‘abcd‘     | 5个字节  |
| ‘abcde‘ | ‘abcd‘  | 4个字节  | ‘abcd‘     | 5个字节  |

VARCHAR（4）所对应的数据所占用的字节数为实际长度加1.

总结：

​         字符长度不固定的类型使用VARCHAR       查询的时候要计算字节的长度

​         字符串长度固定的使用CHAR                      查询速度快。

​         VARCAHR比CHAR省空间

​         CHAR比VARCHAR省时间

1. TEXT类型

表示大文本数据，例如：文章内容、评论等     

### 表的基本操作

- 新建表

```
CREAT TABLE table_name 
(
    id INT, name VARCHAR(20), 
    gender CHAR(1),
    birthday DATE,
    job VARCHAR(20),
    salary DOUBLE,
    resume TEXT
)

```

- `show tables`

- `desctable_name`查看表结构

- `show creat table table_name`查看建表语句

- 增加列

  `ALTER TABLE table_name ADD colum datatype;`

- 修改列

  `ALTER TABLE table_name MODIFY colum datatype;`

- 删除列

  `ALTER TABLE table_name DROP colum;`

- 修改表名

  `rename TABLE table_name to new_table_name;`

- 修改列名`

  `ALTER TABLE table_name change colum_name new_colum_name datatype;`

- 删除数据表

  `DROP TABLE table_name;`

### 表的约束

| 约束条件    | 说明                             |
| ----------- | -------------------------------- |
| PRIMARY KEY | 主键约束，用于唯一标识对应的记录 |
| FOREIGN KEY | 外键约束                         |
| NOT NULL    | 非空约束                         |
| UNIQUE      | 唯一性约束                       |
| DEFAULT     | 默认值约束，用于设置字段的默认值 |

- 主键约束

每个数据表中最多只能有一个主键约束，定义为PRIMARY KEY 的字段非空而且唯一

`字段名 数据类型 PRIMARY KEY`

- 非空约束

`字段名 数据类型 NOT NULL;`

- 唯一约束

`字段名 数据类型 UNIQUE;`

- 默认约束

`字段名 数据类型 DEFAULT 默认值;`

- 自增设置

`字段名 数据类型 AUTO_INCREMENT;`

### 添加、更新与删除数据

CRUD       create read update delete 

在cmd中插入中文数据注意：在命令台中要将client的编码设置为gbk才可以。详见1.4.4

#### 添加数据

- 为表中所有字段添加数据

**INSERT INTO** table_name
     **VALUES**(value1,value2,value3...)

注意：

l  values中的值必须与表中的字段一一对应。

l  字符和日期型数据应该包含在单引号中

l  如果要插入一个空值，不指定或者使用NULL

- 为表的指定字段添加数据

**INSERT INTO** table_name (colum1,colum2,colum3...)
     **VALUES** (value1,value2,value3...)

注意values中的值必须与列声明中的列一一对应

- 同时添加多条记录

**INSERT INTO** employee
     **VALUES** (value1,value2,value3...),
             (value1,value2,value3...),
             (value1,value2,value3),
             ...;

#### 更新数据

**UPDATE** table_name
     **SET** col_name1=expr1 [, col_name2=expr2 ...]
     [**WHERE** where_definition]

总结：

l  UPDATE语句可以用新值更新原有表中行的列。

l  SET字句指定要修改哪些列和要给与哪些值

l  WHERE需要给定一个条件，表示要更新符号该条件的行，没有WHERE字句，则更新所有行

#### 删除数据

**DELETE from** table_name
     [**WHERE** where_definition];

#### truncate初始化数据表

**truncate** table_name;

#### **truncate**和**delete**的区别

​         delete会一条一条的删

​         truncate先摧毁整张表，再创建一张和原来的表结构一模一样的表

​         拿拆迁举例子

​         truncate在效率上比delete高

​         truncate只能删除整表的数据，也就是格式化。

​         truncate会把自增id截断恢复为1

总结：

l  DELETE语句如果不使用WHERE语句，将删除表中所有数据

l  使用DELETE语句仅仅删除记录，不删除表本身，如果要删除表，使用DROP TABLE语句

### 单表查询

#### 简单查询

**SELECT** [**DISTINCT**] *|{colum1, colum2, colum3...} **FROM** table_name;

l  SELECT指定查询哪些列的数据

l  column指定列名

l  * 号表示查询所有列

l  FROM 指定查询哪种表

l  DISTINCT 可选，指查询结果时，是否去除重复数据

**SELECT** * **FROM** table_name;

**SELECT** colum1, colum2, colum3... **FROM** table_name;

列的顺序不需要固定，只需要与表中的字段名一致即可.

#### 条件查询

带关系运算符的查询

**SELECT** * **FROM** table_name **WHERE** expr;



在WHERE字句中经常使用的运算符

比较运算符

| \> < <= >= = <> | 大于、小于、大于(小于等于)、不等于          |
| --------------- | ------------------------------------------- |
| BETWEEN…AND     | 显示在某一区间的值 比如：BETWEEN 50 AND 100 |
| IN(set)         | 显示在in列表中的值，例：in(100,200)         |
| LIKE ‘pattern’  | 模糊查询:%_\[][^]                           |
| IS NULL         | 判断是否为空                                |

逻辑运算符

| AND  | 多个条件同时成立                  |
| ---- | --------------------------------- |
| OR   | 多个条件任一成立                  |
| NOT  | 不成立，例：WHERE NOT(salary>100) |

LIKE语句中，**%**代表零个或多个任意字符，_代表一个字符，[]表示符合其中一个：老[1-9] ，[^]表示非其中的一个

### 高级查询

#### 聚合函数

在实际开发中，经常需要对某些数据进行统计，例如统计某个字段的最大值，最小值，平均值等，为此，MySQL提供了一些函数来实现这些功能。

| 函数名称 | 作用               |
| -------- | ------------------ |
| COUNT()  | 返回某行的列数     |
| SUM()    | 返回某列值的和     |
| AVG()    | 返回某列的平均值   |
| MAX()    | 返回某列值的最大值 |
| MIN()    | 返回某列的最小值   |

Ø  **COUNT**（列名）返回某一列，行的总数

**SELECT COUNT**(*) | **COUNT**(列名) **FROM** table_name
     [**WHERE** where_definition];

Ø  **SUM()**函数返回满足WHERE条件的行的和

**SELECT SUM**(列名) {, **SUM**(列名)...} **FROM** table_name
     [**WHERE** where_definition];

注意：SUM仅对数值起作用，否则报错

​         对多列求和，“,”不能少。

Ø  **AVG()**返回返回满足WHERE条件的一列的平均值

**SELECT AVG**(列名) {,**AVG**(列名)...} **FROM** table_name
     [**WHERE** where_definition]

Ø  **MAX()/MIN()**函数返回满足WHERE条件的一列的最大/最小值

**SELECT MAX**(列名) **FROM** table_name
     [**WHERE** where_definition];

#### 对查询结果排序

**SELECT** colum1, colum2, colum3..
     **FROM** table_name
     **ORDER BY** colum **ASC**|**DESC**;

ORDER BY 指定排序的列，排序的列表即可以是表中的列名，也可以是SELECT语句后指定的列名

ASC 升序，DESC 降序

ORDER BY 字句应该位于SELECT 语句的结尾

#### 分组查询

#### 使用LIMIT限制查询结果的数量

**SELECT** colum1, colum2, ...
     **FROM** 表名
     LIMIT [OFFSET, ] 记录数

LIMIT表示从哪一条记录开始往后【不包含该记录】，以及一共查询多少记录

OFFSET表示偏移量，如果为0则表示从第一条记录开始，如果为5则表示从第6条记录开始，默认为0

使用场景：分页查询

LIMIT 5,6：表示从第6开始查询6个

#### 函数（列表）

#### 为表取别名

**SELECT** 表别名.id,表别名.name... **FROM** 表名 **AS** 表别名
     **WHERE** 表别名.id = 2...

#### 为字段取别名

**SELECT** 字段名 [**AS**] 别名 [,字段名 [**AS**] 别名,...] **FROM** 表名;

### 多表查询

#### 外键

为了保证数据的完整性，将两张表之间的数据建立关系，因此就需要在成绩表中添加外键约束。

外键是指引用另一个表中的一列或多列，被引用的列应该具有主键约束或唯一约束。

外键用于建立和加强两个表数据之间的链接。

#### 为表添加外键约束

Ø  创建表的时候添加外键

**CREATE TABLE** department(
     id **INT PRIMARY KEY** auto_increment,
     name **VARCHAR**(20) **NOT NULL** );

 **CREATE TABLE** employee(
     id **INT PRIMARY KEY** auto_increment,
     name **VARCHAR**(20) **NOT NULL**,
     dept_id **INT**,
     **FOREIGN KEY** (id) **REFERENCES** department(id)
 );

Ø  表已经存在，通过修改表的语句增加外键

ALTER TABLE 表名 ADD CONSTRAINT 外键名 FOREIGN KEY(外键字段名) REFERENCES 外表表名(主键字段名);

#### 删除外键约束

ALTER TABLE 表名 DROP FOREIGN KEY 外键名;

#### 连接查询

- 内连接

```
SELECT * FROM employee AS e INNER JOIN dep AS d WHERE e.id = d.id AND ...
SELECT * FROM employee AS e INNER JOIN dep AS d ON e.id = d.id AND ...

```

### Node操作MySQL数据库

使用mysql包

```javascript
var mysql      = require('mysql');
// 创建连接
var connection = mysql.createConnection({
  host     : 'localhost',
  user     : 'me',
  password : 'secret',
  database : 'my_db'
});
 
// 连接数据库
// 可以省略query会自动连接
connection.connect();
 
// 执行操作
// 结果数组
connection.query('SELECT 1 + 1 AS solution', function (error, results, fields) {
  if (error) throw error;
  console.log('The solution is: ', results[0].solution);
});
 
// 关闭连接
connection.end();
```

#### 链接池

```javascript
var mysql = require('mysql');
var pool  = mysql.createPool({
  host     : 'example.org',
  user     : 'bob',
  password : 'secret'
});
 
pool.getConnection(function(err, connection) {
  // Use the connection 
  // mysql提供的利用?的方式给sql传参的方法
  connection.query( 'SELECT something FROM sometable WHERE name=?', [name], function(err, rows) {
    // And done with the connection. 
    connection.release();
 
    // Don't use the connection here, it has been returned to the pool. 
  });
});
```

#### 封装

```javascript
var mysql = require('mysql')

var pool = mysql.creactPool({
    host: 'localhost',
    user: 'me',
    password: 'root',
    database: 'db'
})

exports.query = function(sql, params, callback) {
    let prms = []
    let cb = null
    if(arguments.length === 2 && typeof arguments[1] == 'function') {
        cb = callback
    }else if(arguments === 3 && Array.isArray(arguments[1]) && typeof arguments[2] == 'function') {
        prms = params
        cb = callback
    }else {
        throw new Error("参数个数或类型不匹配")
    }
    pool.getConnection.query(sql, prms, function() {
        connection.release()
        cb.apply(null, arguments)
    })
}

// 使用
const db = require('./db')
sql = ''
db.query(sql, function(err, results) {
    if(err) {
        return next(err)
    }
    ...
})
// 执行的结果判断：插入
result.insertId != 0
// 执行的结果判断：更新
result.affectRows
```

### Models模块

```javascript
// 引入数据库操作模块
var db = require('./db')
function User(user) {
    this.name = user.name
    this.age = user.age
}
User.prototype.save = function(callback) {
    db.jquery(sql, function(err, results) {
        if(err) {
            return callback(err, null)
        }
        callback(results, null)
    })
}
module.exports = User
// cotroller模块使用
let user = new User({
    name: '',
    age: 12
})
user.save(fn)
```

## 