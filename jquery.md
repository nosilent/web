jquery

文件入口

    $( document ).ready(function() {
       //代码
    })
    //$是jquery的简写形式
    //只有在页面文档对象模型(DOM)准备好,代码才会运行
    //简写
    $(function(){
        //代码
    })

$冲突

通过使用jQuery.noConflict()将其赋值给一个变量来代替$，或以参数的形式。

- 赋值

    var $j = jQuery.noConflict();//返回对jQuery函数的引用

- 立即调用函数

    jQuery.noConflict();
    (function( $ ) {
     
    })( jQuery );

- 参数

    jQuery(document).ready(function( $ ) {
        
    });
    //或者
    jQuery(function($){
        
    });

元素操作

.attr()

.attr()可以接受一个键和一个值，或者一个包含一个或多个键/值对的对象。 

    //设置
    $( "a" ).attr({
        title: "all titles are the same too!",
        href: "somethingNew.html"
    });
    //获取
    $( "a" ).attr( "href" )





