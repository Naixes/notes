

## PHP

超文本预处理器，脚本语言。

主要适用于web开发领域，PHP做出的动态网页，是将程序嵌入到HTML里去执行，效率比完全生成HTML标记的CGI要高很多，PHP还可以执行编译后代码，编译可以加密和优化代码执行，使代码运行更快。

## 语法

1. 块级作用域
2. 变量
3. 导入
4. 数组
5. session
6. 处理表单数据

```php
// index.php
<?php
    // session 会话机制
    php session_start();
	$_SESSION['view'] = 1
?>


<?php
    // 引入
    require_once("a.php");
	// 出错也会继续执行 
	// include_once("a.php");
    
	$a = "测试";
	echo $a;
	if(isset($a)) { // 判断是否被声明
        $b = "块级作用域";
        global $a; // global声明过后可以使用，文件内生效
        $GLOBAL['a'] = "test"; // 全局变量，其他文件也可以使用，使用时也是$GLOBAL['a']
        echo "已声明";
    }else {
        echo "未声明"; // 外部变量内部不能使用
    }
	echo $b; // 内部变量外部不能使用

	// 数组
	$arrayTest = array("0"=>"xx", "1"=>"xx2")
    echo $arrayTest[0]
    
    // session

	// 会话存储
	session_start(); 
	$_SESSION['views'] = 'home';
	echo $_SESSION['views'];
        
    // 处理表单
?>
<form action="submit.php" method="get">
	<p>
		<label for="username">账号</label>
		<input type="text" name="username">
	</p>
	<p>
		<label for="password">密码</label>
		<input type="password" name="password">
	</p>
	<input type="submit" value="提交">
</form>
            
// submit.php
            
<?php
// 设置报头
// header("Content-type:text/html;charset=utf-8");
header("Content-type:text/json;charset=utf-8");
$username = $_REQUEST['username'];
// $username = $_GET['username'];
// $username = $_POST['username'];
if($username === 'admin') {
	echo json_encode(array('msg'=>'登陆成功','code'=>"200"));
}else {
	echo json_encode(array('msg'=>'登陆失败','code'=>"500"));
}
?>
```

7. jquery

```php
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<meta http-equiv="X-UA-Compatible" content="ie=edge">
	<title>PHP</title>
	<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
</head>
<body>
	<?php

	?>
	<form action="submit.php" method="get">
		<p>
			<label for="username">账号</label>
			<input id="username" type="text" name="username">
		</p>
		<p>
			<label for="password">密码</label>
			<input type="password" name="password">
		</p>
		<input id="btn" type="submit" value="提交">
	</form>
	<script>
		console.log($)
		$('#btn').click(function(e) {
			console.log('click')
			e.preventDefault()
			$.ajax({
				url: 'submit.php',
				method: 'GET',
				data: {
					username: $('#username').val()
				},
				success: function(data) {
					console.log(data)
				}
			})
		})
	</script>
</body>
</html>
```

## mysql

LAMP(linux, apache, mysql, php)开发环境

### phpMyAdmin

用来操作mysql

```php
<?php
// Create connection
$con=mysqli_connect("localhost","root","","php_test");

// Check connection
if (!$con)
{
	// .连接字符串
	die("Failed to connect to MySQL: " . mysqli_connect_error());
}else {
	$title = $_REQUEST['newstitle'];
	$img = $_REQUEST['newsimg'];
	$content = $_REQUEST['newscontent'];
	$addtime = $_REQUEST['newsdate'];
	// $result = mysqli_query($con,"INSERT INTO news (title, img, content, addtime) VALUES ('tit', 'png', '内容', '2020-02-20')");
	$result = mysqli_query($con,"INSERT INTO news (title, img, content, addtime) VALUES ('" . $title . "','" . $img . "','" . $content . "','" . $addtime . "')");
	if(!$result) {
		die('Error:' . mysqli_error($con));
	}else {
		echo 'ok';
	}
	mysqli_close($con);
}
?>
```

## PDO

PHP 数据对象 （PDO） 扩展为PHP访问数据库定义了一个轻量级的一致接口。

PDO 提供了一个数据访问抽象层，这意味着，不管使用哪种数据库，都可以用相同的函数（方法）来查询和获取数据。

PDO随PHP5.1发行，在PHP5.0的PECL扩展中也可以使用，无法运行于之前的PHP版本。

可以通过 PHP 的 phpinfo() 函数来查看是否安装了PDO扩展。

```php
<?php
$dbms='mysql';     //数据库类型
$host='localhost'; //数据库主机名
$dbName='php_test';    //使用的数据库
$user='root';      //数据库连接用户名
$pass='';          //对应的密码
$dsn="$dbms:host=$host;dbname=$dbName";

try {
    $dbh = new PDO($dsn, $user, $pass); //初始化一个PDO对象
    echo "连接成功<br/>";
    /*你还可以进行一次搜索操作
    foreach ($dbh->query('SELECT * from FOO') as $row) {
        print_r($row); //你可以用 echo($GLOBAL); 来看到这些值
    }
		*/
		// 插入一个值
		$query= "INSERT INTO news (title, img, content, addtime) VALUES ('title', 'http://xxx', 'con', '2020-02-20')";
		echo $query;
		$res = $dbh->exec($query);
		echo $res;
		echo "受影响行数" . $res;
    $dbh = null;
} catch (PDOException $e) {
    die ("Error!: " . $e->getMessage() . "<br/>");
}
//默认这个不是长连接，如果需要数据库长连接，需要最后加一个参数：array(PDO::ATTR_PERSISTENT => true) 变成这样：
$db = new PDO($dsn, $user, $pass, array(PDO::ATTR_PERSISTENT => true));

?>
```

## 面向对象

出现：软件危机

软件工程学分为结构化方法（按周期分为分析，设计，编程）和面向对象

OOP：使代码简洁，易维护，高重用

目标：重用性，灵活性，扩展性

特点：封装，继承，多态

### 类和对象

对象的特性：行为，状态，标识

类包含声明，成员属性，成员方法

```php
// 简单
[修饰符] class 类名 {
    [成员属性/变量] // 修饰符 $变量名[=默认值] // 不能是带运算符的表达式，变量，方法或函数调用
    [成员方法/函数] // 修饰符 function 方法名(参数...){}
}

// 完整
[修饰符] class 类名 [extends 父类][implements 接口1,[, 接口2]] {
    [成员属性/变量]
    [成员方法/函数]
}

$对象名称 = new 类名称();
$对象名称 = new 类名称([参数列表]);
$对象名称 -> 成员属性 = 赋值;
echo $对象名称 -> 成员属性;
$对象名称 -> 成员方法(参数);

$this;
    
"xxx{$变量名}"
```

#### 构造方法和析构方法

```php
<?php
	class Person {
		// 构造函数：new的时候执行
		public function __construct($age) {
			$this->age = $age;
		}
		// 析造函数：对象销毁时执行
		public function __destruct() {
			// 可以进行资源的释放，数据库关闭，读取文件关闭
			echo "bye" . $this->age;
			echo "bye {$this->age}";
		}
		public function getAge() {
			return $this->age;
		}
	}

	$p1 = new Person(30);
	$p2 = new Person(20);
	echo $p1->getAge();
?>
```

### 封装性

#### 私有成员

修饰符：public，private，protected（子类可访问）

魔术方法：`__get, __set, __isset, __unset`

```php
<?php
	class Person {
		public $name;
		private $age;
		protected $money;

		// 构造函数：new的时候执行
		public function __construct($name, $age, $money) {
			$this->name = $name;
			$this->age = $age;
			$this->money = $money;
		}

		// 魔术方法：只适用于私有或保护
		
		public function __get($key) {
			// if($key === 'age') {
			// 	return $this->age;
			// }
			return $this->$key;
		}

		public function __set($key, $value) {
			if($key === 'money') {
				echo "ok";
				$this->money = $value;
			}
		}

		// 判断时触发
		public function __isset($key) {
			if($key === 'money') {
				return true;
			}
		}

		// 删除属性时触发
		public function __unset($key) {
			if($key === 'money') {
				unset($this->money);
			}
		}
	}

	$p1 = new Person('a', 18, 10);
	echo $p1->name;
	echo $p1->age;
	$p1->money = 20;
	echo $p1->money;
	// 显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。
	var_dump(isset($p1->money));
	// isset：私有会返回false
	var_dump(isset($p1->age));
	unset($p1->money);
	echo $p1->money;
?>
```

### 继承

php只允许单继承

### 多态

子类重载父类的方法时

```php
<?php
	class Person {
		public $name;
		private $age;
		protected $money;

		// 构造函数：new的时候执行
		public function __construct($name, $age, $money) {
			$this->name = $name;
			$this->age = $age;
			$this->money = $money;
		}

		public function getSex() {
			echo "unknow";
		}
	}

	class Man extends Person{
		public $sex;

		public function __construct($name, $age, $money) {
			parent::__construct($name, $age, $money);
			$this->sex = "man";
		}

		// php重写，5.4以后需要与父类参数个数一致否则会报警告
		public function getSex($name) {
			// php实现重载
			parent::getSex();
			echo "{$name} is {$this->sex}";
		}
	}

	$man1 = new Man('jack', 18, 200);
	// 参数不对会报错
	// $man1->getSex();
	$man1->getSex('jack');
?>
```

### 抽象类和接口

#### 抽象方法和抽象类

抽象方法：没有方法体和花括号直接分号结束，包含这种方法的类一定是抽象类

抽象类：以abstract声明

抽象类特点：不能实例化，要想使用抽象类，就必须定义一个类继承这个抽象类，并定义覆盖父类的抽象方法（实现抽象方法）

#### 接口

为了解决只能单继承的问题

制定了一个实现了该接口的类必须实现的一系列函数

```php
interface 接口名称 {
    // 常量成员（使用const关键字定义）
    // 抽象方法（不需要abstract关键字）
}
class 类名 implements 接口1, 接口2{...}
```

##### 与抽象类的区别

接口是对动作的抽象，表示能做什么，对类的局部行为进行抽象

抽象类是对根源的抽象，表示是什么，对整体进行抽象

所以类只能继承一个类，但可以实现多个接口

对象的多态性：是指父类中定义的属性或方法被继承之后，可以有不同的数据类型或表现出不同的行为。

```php
<?php
	// 接口中的方法都是抽象的
	// 接口中可以声明常量
	interface Action {
		const NAME = 'jack';
		public function run();
		public function eat();
	}
	interface Study {
		public function study();
	}

	// 抽象类中也可以有普通方法
	abstract class Person implements Action, Study {
		const PI = 3.14;
		// public abstract function eat();
		// public abstract function run();
		// public abstract function study();
	}

	class Student extends Person {
		const PI = 3.14;
		public function eat() {
			echo "eat";
		}
		public function run() {
			echo "run";
		}
		public function study() {
			echo "study";
		}
		public function getPI() {
			echo self::PI;
		}
	}

	$stu1 = new Student();
	$stu1->eat();
	$stu1->run();
	$stu1->study();
	// 获取常量
	$stu1->getPI();
	echo Action::NAME;
	echo Person::PI;
	echo Student::PI;
?>
```

### 常见的关键字

#### final

只能修饰类和方法

特性：修饰类不能被继承；修饰方法不能被重写

目的：安全；需求

#### static

表示静态，用于修饰成员属性和方法

修饰后可以直接使用类名访问，不用实例化

`self::$静态属性; self::静态方法`

静态方法不能使用非静态的内容，即不能使用$this

#### 单例设计模式

#### const

define()可以定义常量，但是在类中常使用const定义常量

#### instanceof

用于检测当前对象是否属于某一类或其子类

### 常用方法

### 错误处理

#### 系统自带的异常处理

```php
<?php
try{
	$num = 2;
	if($num === 1) {
		echo "success";
	}else{
		throw new Exception("num应该等于1");
	}
}catch(Exception $e){
	echo "错误文件为：";
	echo $e->getFile();
	echo "错误行数为：";
	echo $e->getLine();
	echo "错误代码为：";
	echo $e->getCode();
	echo "错误信息为：";
	echo $e->getMessage();
}
?>
```



#### 自定义的异常处理

```php
<?php
class myException extends Exception{
	public function getAllInfo() {
		return "错误文件为：{$this->getFile()}，错误行数为：{$this->getLine()}，错误代码为：{$this->getCode()}，错误信息为：{$this->getMessage()}";
	}
}
try{
	$num = 3;
	if($num === 1) {
		echo "success";
	}elseif($num === 3){
		throw new myException("num不应该等于3");
	}elseif($num === 4){
		throw new Exception("num不应该等于4");
	}
	// 可捕获多个不同类型的异常，注意顺序
}catch(myException $e){
	echo $e->getAllInfo();
}catch(Exception $e){
	echo $e->getMessage();
}
?>
```

### 其他

#### 魔术方法

__toString：在直接输出引用对象时调用

```php
<?php
// Declare a simple class
class TestClass {
    public $foo;
 
    public function __construct($foo) {
        $this->foo = $foo;
    }
 
    // 定义一个__toString方法，返加一个成员属性$foo
    public function __toString() {
        // 一定要有返回值
        return $this->foo;
    }
}
 
$class = new TestClass('Hello');
 
// 直接输出对象
echo $class;
?>
```

__clone：根据一个对象完全克隆出一个一模一样的对象，而且克隆以后，两个对象互不干扰

```php
<?php
class Person {
    // 下面是人的成员属性
    var $name;  // 人的名子
    var $sex;   // 人的性别
    var $age;   // 人的年龄
 
    // 定义一个构造方法参数为属性姓名$name、性别$sex和年龄$age进行赋值
    function __construct($name = "", $sex = "", $age = "") {
        $this->name = $name;
        $this->sex = $sex;
        $this->age = $age;
    }
 
    // 这个人可以说话的方法，说出自己的属性
    function say() {
        echo "我的名子叫：" . $this->name . " 性别：" . $this->sex . " 我的年龄是：" . $this->age . "<br>";
    }
}
 
$p1 = new Person("张三", "男", 20);
 
// 使用“clone”克隆新对象p2，和p1对象具有相同的属性和方法。
$p2=clone $p1;
$p2->say();
?>
    
// __clone  
<?
class Person {
    // 下面是人的成员属性
    var $name;  // 人的名子
    var $sex;   // 人的性别
    var $age;   // 人的年龄
 
    // 定义一个构造方法参数为属性姓名$name、性别$sex和年龄$age进行赋值
    function __construct($name = "", $sex = "", $age = "") {
        $this->name = $name;
        $this->sex = $sex;
        $this->age = $age;
    }
 
    // 这个人可以说话的方法, 说出自己的属性
    function say() {
        echo "我的名子叫：" . $this->name . " 性别：" . $this->sex . " 我的年龄是：" . $this->age . "<br>";
    }
 
    // 对象克隆时自动调用的方法, 如果想在克隆后改变原对象的内容，需要在__clone()中重写原本的属性和方法
    function __clone() {
        // $this指的复本p2, 而$that是指向原本p1，这样就在本方法里，改变了复本的属性。
        $this->name = "我是假的 $that->name";
        $this->age = 30;
    }
}
 
$p1 = new Person("张三", "男", 20);
$p2 = clone $p1;
$p1->say();
$p2->say();
?>
```

serialize()：有时候需要把一个对象在网络上传输，为了方便传输，可以把整个对象转化为二进制串，等到达另一端时，再还原为原来的对象，这个过程称之为**串行化(也叫序列化)**。我们使用**serialize()**函数来串行化一个对象，另一个是**反串行化**，就是把对象转化的二进制字符串再转化为对象， 我们使用**unserialize()**函数来反串行化一个对象。

两种情况：把一个对象在网络中传输的时候要将对象串行化；把对象写入文件或是数据库的时候用到串行化。

```php
<?php
class Person {
    // 下面是人的成员属性
    var $name;    // 人的名子
    var $sex;     // 人的性别
    var $age;     // 人的年龄
 
    // 定义一个构造方法参数为属性姓名$name、性别$sex和年龄$age进行赋值
    function __construct($name = "", $sex = "", $age = "") {
        $this->name = $name;
        $this->sex = $sex;
        $this->age = $age;
    }
 
    // 这个人可以说话的方法, 说出自己的属性
    function say() {
        echo "我的名子叫：" . $this->name . " 性别：" . $this->sex . " 我的年龄是：" . $this->age . "<br>";
    }
}
 
$p1 = new Person("张三", "男", 20);
$p1_string = serialize($p1);         // 把一个对象串行化，返一个字符串
echo $p1_string . "<br>";           // 串行化的字符串我们通常不去解析
$p2 = unserialize($p1_string);      // 把一个串行化的字符串反串行化形成对象$p2
$p2->say();
?>
```

`__sleep()`和`__wakeup()`：序列化的时候会调用一个`__sleep()`方法来完成一些事情；而在由二进制串重新组成一个对象的时候，则会自动调用PHP的另一个函数`__wakeup()`，做一些动作。

`__sleep()`函数不接受任何参数， 但返回一个数组，其中包含需要串行化的属性。末被包含的属性将在串行化时被忽略，如果没有`__sleep()`方法，PHP将保存所有属性。

```php
<?
class Person {
    // 下面是人的成员属性
    var $name;  // 人的名子
    var $sex;   // 人的性别
    var $age;   // 人的年龄
 
    // 定义一个构造方法参数为属性姓名$name、性别$sex和年龄$age进行赋值
    function __construct($name = "", $sex = "", $age = "") {
        $this->name = $name;
        $this->sex = $sex;
        $this->age = $age;
    }
 
    // 这个人可以说话的方法, 说出自己的属性
    function say() {
        echo "我的名子叫：" . $this->name . " 性别：" . $this->sex . " 我的年龄是：" . $this->age . "<br>";
    }
 
    // 指定串行化时把返回的数组中$name和$age值串行化，忽略没在数组中的属性$sex
    function __sleep() {
        $arr = array("name", "age"); // 此时，属性$sex将被删除！！！
        return($arr);
    }
 
    // 重新生成对象时，并重新赋值$age为40
    function __wakeup() {
        $this->age = 40;
    }
}
 
$p1 = new Person("张三", "男", 20);
 
// 把一个对象串行化，返一个字符串，调用了__sleep()方法,忽略没在数组中的属性$sex
$p1_string = serialize($p1);
echo $p1_string . "<br>"; // 串行化的字符串我们通常不去解析
 
$p2 = unserialize($p1_string); // 反串行化形成对象$p2重新赋值$age为40
$p2->say();
?>
```

##### 自动加载类

php5中当new一个不存在的类时，会自动调用__autoload()，并将类名作为参数传入此函数。可以实现类的自动加载。

## 与js比较

类，继承