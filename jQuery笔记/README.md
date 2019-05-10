# jq 特点：

    1.隐式迭代
    2.链式编程
    当操作是设置型元素：可以一直链式编程
    当操作是获取型元素：不可以一直链式编程（断链）

# 1.jq 的入口函数

    1.$(function(){

    });

    2.$(document).ready(function(){

    });

    3.jQuery(function(){

    });

# 2.dom 与就 jq 互转

    dom 对象无法使用 jq 对象里的方法；
    jq 对象无法使用 dom 对象的属性和方法；

1.dom 对象转 jq 对象：

    $("div")
        $(div)

2.jq 转 dom 对象：
  
    $("div")[0]

3.jq转dom对象

    $("div").get(0)

# 3.jq 选择器：

    id 选择器： $("#id")  获取指定的id元素
    全选选择器： $("\*") 获取所有
    类选择器： $(".class") 获取指定的class选择器
    标签选择器：  $("div) 获取同一类的所有元素
    并集选择器： $("div,p,li")
    后代选择器： $("div li")
    交集选择器： $("div.current")
    子代选择器： $("div>li")
    含有指定类名的标签选择器: $('div.goback')

# 4.隐式迭代：

    遍历内部的 dom 元素的过程叫做隐式迭代 

# 5.筛选选择器：

    $("li:first") 获取第一个li
    $("li:last") 获取最后一个 li
    $("div:eq(2)") 获取索引为2的元素
    $("div:odd") 奇数
    $("div:even") 偶数

# 6.方法：

    parent()  $("li").parent() 查找父元素
    children(“li”) 最近的儿子
    find("li") 后代选择器
    siblings() 兄弟选择器
    nextAll() 查找当前元素之后的所有同辈元素
    prevAll() 查找当前元素之后的所有同辈元素
    hasClass() 查找当前类名
    eq(index)索引
    addClass（）增加类名

# jq 的链式编程：

    获取型：布局有链式编程
    设置型：具有链式编程
