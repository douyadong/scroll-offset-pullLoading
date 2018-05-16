# 关于jquery的scroll()、scrollTop()和offset()方法理解以及下拉加载以及e.clientX,e.pageX,e.offsetX,e.screenX;

## scroll()
```
$(window/元素).scroll(fuction(){
    console.log('发生滚动，事件执行执行')
})
```
## scrollTop()
```
$(widow).height()表示浏览器窗口的高度;
$(document).height()表示文档(页面)的高度;
$(window).scrollTop()表示页面(不是浏览器窗口)滚动高度，但是所有浏览器都支持，因此在获取页面滚动高度时建议使用window;
$(document).scrollTop()同样表示页面滚动高度;
**scrollLeft()有相似效果**
```
## offset()
```
该方法设置或返回备选元素相对于文档的偏移坐标，以该元素的左上角和文档左上角为基点;
$(selector).offset({top:1,left:2})设置位置;
$(selector).offset().top;获取该元素在文档中的位置;
```
## 下拉加载数据
```
($(window).height()+$(window).scrollTop())>($(最后一个标签).height()+$(最后一个标签).offset().top-0(也可减其他值，表示未拉到底时即可加载));
设置一个外部变量，用来判断是否还需要发送请求加载数据列表;
var continuePullLoad=true;
$(selector).scroll(function(){
    if((($(window).height()+$(window).scrollTop())>($(最后一个标签).height()+$(最后一个标签).offset().top-0(也可减其他值，表示未拉倒底时即可加载)))&& continuePullLoad){
        continuePullLoad=false;//必须在发送一次请求成功之后，才能再次发送请求;
        $.ajax({
            success:function(){
                if(加载数据完毕){
                    $(selector).off("scroll")//关闭滚动式触发的事件
                }else{
                    未加载全部数据数据continuePullLoad=true;可以再次发送请求;
                }
            }
        })
    }
})
```
## 点击元素获取位置信息
1. [e.clientX,e.pageX,e.offsetX,e.screenX](https://www.cnblogs.com/jiangxiaobo/p/6593584.html) https://www.cnblogs.com/jiangxiaobo/p/6593584.html