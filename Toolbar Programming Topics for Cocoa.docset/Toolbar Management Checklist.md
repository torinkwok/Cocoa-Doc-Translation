# Toolbar Management Checklist

#### Before you begin coding:

* If you have image-based toolbar items, find or create the images (in the proper size and aspect ratio) and add them to your project as a resource.

* If you have view-based toolbar items, create each view in Interface Builder, specify an outlet for a custom controller object, and connect the view to the outlet.

* If the view is an off-the-shelf palette object, just make an outlet connection.

* Specify or (for default toolbar items) identify the unique string identifiers that you intend to use for toolbars and toolbar items.

* Add to an application menu (usually named View) the menu items Show Toolbar and Customize Toolbar..., connect these to the First Responder icon in the nib file window, and select the actions *toggleToolbarShown:* and *runToolbarCustomizationPalette:*. (Note that NSWindow automatically changes *“Show Toolbar”* to *“Hide Toolbar”* as appropriate.)

For further information, see [ "Adding and Removing Toolbar Items" ](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ).”

```
Note: You can create a toolbar in Interface Builder as described in "Creating a Toolbar in Interface Builder". The toolbar can have a default set and allowed set of toolbar items. If you use Interface Builder for this purpose, you may ignore many of the programmatic steps described below. At runtime, you can combine toolbars and toolbar items unarchived from a nib file and those created programmatically.
```

# 工具栏管理清单

**在你编写代码之前：**

* 如果你有*基于图像*的工具栏项，查找或者创建需要用到的图像（用适当的尺寸和纵横比）并且将它们作为资源文件添加到你的项目中。

* 如果你有*基于视图*的工具栏项，则在Interface Builder中逐一创建视图，为定制的控制器对象指定outlet，然后将视图连接到outlet上。

* 如果视图是现成的调板对象，只需要连接到outlet上即可。

* 指定或（对于默认的工具栏项）确定你打算用于工具栏和工具栏项中的唯一的字符串标识符。

* 添加一个应用程序菜单（通常叫做`视图`)和显示`显示工具栏`及`定制工具栏...`的菜单项，将它们连接到nib文件窗口中的*First Responder*图标，并且选择与*toggleToolbarShown:*和*runToolbarCustomizationPalette:*两个动作进行连接。（注意NSWindow会根据情况自动将*Show Toolbar*改变成*Hide Toolbar*）。

了解进一步的信息，参阅：[“Adding and Removing Toolbar Items”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ)”。

```
注意：你可以像“Creating a Toolbar in Interface Builder.”中描述的在Interface Builder中创建一个工具栏。工具栏可以有一个默认的项集合以及一个当前允许的项集合。如果你是为此目的使用Interface Builder，你可以忽略下面描述的很多编程步骤。在运行时，你可以将从*nib文件解归档的工具栏和项*与*那些以编程方式创建的工具栏和项* 组合使用。
```

-----------

**What happens:** The application launches or a document is created or opened, causing a nib file to be loaded and its object unarchived.

* A custom controller class in *awakeFromNib* or, for document-based applications, an NSDocument subclass in *windowControllerDidLoadNib:* completes the following steps for each toolbar it uses:
    1. It makes a new NSToolbar object using *initWithIdentifier:*.
    2. It sets attributes of the toolbar if the defaults won’t do using *setAllowsUserCustomization:*, *setAutosavesConfiguration:*, and
    *setDisplayMode:*.
    3. It sets the toolbar’s delegate (usually itself).
    4. It associates the toolbar with a window by sending the NSWindow object a *setToolbar:* message.
    
For further information see [“Adding and Removing Toolbar Items” ](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ)

**What happens:** 在应用程序启动，或者创建或打开一个文档时，会引起nib文件被加载并且nib文件中的对象被解归档。

* 一个定制的控制器会在*awakeFromNib*中，而对于一个基于文档的应用中的NSDocument子类来说会在*windowControllerDidLoadNib:*中，为它所使用的每个工具栏完成如下的步骤：
    1. 使用*initWithIdentifier:*方法创建一个新的NSToolbar实例。
    2. 使用*setAllowsUserCustomization:*，*setAutosavesConfiguration:*以及*setDisplayMode:*来更改工具栏被创建时默认的属性。
    3. 设置工具栏实例的委托（通常是该对象本身）
    4. 通过给NSWindow对象发送*setToolbar:*消息来将创建好的工具栏与一个NSWindow相关联。
    
更多进一步的信息请参阅[“Adding and Removing Toolbar Items”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ)

-----------

**What happens:** The NSToolbar object begins communicating with its delegate in order to populate the toolbar with toolbar items.

1. The window gets the allowed and default toolbar item identifiers:
    * The toolbar object calls the delegate method *toolbarAllowedItemIdentifiers:* to get the total set of possible toolbar items.
    
    * Unless it finds the default toolbar configuration in user preferences, the toolbar calls the delegate method *toolbarDefaultItemIdentifiers:* to get the default set.
    To have the default configuration saved to and read from user preferences, the NSToolbar object’s *autosavesConfiguration* attribute must be set.

    * If certain toolbar items should indicate a selected state, the delegate should implement *toolbarSelectableItemIdentifiers:* to return the identifiers of those toolbar items.
    
2. The window asks for each NSToolbarItem object (by identifier) to insert into the toolbar.

    * To add each toolbar item to the toolbar, the NSToolbar object sends *toolbar:itemForItemIdentifier:willBeInsertedIntoToolbar:* to the delegate.
    
    If the NSToolbarItem object is image-based, get the image from the application bundle (for example, by using the NSImage class method *imageNamed:*) and send
    *setImage:* to the toolbar item. Also set the toolbar item’s label, palette label, target, and action. You may also set a menu form representation.
    
    If the toolbar item is view-based, send *setView:* to the toolbar-item object, passing in the outlet to the view. Also set the toolbar item’s label, palette label,
    its minimum size (minSize), and its maximum size (maxSize). (If you do not set a minSize and maxSize, the view does not appear because it is sized to zero in both
    dimensions.) You may also set a menu form representation.

    * If the delegate wants to customize a toolbar item before it is added, it can also implement the *toolbarWillAddItem:* notification method.

For further information see [“Adding and Removing Toolbar Items,”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ ) [“Setting a Toolbar Item’s Representation,”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemRep.html#//apple_ref/doc/uid/20000722-BBCGFFHE) [“Setting a Toolbar Item’s Size”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemSize.html#//apple_ref/doc/uid/20000754-BAJEFGAB) and [“Setting a Toolbar Item’s Size.”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemSize.html#//apple_ref/doc/uid/20000754-BAJEFGAB)

**What happens:** NSToolbar对象为了使用工具栏项填充工具栏，会开始与它的委托对象进行通信。

1. 窗口获取当前允许的和默认的工具栏项的标识符：
    * 工具栏对象调用委托方法*toolbarAllowedItemIdentifiers:*来获得当前全部可用的工具栏项。
    
    * 如果没有在用户偏好中找到工具栏的默认配置，那么工具栏对象可以调用委托方法*toolbarDefaultItemIdentifiers:*去获取默认的工具栏项集合。
    
    想要存储默认配置到用户偏好中或者从用户偏好中读取默认配置，必须设置工具栏对象的*autosavesConfiguration*属性。
    
    * 如果一个工具栏项要表明选中状态，委托应该实现*toolbarSelectableItemIdentifiers:*方法去返回那些工具栏项的标识符。
    
2. 窗口会要求每个NSToolbarItem对象（通过标识符）插入到工具栏中。
    * 要将每个工具栏项添加到工具栏中，NSToolbar对象会给它的委托发送*toolbar:itemForItemIdentifier:willBeInsertedIntoToolbar:*消息。
    
    如果NSToolbarItem对象时基于图像的，会从application bundle获取图像（比如说使用NSImage的类方法*imageNamed:*）并给工具栏项发送*setImage:*消息。也可以设置工具栏项的标签（label），调板标签（palette label），目标（target）以及动作（action）。你还可以设置一个*菜单表现形式*。
    
    如果工具栏项是基于视图的，会给工具栏项对象发送*setView:*消息，并给视图传递一个outlet。也可以设置工具栏项的标签（label），调板标签（palette label），目标（target）以及动作（action）。你还可以设置一个*菜单表现形式*
    
    * 如果委托想要在一个工具栏项被添加到工具栏之前定制它，也可以实现*toolbarWillAddItem:*通知方法。

了解进一步的信息请参阅：[“Adding and Removing Toolbar Items,”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/AddRemoveToolbarItems.html#//apple_ref/doc/uid/20000755-BBCGJCDJ ) [“Setting a Toolbar Item’s Representation,”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemRep.html#//apple_ref/doc/uid/20000722-BBCGFFHE) [“Setting a Toolbar Item’s Size”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemSize.html#//apple_ref/doc/uid/20000754-BAJEFGAB)以及[“Setting a Toolbar Item’s Size.”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/SettingTBItemSize.html#//apple_ref/doc/uid/20000754-BAJEFGAB)    

--------------

**What happens:** Users click toolbar items; the runtime context of the application changes.

* Declare and implement action methods for each of your custom toolbar items, usually in a custom controller class.
When you create a toolbar item you can identify the selector of each of these methods through the *setAction:* method of NSToolbarItem. Also set the target by calling the *setTarget*:, usually passing in self.

* Validate toolbar items.
If the toolbar item is image-based, the target of an action should implement *validateToolbarItem:* if it wants validation more specialized than the default. If the toolbar item is view-based, you should create a subclass of NSToolbarItem for the item and override the *validate* method.

For further information, see [“Validating Toolbar Items.”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/ValidatingTBItems.html#//apple_ref/doc/uid/20000753-BAJGFHDD)


**What happens:** 用户点击工具栏项时；app的运行时环境改变时。

* 为你的每个工具栏项声明并实现action，通常是在一个定制的控制器类中做这些工作。
当你创建一个工具栏项时，可以通过NSToolbarItem的*setAction:*方法对这些方法的selector进行标记。也可以通过调用*setTarget*方法来设置目标（target），通常将控制器自身作为*setTarget*方法的参数传入。

* 验证工具栏项。
如果工具栏项时基于图像的，且如果想要比默认的验证更有针对性，则其action的目标应该实现*validateToolbarItem:*方法。如果工具栏项时基于视图的，你应该为该项创建NSToolbarItem的子类，并且重写其*validate*方法。

进一步的信息请参阅：[“Validating Toolbar Items.”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/ValidatingTBItems.html#//apple_ref/doc/uid/20000753-BAJGFHDD)

---------------













