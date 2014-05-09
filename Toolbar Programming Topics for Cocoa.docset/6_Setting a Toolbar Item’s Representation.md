# Setting a Toolbar Item’s Representation

The *label* attribute of a toolbar item is displayed as the text for the toolbar item when the toolbar is in Icon & Text Mode or Text Only Mode. By default, the label is also used in the overflow menu as the title of the menu item representing the toolbar item. The *paletteLabel* attribute of an item is used instead of *label* in the customization palette. (If *paletteLabel* is not set, the customization palette does not use *label* by default.)

Clicking on the label of an image item in Text Only Mode or selecting an image item’s overflow menu item simply invokes the image item’s action.

View items, on the other hand are more complex and can’t usually be handled so simply. Primarily to give view items more flexibility, NSToolbarItem provides a *menuFormRepresentation* attribute.

Every toolbar item has a menu form representation, which is a menu item. The toolbar provides an initial default menu form representation that uses the toolbar item’s label as the menu item’s title. The application can provide a custom menu form representation which can have a submenu and which can have a title different from the toolbar item’s label. If a toolbar item’s custom menu form representation has a submenu, then the toolbar drops down that submenu under the toolbar item in Text Only Mode and displays the submenu in the overflow menu.

If a view item’s menu form representation attribute has not been set, NSToolbar disables the overflow menu item as well as the toolbar item’s text in Text Only Mode. If the attribute has been set and the menu form representation has a submenu, NSToolbar enables the overflow menu item as well as the toolbar item’s text in Text Only Mode. If the attribute has been set and the menu form representation does not have a submenu, the toolbar validates the menu item to determine whether to enable the toolbar item’s text in Text Only Mode and the toolbar item’s overflow menu item. For more detail on how the validation works, see [“Validating Toolbar Items.”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/ValidatingTBItems.html#//apple_ref/doc/uid/20000753-BAJGFHDD)

Image items as well as view items can use a simple *menuFormRepresentation* without a submenu merely for the purpose of replacing *label* as the title of the toolbar item’s overflow menu item. The only situation in which you should use this feature is when the *label* is empty.

# 设置工具栏项的展示形式

当工具栏在Icon & Text或者Text Only模式中时，工具栏项的*label*属性被显示为工具栏项的文本。默认情况下，标签也被以展现工具栏项的菜单项标题的形式用在溢出菜单中。在定制调板中使用*paletteLabel*而非*label*（如果*paletteLabel*没有被设置，定制调板在默认情况下也不会使用*label*）。

在Text Only模式下点击图像项的标签或者选中图像项的溢出彩蛋项时，只会简单地调用图像项的action方法。

另一方面对于视图项来说会更复杂一点，并且无法像通常那样进行简单地处理。主要是为了给视图项更多的灵活性，NSToolbarItem提供了一个*menuFormRepresentation*属性。

每个工具栏项都有一个本质上是一个菜单项的菜单展示形式。工具栏提供一个初始的默认菜单展示形式，其使用工具栏项的的标签作为其菜单项的标题的。应用程序可以提供定制的菜单展示形式，其可拥有子菜单并且可以拥有与工具栏项的标签不同的标题（译注：默认的menu form representation的菜单项标题与工具栏项的标签相同，定制的可以不同）。如果一个工具栏项的定制菜单表现形式拥有一个子菜单，那么在Text Only模式下工具栏可以在工具栏项下方下拉出该子菜单，并且可以在溢出菜单中显示这个子菜单。

如果视图项的*菜单表现形式*属性没有被设置，NSToolbar在Text Only模式下会禁用溢出菜单项和工具栏项的文本。如果该属性被设置并且菜单表示形式拥有一个子菜单，那么在Text Only模式下NSToolbar会使溢出菜单项和工具栏项的文本可用。如果该属性被设置但是菜单表示形式没有子菜单，那么工具栏会验证菜单项以决定工具栏项的文本在Text Only模式和工具栏项溢出菜单中是否可用。更多关于如何进行验证工作的细节，参阅[“Validating Toolbar Items。”](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/Toolbars/Tasks/ValidatingTBItems.html#//apple_ref/doc/uid/20000753-BAJGFHDD)

图像项和视图项都可以仅仅使用简单的*menuFormRepresentation*方法而不用子菜单，来达到以工具栏项的溢出菜单项的标题来替换*label*的目的。只有当*label*为空时，你才应该使用该特性。




