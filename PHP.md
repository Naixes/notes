```php
// index.php
<?php
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
	if(isset($a)) {
        $b = "块级作用域";
        global $a; // global声明过后可以使用
        $GLOBAL['a'] = "test"; // 全局变量，其他文件也可以使用 
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
?>
```

