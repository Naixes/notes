## MongoDB

关系型数据库

- `sql`语句操作
- 需要设计表结构
- 约束：主键，默认值等

非关系型数据库

- 库=>库
- 表=>集合
- 数据=>文档对象

不需要设计表结构，灵活

```
{
  // 库
  baidu: {
  	  // 集合
      users:[
        // 文档
        {name:"xx", age: 20},
        ...
      ],
      products: [
      	...
      ]
      ...
  },
  taobao: {
      ...
  }
  ...
}
```

### 启动和关闭数据库

启动

```shell
# 默认使用执行mongod命令盘符根目录下的/data/db作为数据存储目录，需要手动创建
mongod
# 修改默认存储路径
mongod --dbpath=路径
```

关闭：ctrl+c或直接关闭命令行

### 连接退出数据库

连接

```shell
# 默认连接本机服务
mongo
```

退出

```shell
exit
```

### 基本命令

```shell
# 查看数据库
show dbs
# 查看当前数据库
db
# 新建数据库
use 数据库名称
# 插入数据
db.student.insertOne({"name":"haha"})
# 显示所有集合
show collections
# 查询所有数据
db.student.find()
```

### 在Node中操作MongoDB

- 使用官方的mongodb包

- 使用第三方mongoose

  基于mongodb包的封装

  [](mongoosejs.com)

  ```javascript
  var mongoose = require('mongoose')
  // 连接数据库test
  mongoose.connect('mongodb://localhost/test', {useMongoClient: true})
  
  // mongoose.Promise = global.Promise
  
  // 会生成小写的复数的集合名
  var Cat = mongoose.model('Cat', {name: String})
  var kitty = new Cat({name: 'kittyCat'})
  // 持久化保存
  kitty.save(function(err) {
      if(err) {
          console.log(err)
      }
      console.log('meow')
  })
  ```

### mongoose

#### 设计Schema发布Model

```javascript
var mongoose = require('mongoose')
mongoose.connect('mongodb://localhost/test')
// 设计文档结构
var blogSchema = newSchema({
    title: {type: String, require: true},
    author: String,
    gender: {type: Number, enum: [0, 1]}
    comments: [{body: String, data: Date}],
    date: {type: Date, default: Date.now},
    meta: {votes: Number, favs: Number}
})
// 发布模型
// 参数1：集合名称首字母大写，会生成小写的复数的集合名
// 参数2：架构
// 返回： 模型构造函数
var BlogModel = mongoose.model('Blog', blogSchema)
// 使用构造函数
```

#### 操作数据

```javascript
// 新增数据
var blogDoc = new Blog({
    ...
})
blogDoc.save(function(err, ret) {
    
})

// 查询数据
// 查询所有
BlogModel.find(function(err, ret) {
    // ret为结果数组
})
// 条件查询
BlogModel.find({id: 1}, function(err, ret) {
    // ret为结果数组
})
// 查询一个
// 没有条件时返回第一个
BlogModel.findOne({name: 'xx'}, function(err, ret) {
    // ret为结果文档对象
})
// 多个条件只符合一个
BlogModel.findOne({$or[{key1: val1}, {key2: val2}]}, function(err, ret) {
    // ret为结果文档对象
})

// 删除数据
// 删除所有符合条件的数据
BlogModel.remove({条件}, function(err, ret) {})
BlogModel.findOneAndRemove({条件}, function(err, ret) {})
BlogModel.findByIdAndRemove(id, function(err, ret) {})

// 更新数据
BlogModel.update({条件}, {修改内容}, function(err, ret) {})
BlogModel.findOneAndUpdate({条件}, {修改内容}, function(err, ret) {})
BlogModel.findByIdAndUpdate(id, {修改内容}, function(err, ret) {})
```

**注意**：数据库中的id是_id，\_id中有引号可以用replace(/"/, '')去除

### 数据操作模块（Models模块）

将数据操作提取到一个文件crud.js，不关心业务，只存取数据

封装异步代码必须用到callback

```javascript
exports.findAll = function(cb) {
    fs.readFile('', function(err, data) {
        if(err) {
            cb(err)
        }
        cb(null, cb(JSON.parse(data)))
    })
}
exports.save = function(cb) {}
exports.update = function(cb) {}
exports.delete = function(cb) {}

// router.js中调用
var crud = require('./crud.js')
crud.find(function(err, data) {
    if(err) {
        res.status(500).send('Server err')
    }
    res.render('index.html', data)
})
```

## 