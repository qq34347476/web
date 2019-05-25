# PHP

## 服务器的概念：

    是网络为客户端计算机提供各种服务的高性能计算机
    服务器就是个软件
        这个软件主要是可以为客户端提供服务的软件  
        ---- 如果参与运算程序需要配合后台语言java   php   c；
    只有当其他计算机中的浏览器发出请求时 服务器才能响应
B/S架构：

    浏览器与服务器交互；

C/S架构：

    下载到本地 在与服务器交互；

ip：

    每台计算机的标识 ---作为一个计算机的标识

url:

    地址栏中输入的网址url  统一资源定位符    http:www.baidu.com/index.html?id=1  

http:\\  和  https:\\

    超文本传输协议  服务器传输超文本到本地浏览器的传送协议；

    注意：
        http是无链接 含义是每次链接只处理一个请求 收到客户的应答即断开；
        http请求时无状态请求  是指对事物没有记忆能力  CGI处理程序

www：

    万维网服务器 是指世界各地的计算机网络
        baidu.com： 是百度的域名
        index.html：文件路径

域名与ip地址对应关系：

    多个域名可以对应一个ip地址

## php的特点：

    1.混合了c  java  php自创的语法
    2.php可以将程序嵌入到网页中去
    3.支持所有流行的数据库以及操作系统
    4.弱类型

## php的输出语句：

    echo  只能输出字符串 等单一数据 不能输出数据类型 数组等
    print(): 只能输出字符串 等单一数据  不能输出数据类型 数组等有返回值
    print_r(): 可以输出字符串 数组。。可以输出复杂数据类型
    var_dump: 字符串 数据类型  长度
    die()  先输出内容 退出程序

## php中的函数：

    isset():判断变量是否定义；
        如果定义返回true   否则返回false
        在php中true---->1   false---null
    empty():
        判断值是否为空； 0   "0"  false    Array()   null
    unset(): 删除变量

## php中的数组：

索引数组：通过索引操作数组

    $arr = Array(1,2,3,true,"abc");
    $arr = [1,2,3,4,5]

    访问与js一样

隐形数组：$arr[] = 1;给变量增加一个中括号 系统自动生成数字下标 与值

    对于索引数组： 自动递增数组的索引
    对于关联数组： 从0开始索引

二维数组：

    $arr = Array(
        "first"=>Array(
            "name"=>"jack",
            "age"=>20
        ),
        "two"=>Array(
            "name"=>"jack",
            "age"=>20
        )
    );

关联数组：

    以键值对的形式描述数据
        $arr = array(
            "name"=>"jack",
            "age"=>20,
            "gender"=>true
        )  

### 遍历数组：

1.for循环

    for($i = 0;$i<count($arr);$i++){
        只能遍历索引数组
    }

2.foreach循环

    foreach($arr as $key=>$value){
       遍历索引数组  与关联数组
       $key：属性（索引）
       $value 值
    }

    可以简写:
    foreach($arr as $value){
  
    }

数组的注意事项：

    1.如果添加元素的时候设置key name就没有索引
    2.如果没有设置key值 那么系统自动生成索引
    3.如果数组已经存在 那么就将元素添加到当前数组中
    4.如果不存在就先创建 在赋值

二维数组遍历：

    foreach($arr as $value){
        // print_r($value);
        foreach($value as $value1){
            print_r($value1);
        }
    }

## 数据类型转换：

    转换整型：$num = (int)$str;
    转换为浮点型：$int = floatval($num);
    转化为字符串：(String)$str
    转化布尔型： (bool)$str
    算数运算符：
        + - * % ++ --；
    逻辑运算符：
        ! && ||；
    比较运算符：
         >  <  >= <= ==
    三元运算符：
        a>b?"":""

## global:引用全局变量

    1.  不能再引用的同时对变量赋值 
    2.  如果没有参数项引用其他变量  需要global；
    3.  global 本质是引用 改变值全局也会发生变化；

## php字符串拼接：

    字符串与字符串之间用  点(.)
    单引号与双引号的区别：
    双引号会解析变量

## 超全局变量：

    $GLOABLS;
    $_SERVER;
    $_GET
    $_POST
    $_COOKIE
    $_SESSION

只要定义变量 都会存储在超全局变量中的  $GLOABLS;

$GLOABLS 与  global区别：

    $GLOABLS 真实存在的
    global  只是引用

## 定义常量的语法：

    define("常量名称",常量值,true|false)；
    例如： define("PI",3,14,true);  true:不敏感（支持大写和小写）;

## 魔术常量：

    __LINE__ 当前的代码行数
    __FILE__:当前文件夹的路径
    __DIR__:获取文件目录;

## 载入文件： 相当在当前文件下执行代码；

    include:  1.如果引入失败  不会影响下面的元素 可以执行多次;
    include_once:  2.当引入失败不会影响下面 的元素的执行！多次的情况下  只会载入一次。
    require: 如果代码载入失败，后续代码不会执行
    require_once:2.当引入文件失败会影响下面的代码的执行  只能引入一次；

strlen() 获取字符串的长度

时间：

    echo date("Y-M-D H:I:S");

读取文件：

    file_get_contents:读取文件

写入文件：

    覆盖写入文件
        $res = file_put_contents("data.txt","写入的内容",");
    追加写入文件
        $res = file_put_contents("data.txt","写入的内容",FILE_APPEND");