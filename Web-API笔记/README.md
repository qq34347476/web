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

## innerHTML与innerText

都是设置 或者 获取元素内容的

获取的区别：

    innerHTML：会获取空格  标签  文本
    innerText: 不会获取空格  标签  只会获取文本

设置的区别：

    innerHTML：会解析标签
    innerText:不会解析标签

## this：事件下面的this

    事件的调用者  事件的执行者。

## 几个true默认的属性

    checked:true:默认选中项
    selected：true: 默认选中项
    disabled:true; 禁用

## className:操作类名

## style:本质是行内样式

## 自定义属性： 自己定义的属性

    获取 元素.getAttribute("属性名")
    设置: 元素.setAttribute("属性名","属性值");
    删除：元素.removeAttribute("属性名")
