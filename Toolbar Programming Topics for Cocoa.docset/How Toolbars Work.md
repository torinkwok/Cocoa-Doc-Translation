# How Toolbars Work

NSToolbar and NSToolbarItem classes provide you with a standard way to display a toolbar for a titled window below its title bar. These classes also provide users with a standard way to customize toolbars and save those customizations. This is what a toolbar looks like:

# 工具栏如何工作

NSToolbar和NSToolbar两个类为你提供了在标题窗口的标题栏下方显示工具栏的标准途径。这些类也为用户提供了定制工具栏和保存那些定制的标准途径。下面展示了工具栏看上去是什么样子的：
![ Example toolbar ]( http://cl.ly/image/1y2b0K3O0G2r/Screen%20Shot%202014-05-06%20at%2018.13.56.png ).



To create a toolbar, you must create a delegate that provides important information:

* A list of default toolbar identifiers. This list is used when reverting to default, and constructing the initial toolbar.
The default set of toolbar items can also be specified using toolbar items found in the Interface Builder library.

* A list of allowed item identifiers. The allowed item list is used to construct the customization palette, if the toolbar is customizable.

* The toolbar item for a given item identifier.

When you create an NSToolbar, you give it an identifier. NSToolbar assumes all toolbars with the same identifier are the same, and automatically synchronizes changes. For instance, take a mail application. Your application’s compose windows’ toolbars would have the same identifier string. So, when you re-order items in one toolbar, the changes automatically propagate to any other compose windows currently open.

Most toolbars will contain simple clickable items that act like buttons. The simplest toolbar item is defined by its icon, label, palette label (used in the customize sheet), target, action, and tooltip. Most toolbars can be represented using these simple items. If you need something more complex in your toolbar, call setView: on a toolbar item to provide a custom view. For example, you could create a toolbar item that contains a pop-up menu or a text field and button.

```
Note: In OS X v10.4 and earlier versions of the operating system, only toolbar items that are pop-up buttons can have key equivalents. In OS X v10.5 and later, all visible controls in a toolbar can have key equivalents.
```

要创建一个工具栏，你必须创建一个提供重要信息的委托：

* 一个默认的工具栏ID列表。这个列表通常在重置工具栏到默认状态和初始化工具栏时使用。

* 一个被允许的工具栏项ID列表。被允许的工具栏项列表通常用于在工具栏是可定制的时创建定制调板。

* 给定项的工具栏的ID

当你创建一个NSToolbar时，会赋给它一个标识符。NSToolbar假设所有具有相同标识符的工具栏都是相同的，并且会自动同步更改。例如，Mail.app。你的app的众多组合窗口的工具栏将会拥有相同的标识符字符串。所以，当你重新排列一个工具栏中的项时，改变会自动传播给任何当前打开的其他组合窗口。

大多数工具栏会包含简单的可点击的并且动作像一个button的项。最简单的工具栏项是通过它的图标（icon），标签（label），调板标签（palette label，在定制sheet窗口中使用），目标（target），动作（action）以及工具提示（tooltip）。大多数工具栏可以使用这些简单的项被展示出来。如果你需要在你的工具栏中有一些更复杂的东西，在一个工具栏项上调用*setView:*方法以提供定制视图。比如说你可以创建一个包含一个弹出式菜单或文本域以及一个button的工具栏。

```
注意：在OS X 10.4以及更早版本的操作系统中，只有弹出式按钮项可以有一个快捷键。在OS X 10.5和之后的版本中，所有在工具栏中可见的NSControl子类对象都可以拥有快捷键。
```



There are a couple of standard toolbar item identifiers that NSToolbar knows about. **NSToolbarSeparatorItemIdentifier** is the standard vertical line separator. **NSToolbarSpaceItemIdentifier** is a fixed width space. **NSToolbarFlexibleSpaceItemIdentifier** is a variable width space. Additionally, there are **NSToolbarShowColorsItemIdentifier**, **NSToolbarShowFontsItemIdentifier**, **NSToolbarPrintItemIdentifier**, and **NSToolbarCustomizeToolbarItemIdentifier**. These items are accessible only by identifier.

If you need to change the action sent by a standard item, write a toolbarWillAddItem: notification method.

When a user customizes the toolbar of an application’s window, that customization is saved as a user preference. The customized toolbar is used thereafter when the application launches in place of the default set of toolbar items specified by the developer.


有几个NSToolbar知道的标准工具栏项标识符。**NSToolbarSeparatorItemIdentifier**是标准的垂直分割线。 **NSToolbarSpaceItemIdentifier**是一个固定的宽度空间。**NSToolbarFlexibleSpaceItemIdentifier** 是一个可变的宽度空间。此外，还有**NSToolbarShowColorsItemIdentifier**, **NSToolbarShowFontsItemIdentifier**, **NSToolbarPrintItemIdentifier**, 以及**NSToolbarCustomizeToolbarItemIdentifier**。这些项只能通过标识符才能使用。

如果你需要更改标准项所发送的动作，可以编写一个*toolbarWillAddItem:*通知方法。

当一个用户定制一个app的窗口中的工具栏时，定制信息会被保存在一个用户偏好中。定制过的工具栏会被使用，之后当app再启动时，定制好的工具栏项会替代app开发者指定的默认的项集合。





