
# 设计思路

构造函数 DragBox

```
	属性：	ele
			isdraged  是否被拖拽
			dragbox   拖拽的对象
		drop    鼠标释放时自动调用的处理函数
	方法：
		setlisten	设置放下监听
		unsetlisten	取消放下监听

```


# 遇到的问题及解决方法

## 如何取消父元素的 drop 监听函数，并给新建的子元素添加 drop 函数

```
// 绑定监听函数，监听函数为对象自己的drop函数
$(document).bind("mouseup", this, this.drop);

// 取消自己的鼠标释放监听函数
$(document).unbind("mouseup", this.drop);
```

## 如何判读释放的是哪个元素？

尝试1： 给单独元素添加 onmouseup 事件监听函数

	这样不行，因为释放鼠标时，盛放元素的盒子是不能捕获 鼠标抬起到事件。

【解决方法】 
```
// 绑定监听函数，监听函数为对象自己的drop函数
$(document).bind("mouseup", this, this.drop);

```

jQuery 中 bind 是可以多个函数一起调用的。然后，通过bind的调用顺序是由绑定顺序来决定，后面绑定的先调用。

在创建的DOM元素对象中添加属性 isdraged 来区分，是哪个元素当前正在被拖拽：

```
// 是否被拖拽
this.ele.isdraged = false;
// 备份当前对象
this.ele.dragbox = this;
```

# 还需完善的工作

1. 小窗口可以关闭，关闭后复原
	初步思路： 在小窗口中添加关闭按钮，及关闭的事件处理函数

2. 不止竖着添加，也可以横竖添加
	初步思路： 在拖拽的对象中添加标记，下次采用哪种方式来添加


	