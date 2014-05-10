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
