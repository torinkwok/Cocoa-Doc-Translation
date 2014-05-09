# Validating Toolbar Items

The toolbar validates every visible image item and every invisible item’s overflow menu item.

By default toolbar items have click-through behavior, which is to say that toolbar items remain enabled and clickable when the user switches to another window or even another application. To change this behavior for a toolbar item, your validation code needs to take the larger environment into account. See *Aqua Human Interface Guidelines* for more information on click-through behavior.


# 验证工具栏项

工具栏会验证每一个可视的图像项，以及每一个不可视的项的溢出菜单项。

默认情况下工具栏项拥有点击行为，其告知工具栏项当用户切换到另一个窗口甚至是另一个app时仍保持可用和可点击。要更改工具栏项的这一行为的话，你的验证代码需要考虑更大范围的环境。参阅*Aqua Human Interface Guidelines*以了解共多关于*点击行为*的信息。


## Image item validation

The toolbar automatically takes care of darkening an image item when it is clicked and fading it when it is disabled. All your code has to do is validate the item. If an image item has a valid target/action pair, then the toolbar will call NSToolbarItemValidation’s validateToolbarItem: on target if the target implements it; otherwise the item is enabled by default.

In the absence of a custom menu form representation, NSToolbar validates an image item’s overflow menu in the same way that it validates the toolbar item in the toolbar.

## 图像项的验证

