# Subclassing NSToolbarItem

To provide enabling behavior or to modify click-through behavior on a view item, you must override *validate* and may want to override *isEnabled* and *setEnabled:*.

To enable multiple copies of the item in the toolbar, you must override *allowsDuplicatesInToolbar* to return YES.

Your subclass must conform to the NSCopying protocol.

# 子类化NSToolbarItem

要再一个视图项上提供启用行为或者修改点击行为，你必须重写*validate*方法，并且又是可能还需要重写*isEnabled*和*setEnabled:*方法。

要想允许在一个工具栏中能够存在某一个项的多个副本，你必须重写*allowsDuplicateInToolbar*方法来返回YES。

你的子类必须遵循NSCopying协议。