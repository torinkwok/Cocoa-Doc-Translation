# Creating a Toolbar in Interface Builder

Beginning with OS X v10.5 (Leopard), you can create a toolbar in Interface Builder. You can do almost anything with toolbars in Interface Builder that you can do programmatically. At runtime, you may combine toolbars and toolbar items that are unarchived from a nib file and those that are programmatically created.

# 在Interface Builder中创建工具栏

从OS X 10.5（Leopard）开始，你可以在Interface Builder中创建工具栏。你可以在Interface Builder中用工具栏做任何你能以编程方式做的事情。在运行时，你可以将那些从nib文件中解归档的工具栏和工具栏项，与那些以编程的方式在代码中创建的组合在一起使用。



## Adding a Toolbar to a Window

Open your application’s nib file and search the Interface Builder library for “toolbar”. A toolbar object and a number of toolbar items are listed in the library.

## 添加工具栏到窗口

打开你的应用程序的nib文件，并且在Interface Builder库中中搜索“toolbar”。一个工具栏对象和若干个工具栏项都会被列在库中。

![ Figure1 ](http://i.imgbox.com/a4OufytQ.png)

Drag the toolbar object onto a window. Interface Builder automatically positions it below the window bar and above the window’s content view. It displays the "default” default set of toolbar items.

将工具栏对象拖拽到一个窗口上。Interface Builder会自动将其定位到窗口标题栏之下及窗口内容视图（content view）之上。它会显示“default”默认的工具栏项集合。

![ Figure 2 ](http://i.imgbox.com/Mml1ZhrG.jpg)

Select the toolbar (if it isn’t already selected) and display the Attributes pane for the toolbar in the inspector (Command-1). Set the desired attributes of the toolbar; make sure Customizable is selected if you want users to add items from the allowed set.

选中工具栏（如果还没有被选中）并且在检视器中显示工具栏的属性面板（Command-1）。设置期望的工具栏属性；如果你想让用户从允许的工具栏项集合中添加项，那就要确保Customizable复选框被选中。

![ Figure 3 ](http://i.imgbox.com/cebRI8mg.png)

Note that the Attributes pane for toolbars does not include a field for the toolbar identifier. Remember that the purpose of the identifier is to differentiate toolbars assigned to different kind of windows, for example, between the toolbars for document windows and the toolbar for a utility window. Because you would store these different toolbars in different nib files, there is little need for toolbar identifiers.

注意工具栏的属性面板中没有包含用来设置工具栏标识符的文本域（译注：文档中的demo使用的是老版本的Xcode，而在Xcode 5.x中，工具栏的属性检视器中包含设置标识符的文本域。如上图所示，该截图是译者使用的新版的Xcode 5的截图）。回想一下，标识符的目的是用于区分被赋给不同类型窗口的工具栏，比如说在文档窗口的工具栏和工具窗口的工具栏之间进行区分。因为你将会在不同的nib文件中存储这些不同的工具栏，所以在这里基本上不会需要工具栏标识符。

# Adding and Configuring Toolbar Items

Next you add and possibly remove toolbar items to both the allowed set of items and the default set. A toolbar item can be one of the standard ones (for example, Colors) or can be a custom toolbar item. Start by clicking the toolbar if it is already selected or double-clicking it if it is not selected. This displays a view containing the allowed toolbar items.

# 添加并配置工具栏项

接下来向允许的工具栏项集合和默认集合中添加并且可能从它们中移除项。一个工具栏项可以是标准工具栏项中的某一个（比如说`颜色`项），或者可以是一个定制的工具栏项。如果已经选中了工具栏那么单击其开始，如果还未选中工具栏，那么从双击其开始。这会显示出一个视图包含允许的工具栏项：

![ Figure 4](http://i.imgbox.com/PCbGIocq.jpg)








