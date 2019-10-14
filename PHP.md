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
    echo $_SESSION['view']
        
    // 处理表单
    header("Content-type:text/html;charset=utf-8")
    $username = $_GET["usernmae"]
    $username = $_POST["usernmae"]
    $username = $_REQUEST["usernmae"]
    if($username == 'damin') {
        echo json_encode(array('mag'=>'登陆成功', 'errCode'=>'ok'))
    }
?>
```

##  mysql

### phpMyAdmin

用来操作mysql