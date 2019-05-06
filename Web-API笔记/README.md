# API 第一天：

API：应用程序接口 arr.push()

DOM:页面上所有的动态效果

## 获取元素：

1.通过 id 名获取：

    获取元素  通过id的形式获取   元素    通过id的形式获取 只能通过document获取
     var box = document.getElementById("box");

2.通过标签名的形式获取

    获取元素   通过标签名获取   伪数组（集合）   不管页面有几个元素   获取的都是伪数组
     var li = document.getElementsByTagName("li");

3.通过 class 的形式获取：

    获取元素  通过class的形式获取  伪数组（集合）
    var one = document.getElementsByClassName("one");

4.h5 新增的选择器：

    var box = document.querySelector("div");   .class   #id   标签名  获取一个元素;
    var box = document.querySelectorAll("#box")   .class   #id   标签名 获取所有的元素 伪数组;

5.获取 body 元素：

    document.body;

5.获取 html 元素：

    document.documentElement;

## innerHTML 与 innerText

都是设置 或者 获取元素内容的

获取的区别：

    innerHTML：会获取空格  标签  文本
    innerText: 不会获取空格  标签  只会获取文本

设置的区别：

    innerHTML：会解析标签
    innerText:不会解析标签

## this：事件下面的 this

    事件的调用者  事件的执行者。

## 几个 true 默认的属性

    checked:true:默认选中项
    selected：true: 默认选中项
    disabled:true; 禁用

## className:操作类名

## style:本质是行内样式

## 自定义属性： 自己定义的属性

    获取 元素.getAttribute("属性名")
    设置: 元素.setAttribute("属性名","属性值");
    删除：元素.removeAttribute("属性名")

# h5 新增的自定义属性

定义：

    data-开头  data-name

获取：

    1.  ele.dataset.name;
    2.  ele.dataset["name"];

## 节点：元素节点 文本节点 属性节点

    元素节点：

        1.parentnode  父节点
        2.children  子元素
        3.firstELementChild:第一个子元素
        4.lastELementChild:最后一个子元素
        5.appendChild()
        6.insertBefore()
        7.cloneNode();
        8.createElement();

## 克隆节点:

        cloneNode(true|false)   box.cloneNode(false)
        true: 代表深度克隆   会克隆里面的子元素
        false：浅度克隆   只克隆当前标签

## 创建元素:

    1.createElement("p");
    2.document.write("<p></p>");
    3.innerHTML = "<p></p>";

# 与（javascript:;）=（javascript:volid(0);）区别

    #会刷新页面  阻止页面跳转
    javascript:;  阻止页面跳转

## 事件的几种方式：

    1.  <button onclick="fn(5)">点击</button>
        function fn(a) {
            alert(a)
        }
    2.  btn.onclick = function () {
            alert(1)
        }
    3.  btn.addEventListener("click", function () {
            alert(1)
        })

## 清空事件的几种方式：

    1.  btn.onclick = function () {
            alert(1);
            btn.onclick = null;
        }

    2.  btn.addEventListener("click", fn)
            function fn() {
            alert(1);
            btn.removeEventListener("click", fn)
        }

## 事件流三个阶段 

捕获 目标 冒泡

    捕获： document--->html---body--->父元素--->目标元素；
    冒泡： 目标元素--->父元素--->body--->html--->docuemnt

注意：

    当处于目标阶段的时候 捕获与冒泡谁先定义先执行谁！！
    任何事件都有捕获状态！！！
    事件流与位置没有关系 只要是嵌套都会依次发生事件
    事件对象（事件源参数 e）

target: 

    点击了谁(最里层的元素)；

this: 

    绑定的事件

## 阻止浏览器默认行为：

    1. e.preventDefault();
    2. return false;

## 阻止事件冒泡：

    e.stopPropagation()；

## 事件冒泡的应用场景---事件委托

给外层的元素绑定事件 通过 e.target 找到目标元素 在通过冒泡触发事件---事件委托

事件委托的好处：

    减少内存空间
    提高效率 提升浏览器的加载速度！

## 键盘事件

keydown:

    按下键盘 没有松开时候一直触发事件

keyup： 

    弹起键盘时候触发；

# bom加载事件：

    1.load window.onload = function(){} 等到页面元素，外部的 js，图片和引用其他的资源绘制完毕再加载事件。
    2.DOMContentLoaded： 等到页面元素绘制完毕加会加载事件。
    3.resize：当窗口发生变化的时候触发事件;

## 延时器： 只执行一次 当前函数里的内容

    setTimeout(function(){
        console.log(1)
    },毫秒)

### 清除延时器的方式：

    1.clearTimeout(timer)

## 定时器： 重复执行 当前函数里的内容

    setInterval(function () {
        console.log(1)
    },毫秒数)

## this 指向：

this 当调用时候确定 this 指向  ,  当定义时候不能确定 this 指向！！ 

    1.普通函数调用-------指向的是 window（永远）; 
    2.方法调用-----当前调用的对象 事件----当前调用的对象 
    3.构造函数调用：高级回来！！！！! call apply bind(); 
    4.  setInterval(function () {
            console.log(this) //window
        },毫秒数)

## javascript 单线程：

同一时间只能做一件事 上做完之后再继续执行下一件事

    同步：做一件事 造成性能问题；
    异步：做多个事 当执行主线程的内容 定时器放在任务队列里面

## javascript 运行机制： 

    1.先执行主线程里的代码  
    2.当发现 定时器 会把定时器 放到任务对列里面去执行
    3.继续向下执行等主线程的所有代码执行完毕之后再去执行任务队列里的代码
    4.循环去任务队列里面去执行代码 （事件循环）
    5.执行完之后把任务队列清空；

放到任务队里的东西：

    定时器 延时器 ajax 事件 es6---promise

setInterval setTimeout 0 误差--（0.4-10s）

## location 对象：

### 属性：

    href：设置或者获取地址栏信息路径
    search： 获取地址栏参数 ?name=kf&age=18
    pathname:返回路径  
    host:主机名
    port：端口号；

### 坐标系列：

3 组大小位置相关的属性：

    1.offset:
    1.offsetWidth: 获取当前元素的宽度 （包含 width + padding + border）
    2.offsetHeight：获取当前元素的高度 （包含 width + padding + border）
    3.offsetLeft: 获取当前元素距离带有定位父元素的坐标
    4.offsetTop: 获取当前元素距离带有定位父元素的坐标
    5.offsetParent：获取带有定位的最近父元素

offset 与 style

    offset: 获取的是内部样式 不带单位 获取元素位置
    style:获取行内样式 带单位 不包含 padding 及 border 设置元素位置
