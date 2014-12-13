coordinate
==========

screen, page与client坐标的区别，鼠标右键的使用，窗口卸载时的事件的使用

clientX与clientY是相对于浏览器的可视窗口，即能展示内容的窗口的左上角为参考点；
pageX与pageY是相对于我们的文档的左上角为参考点的，即代码中document的左上角，产生滚动条后技能看到效果；
screenX与screenY是以我们显示器的的左上角为参考点。

![image](https://github.com/wenzi0github/coordinate/blob/master/images/1.png)

通常我们鼠标右键时产生的是浏览器默认的右键菜单，我们可以通过 contextmenu 来书写我们自己的右键菜单；
当然，首先我们应该取消右键的默认行为，然后开始我们的菜单。

```javascript
$("body").bind("contextmenu", function(event){
	event = event || window.event;
	// 取消默认的右键行为
	if (event.preventDefault) {
        event.preventDefault();
    }else{ 
        event.returnValue = false;
    }
	
	var x = event.pageX;
	var y = event.pageY;
	
	$("#menu").css({"display":"block", "top":y, "left":x});
})
//单击左键使菜单消失
$("body").bind("click", function(event){		
	$("#menu").css("display","none");
});
```

有时候用户在使用当前页编辑一些内容，或者其他一些重要的操作，需要在用户在关闭浏览器或者刷新浏览器时给用户以提示，防止当前重要的内容丢失，那么我们就可以用 beforeunload 来绑定浏览器卸载事件，这个事件是在浏览器窗口关闭或者刷新前调用的。
```javascript
//关闭页面或者重新加载页面时执行的弹框提示，弹框内容为msg
$(window).bind("beforeunload", function(event){
	event = event || window.event;
    var msg = "leave";
	event.returnValue = msg;
	return msg;
});
```

