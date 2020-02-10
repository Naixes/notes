

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