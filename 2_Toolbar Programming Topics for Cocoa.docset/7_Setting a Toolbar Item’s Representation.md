# Validating Toolbar Items

The toolbar validates every visible image item and every invisible item’s overflow menu item.

By default toolbar items have click-through behavior, which is to say that toolbar items remain enabled and clickable when the user switches to another window or even another application. To change this behavior for a toolbar item, your validation code needs to take the larger environment into account. See *Aqua Human Interface Guidelines* for more information on click-through behavior.


# 验证工具栏项
 
工具栏会验证每一个可视的图像项和每一个不可视的项的溢出菜单项。

默认情况下工具栏项拥有点击行为，其在用户切换到另一个窗口甚至是另一个应用程序时，告知工具栏项保持可用并可被点击。要改变工具栏项的默认行为，你的验证代码需要考虑更大范围的环境。参阅*Aqua Human Interface Guidelines*以了解更多关于点击行为的信息


## Image item validation

The toolbar automatically takes care of darkening an image item when it is clicked and fading it when it is disabled. All your code has to do is validate the item. If an image item has a valid target/action pair, then the toolbar will call NSToolbarItemValidation’s *validateToolbarItem:* on target if the target implements it; otherwise the item is enabled by default.

In the absence of a custom menu form representation, NSToolbar validates an image item’s overflow menu in the same way that it validates the toolbar item in the toolbar.


## 图像项的验证

当一个图像项被点击时工具栏会自动处理其变暗操作，并且当一个图像项被禁用时，工具栏也会自动为其做褪色处理。你的代码需要去验证项。如果一个图像项拥有一个有效的目标(target)/动作(action)对，并且目标实现了NSToolbarItemValidation非正式协议的*validateToolbarItem:*方法的话，工具栏就会调用该协议方法；否则项默认为可用的。

当缺少菜单表示形式时，NSToolbar会使用与验证工具栏项的同样方法，去验证一个图像项的溢出菜单。

## View item validation

Validation for view items is not automatic because a view item can be of unknown complexity. To implement validation for a view item, you must subclass NSToolbarItem and override *validate* (because NSToolbarItem’s implementation of *validate* does nothing for view items). In your override method, do the validation specific to the behavior of the view item and then enable or disable whatever you want in the contents of the view accordingly. If the view is an NSControl you can call *setEnabled:*, which will in turn call *setEnabled:* on the control.

In the absence of a custom menu form representation, NSToolbar by default disables a view item’s overflow menu item.

## 视图项的验证
验证视图项并不是自动进行的，因为一个视图项可能是未知复杂性的。要实现视图项的验证，你必须子类化NSToolbarItem并重写*validate*方法（因为NSToolbarItem的*validate*方法实现不会为视图项做任何事情）。在你重写的方法中，进行与特定视图项行为相关的验证工作，以及在相应的视图的内容中启用或者禁用任何东西。如果视图是一个NSControl，那么你可以调用*setEnabled*方法，该方法会依次在control上调用*setEnabled*方法。

当缺少菜单表示形式时，NSToolbar会缺省禁用视图项的溢出菜单项。

## Overflow menu item validation

If a toolbar item has a custom menu form representation with no submenu, then the toolbar will validate the overflow menu item and the toolbar item’s text in Text Only Mode differently than it would with the default menu form representation: If the menu form representation menu item’s target implements *validateMenuItem:* (part of NSMenuValidation), the toolbar calls that method to validate both the overflow menu item and the toolbar item’s text in Text Only Mode.

## 溢出菜单项的验证

如果一个工具栏项拥有一个不带子菜单的定制菜单展示形式，***then the toolbar will validate the overflow menu item and the toolbar item’s text in Text Only Mode differently than it would with the default menu form representation:（这一句求翻译）***。如果菜单展示形式的菜单项的目标（target）实现了NSMenuValidation非正式协议中的*validateMenuItem:*方法，那么工具栏在Text Only模式下就会调用该协议方法去验证溢出菜单项和工具栏项的文本。






