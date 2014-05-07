# Toolbar Management Checklist

#### Before you begin coding:

* If you have image-based toolbar items, find or create the images (in the proper size and aspect ratio) and add them to your project as a resource.

* If you have view-based toolbar items, create each view in Interface Builder, specify an outlet for a custom controller object, and connect the view to the outlet.

* If the view is an off-the-shelf palette object, just make an outlet connection.

* Specify or (for default toolbar items) identify the unique string identifiers that you intend to use for toolbars and toolbar items.

* Add to an application menu (usually named View) the menu items Show Toolbar and Customize Toolbar..., connect these to the First Responder icon in the nib file window, and select the actions *toggleToolbarShown:* and *runToolbarCustomizationPalette:*. (Note that NSWindow automatically changes *“Show Toolbar”* to *“Hide Toolbar”* as appropriate.)

For further information, see [ "Adding and Removing Toolbar Items" ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ ).”

```
Note: You can create a toolbar in Interface Builder as described in [ “Creating a Toolbar in Interface Builder.” ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Articles/ToolbarInIB.html#//apple_ref/doc/uid/TP40008136-SW1 ) The toolbar can have a default set and allowed set of toolbar items. If you use Interface Builder for this purpose, you may ignore many of the programmatic steps described below. At runtime, you can combine toolbars and toolbar items unarchived from a nib file and those created programmatically.
```

# 工具栏管理清单

**在你编写代码之前：**

* 如果你有*基于图像*的工具栏项，查找或者创建需要用到的图像（用适当的尺寸和纵横比）并且将它们作为资源文件添加到你的项目中。

* 如果你有*基于视图*的工具栏项，则在Interface Builder中逐一创建视图，为定制的控制器对象指定outlet，然后将视图连接到outlet上。

* 如果视图是现成的调板对象，只需要连接到outlet上即可。

* 指定或（对于默认的工具栏项）确定你打算用于工具栏和工具栏项中的唯一的字符串标识符。

* 添加一个应用程序菜单（通常叫做`视图`)和显示`显示工具栏`及`定制工具栏...`的菜单项，将它们连接到nib文件窗口中的*First Responder*图标，并且选择与*toggleToolbarShown:*和*runToolbarCustomizationPalette:*两个动作进行连接。（注意NSWindow会根据情况自动将*Show Toolbar*改变成*Hide Toolbar*）。

了解进一步的信息，参阅：[ “Adding and Removing Toolbar Items” ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ )”。

```
注意：你可以像[ “Creating a Toolbar in Interface Builder.” ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Articles/ToolbarInIB.html#//apple_ref/doc/uid/TP40008136-SW1 )中描述的在Interface Builder中创建一个工具栏。工具栏可以有一个默认的项集合以及一个当前允许的项集合。如果你是为此目的使用Interface Builder，你可以忽略下面描述的很多编程步骤。在运行时，你可以将从*nib文件解归档的工具栏和项*与*那些以编程方式创建的工具栏和项* 组合使用。
```

**What happens:** The application launches or a document is created or opened, causing a nib file to be loaded and its object unarchived.

* A custom controller class in awakeFromNib or, for document-based applications, an NSDocument subclass in windowControllerDidLoadNib: completes the following steps for each toolbar it uses:
    1. It makes a new NSToolbar object using initWithIdentifier:.
    2. It sets attributes of the toolbar if the defaults won’t do using setAllowsUserCustomization:, setAutosavesConfiguration:, and
    setDisplayMode:.
    3. It sets the toolbar’s delegate (usually itself).
    4. It associates the toolbar with a window by sending the NSWindow object a setToolbar: message.
    
For further information see “Adding and Removing Toolbar Items”





