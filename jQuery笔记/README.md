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

3.jq 转 dom 对象

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

    扩展几个选择器:
        $('div.goback') 选取div中的类名为goback的元素
        $("[href]")  选取带有 href 属性的元素
        $(":button") 可以选取所有 type="button" 的 <input> 元素 和 <button> 元素，如果去掉冒号，$("button")只能获取 <button> 元素

    关于 : 和 [] 这两个符号的理解
        ：可以理解为种类的意思，如：p:first，p 的种类为第一个。
        [] 很自然的可以理解为属性的意思，如：[href] 选取带有 href 属性的元素。

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

# jq 的动画方法:

第一组动画：

    hide() 隐藏
    show() 显示
    两者可以写参数 可以写数字类型  第二个参数代表回调函数
    数字类型1000表示1秒

第二组动画：

    slideUp上拉
    slideDown下拉
    参数同上

第三组动画：

    fadeIn 淡入
    fadeOut 淡出
    fadeToggle切换
    fadeTo(1000,.3)  渐变透明度到..1秒内渐变透明度到0.3
    .end() 结束当前的this 指回原来的this

自定义动画：

    animate：
        参数1：对象 ----运动的代码
        参数2：运动事件
        参数3：运动曲线
        参数4：动画执行完毕所要执行的代码

# jq 第二天：

## 属性的操作：

    prop：获取的是元素固有的属性  获取自定义属性结果是undefined
    attr：获取的是自定义属性 attr 可以获取自定义属性同时可以获取固有属性
    data:本质生成在缓存机制里面  不会修改原来的属性 只会临时存储；
    removeAttr()移除属性

## 内容的文本值：

    html() 获取空格 标签 文本内容  设置会解析标签  innerHTML
    text() 获取文本内容  设置不会解析标签  innerText

## jq 遍历元素的方式：

遍历 DOM 元素

    $("ele").each(function(索引,dom元素){
        执行函数
    })

遍历对象 数组：

    $.each(对象,function(index,ele){
        执行函数
    })

创建 添加 删除元素

    var li = $("<li>123</li>");

在当前内容的后面添加元素

    $("div").append(li);

添加到某个元素

    li.appendTo($("div"))

在当前内容的前面添加元素

    $("div").prepend(li)；

添加到当前内容的前面添加元素

    li.prependTo($("div"))

同级元素前面：

    $("div").before(li)

同级元素的后面

    $("div").after(li)

删除元素：

    $("div").remove()   移除本身
    父元素.empty()      移除子元素
    父元素.html("")     移除子元素
    注意：如果子元素有事件只是清除内容  事件还在内存；

## jq 里面的尺寸：

    width()  height()  只包含宽度高度
    innnerwidth()  innnerheight()  包含padding
    outerwidth()  outheight()包含padding+border
    outwidth(true) 包含padding  border  margin

## jq 里面的位置：

    offset()获取元素距离屏幕的距离 offset().top
    position()获取距离父元素有定位的距离
    scrollTop():获取页面卷曲出去的距离
    scrollLeft():获取页面卷曲出去的距离

# jq 第三天

## on 注册事件：

    1.事件委托
    2.动态创建的元素无法有事件  所以需要通过事件绑定 只要是通过动态创建出来的   元素 那么必须通过on绑定事件
    3.事件解绑   $("div").off()  解绑当前元素的所有事件   $("div").off(“click”)
    4.委托解除绑定   $("div").off("click","li");
    $("#btn1").click()
    $("#btn1").trigger("click")
    $("#btn1").triggerHandler("click")

## trigger 与 triggerHandler 区别：

    trigger：会触发事件冒泡  会触发浏览器的默认行为
    triggerHandler：不会触发事件冒泡  不会触发浏览器的默认行为;

## jq 阻止事件冒泡

    1.e.stopPropagation()
    2. return false;在jq里面可以阻止事件冒泡； 在dom不能阻止事件冒泡；

## 多库共存：

    1.var 变量 = jQuery.noConflict()   本质把$赋值给变量
    2.jQuery("div");
    extend() 对象与对象之间的拷贝
    浅拷贝：
        属性拷贝的是值  方法（对象拷贝的地址）
    深拷贝：
         属性拷贝的是值  方法（对象拷贝的值）
    $.extend(true, obj, target);
        参数1：深拷贝|浅拷贝
        参数2：拷贝的对象
        参数3：拷贝的目标对象
        对象里面有相同的属性（方法） 会把原来的覆盖掉
    $.fn---jq方法的顶级对象

懒加载：

    对于页面有很多静态资源，为了节省用户流量和提高页面性能，可以在用户浏览到当前资源的时候
    在对资源进行请求加载。
    原理：简单理解： 当访问一个页面的时候 先把img元素或其他元素的背景图片路径替换一张图片（这样只请求一次）
    只有当图片出现在可视区域内时，才设置真正的图片，让图片显示出来----懒加载
