# 面向对象

    对象
    原型链
    贪吃蛇！！！！优点难
    继承 构造继承  闭包 this指向  正则  函数进阶

## 对象

    不是： java c++
    是： 很多的方法和属性；

面向过程编程！！！

面向对象编程---!

函数式编程（链式编程）.css().css()！！！！

## 面向对象(万物皆对象)

抽象的概念 --- 功能集及数据集的集合！！！

    var dog = {
        color:"red",
        hoddy:"..."
    }

instanceof:

    判断当前实例对象是否属于该构造函数！！！
        arr instanceof Array

constructor:

    指回当前实例的构造函数

## 构造函数：

    就是一个模板，这个模板给实例对象提供一些属性以及方法！

## 实例成员：

    实例对象的属性和方法---实例成员

## 静态成员：

    \$.each() 构造函数的属性和方法----静态成员

## 原型:prototype

为什么使用原型：

    1.减少内存
    2.从开发角度 便于开发
    3.从资源的角度考虑：资源共享

## new 关键字的执行过程：

    1.创建空对象（开辟内存空间）
    2.空对象的指针分配给 prototype（原型）
    3.空对象的指针在分配实例对象
    4.当发现没有 return 返回 this；

## 属性的搜索原则：

    1.当实例对象调用方法和属性的时候
      先去构造函数本身去找
      如果构造函数里面有对应的属性和方法,停止查找
    2.当构造函数没有
      去当前构造函数的原型对象去找
    3.如果还没有
      去原型的原型的原型对象最终的结果是 null

## 属性的设置原则

    当给当前的实例对象设置属性或方法的时候
    会给当前对象添加属性或方法（不会去原型去原型对象下修改） 新增！！！

    当给原型对象重新赋值一个对象的时候 会改变 constructor 属性 所以要手动去设置下

## 继承

继承自己没有， 拿别人的来用 就是自己的一样--继承

改变 this 指向 --->在某种环境下执行---->在特定的环境下调用！！！！

    call:改变this指向
    bind：改变this指向
    apply：改变this指向

    三者的区别：改变函数中的this
        1.call(this,name,age)  参数 this指向  具体的参数  会自调用
        2.apply(this,[name,age]) 参数this的指向  具体的参数
            要加数组的形式(不代表传的参数是数组) 会自调用
        3.bind(this,name,age)  参数 this指向  自己不会调用  只是改变this指向
        如果函数内部不传参数 或者传null  就是函数调用  window

继承的方式：

原型继承：

    function Person(name, age) {
    this.name = name;
    this.age = age;
    }
    Person.prototype.sayhi = function () {
    console.log("hello");
    }
    function Student() {

    };

    Student.prototype = new Person("kf", 20);
    var stu = new Student();
    console.log(stu.name)

## 借用构造函数

借用构造函数继承：

    call() 调用构造函数 改变 this 执行
    function Person(name, age) {
    this.name = name;
    this.age = age;
    }
    Person.prototype.sayhi = function () {
    console.log("hello")
    }
    function Student(name, age, sex) {
    this.sex = sex;
    Person.call(this, name, age)
    }
    var stu = new Student("kf", 1, "男");
    console.log(stu.sayhi());

组合继承：

    function Person(name, age) {
    this.name = name;
    this.age = age
    }
    Person.prototype.sayhi = function () {
    console.log("hello")
    }

    function Teacher(name, age, sex) {
        Person.call(this, name, age)
        this.sex = sex
    }
    Teacher.prototype = new Person();
    var tea = new Teacher(name, age, sex);

快速继承：

    var o = { name: "kf", age: 20 };
    var obj = Object.create(o);
    console.log(obj)

内部的封装

    function create(o) {
    function F() { };
    F.prototype = o;
    return new F();
    }
    var obj = create(o);
    console.log(obj)

## 函数：

### 函数的调用：

    函数式调用： 函数名调用（）
    方法调用： obj.方法
    构造函数调用： new
    上下文调用： call apply bind；

this:

    window：

    1.函数式调用 window
    2.回调函数 函数以参数形式传递
    3.定时器 延时器 window

### 方法调用：

    指向直接调用的方法对象

### 构造函数调用：

    不加 return 默认返回 this
    return {} [] this 指向就是当前返回的对象
    return 1; this 指向还是当前实例对象

## 闭包

## 函数的执行过程：

    调用函数（创建内存地址）
        1.进栈  （进入执行环境）
        2.压栈   执行当前环境的代码
        3.出栈   返回执行环境
        4.销毁   内存空间

## 闭包：

     1.一个封闭的执行环境（隔离区域）
     2.一个作用域可以访问另一个作用域的变量   沙箱模式！！！ 一个具有作用域隔离特性的一个内存结构，
        即为一个闭包

### 闭包到底要解决什么问题：

在 js 当中要解决的问题 就是间接的访问到这个被隔离的数据。

使用 return 数据不能直接访问原来的数据 可以利用函数的返回访问原始数据

    缺点：占用内存！！！
        一个函数内部返回一个函数  函数里面引用着外部函数的变量；
    特点：延展作用域;

    递归：  自己调用自己 一定要有结束条件

        切记：  递归注重的是思想 结果  而不是过程；

## 浅拷贝： 拷贝的是属性 对于对象 拷贝的引用

    function copy(o1, o2) {
    for (var k in o1) {
    o2[k] = o1[k]
    }
    }
    copy(obj, obj1)

## 深拷贝: 拷贝的是属性 对于对象 拷贝的是具体的值

    function deepcopy(o1, o2) {
        for (var k in o1) {
            //因为Array属于Object,所以先判断是否是Array
            if (o1[k] instanceof Array) {  
                o2[k] = [];
                deepcopy(o1[k], o2[k])  //调用归递函数
            //再判断是否是 Object
            } else if (o1[k] instanceof Object) {
                o2[k] = {};
                deepcopy(o1[k], o2[k])  //调用归递函数
            } else {
                o2[k] = o1[k]
            }
        }
     }
    deepcopy(obj, obj1)  //调用函数

## 函数的其他成员：

    name：函数的名字;
    arguments:实参的伪数组;
    arguments.callee打印当前的函数   arguments.callee();

## 正则表达式：

### 创建正则表达式

    1. var reg = /表达式/;
    2. var reg = new RegExp("正则表达式","匹配模式")
        reg.test(匹配对象)
是一个正则匹配的对象 该对象可以对字符串进行 提取  替换  匹配；

### 元字符

    \d:匹配数字的（所有的数字）
    \D:匹配非数字
    \n:换行符
    \w:数字 字母 下划线
    \W:非数字字母 下划线
    * : 紧接着前面的一个字符0次或多次  
    +：紧接着前面的一个字符 出现1次或多次
    ?:0次或1次
    a{3}  aaa  指定次数
    a{3,}  最少3次
    a{1,3}紧跟前面的字符出现的范围
    1(23)* 表示紧跟着前面的一组
    a-z  0-9  A-Z  [0-9a-zA-Z]

基本元字符：

    . 表示任一个非换行的字符
    () 分组 提高优先级
    [] 表示一个字符  例如:[ab]
    | 或者
    转移字符： \  \.

提取：

    exec()  每次只能提取一个
    match() 提取多个 注意是字符串的方法

贪婪模式：

    尽可能提取（查找）很多的数据；

非贪婪模式：

    尽可能提取（查找）少量的数据；

改变贪婪模式；

    * + 等会尽可能多的提取的数据 符号 后面添加 ?
