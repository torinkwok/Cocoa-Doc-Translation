# Setting a Toolbar Item’s Size

When we speak of toolbar item size or toolbar height in this section, we’re referring to the image area or view area when the toolbar is displaying in Icon & Text or Icon Only Mode.

The displayed resolution of an image item is dependent on the *sizeMode* of the toolbar. You should provide image representations specific to the default, regular and small size modes in a single image that supports multiple image representations such as icns or tiff. The appropriate image representation is automatically displayed for the toolbar's current *sizeMode*. If an appropriate representation is not available, the toolbar scales the a representation to the appropriate size for the current mode, at a cost in performance and appearance. Images that are not square are scaled to fit. An image item’s image is also scaled down and used in the image item’s overflow menu item. For more information, see the section on toolbar icons in [““Icons””](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AppleHIGuidelines/IconsImages/IconsImages.html#//apple_ref/doc/uid/20000967-TP6) in [Aqua Human Interface Guidelines.](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AppleHIGuidelines/Intro/Intro.html#//apple_ref/doc/uid/20000957)

The *minSize* and *maxSize* toolbar item properties are for use only by view items. They must not be left unset (or the view will not display), and unless you are implementing intelligent stretching behavior in a view item, both the *minSize* and *maxSize* properties should equal the size of the item’s view. The toolbar takes care of providing space between toolbar items, so a view should be just big enough to enclose the frames of its content objects. It’s OK for a view item’s *minSize* height to be less than the usual 32 pixels (to work optimally with possible future toolbar enhancements).

> Note: As of OS X v10.5, if you call setView: on an NSToolbarItem object without also calling setMinSize: or setMaxSize:, the toolbar item sets its minimum and maximum size equal to the view’s frame.

# 设置工具栏项的尺寸

当我们在这部分中谈及到工具栏项的尺寸或者工具栏的高度时，我们指的是当工具栏在Icon & Text或者Icon Only模式下显示时的图像区域或视图区域。

图像项的显示分辨率依赖于工具栏的*sizeMode*(参见[ NSToolbar Class Reference ](https://developer.apple.com/library/mac/documentation/cocoa/reference/applicationkit/classes/NSToolbar_Class/Reference/Reference.html#//apple_ref/doc/uid/20000681-SW9)中的**Constants**部分）。你应该在诸如.icns或.tiff这类提供多个图像表示的单一图像中提供特定于默认（NSToolbarSizeModeDefault），矩形（NSToolbarSizeModeRegular）和小型尺寸（NSToolbarSizeModeSmall）模式的图像表示。适当的图像表示或根据工具栏的当前的*sizeMode*自动显示，如果一个适当的图像表示不可用，那么工具栏会自动将当前模式下的图像表示缩放到适当的尺寸。不是正方形的图像，会被缩放成正方形。图像项的图像也会按比例缩小并用在图像项的溢出菜单中。了解更多信息，参阅[Aqua Human Interface Guidelines](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AppleHIGuidelines/Intro/Intro.html#//apple_ref/doc/uid/20000957)中[““Icons””](https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AppleHIGuidelines/IconsImages/IconsImages.html#//apple_ref/doc/uid/20000967-TP6)的工具栏图标部分。

工具栏项的*minSize*和*maxSize*属性只能通过视图项被使用。它们绝对不能不设置（否则视图将不会显示），并且除非你正在一个视图项中实现智能拉伸行为，否则*minSize*和*maxSize*属性的值都应该等于项的视图的尺寸。工具栏会处理在两个项之间提供的空白，所以视图应该是大到足以装下它的内容对象的边框。视图项的*minSize*高度小于通常的32像素也是可以的(to work optimally with possible future toolbar enhancements)。

> 注意：自OS X 10.5起，如果在一个NSToolbarItem对象上调用setView:的同时，没有调用setMinSize:或者setMaxSize:方法，工具栏项会将它的最大和最小尺寸设置为与视图的边框（frame）相同。

The height of the toolbar is the height of the greatest minSize height of any item visible in the toolbar at the time. If a view item’s maxSize height is less than the height of the toolbar, then the toolbar centers the item’s view within the available vertical space. If a view item’s view does something intelligent when it is stretched, then you will set its maxSize greater than its minSize in height, width, or both. Horizontally-stretchable view items, including the Flexible Space standard item, compete equally for available horizontal space. An example of a view item that stretches horizontally is the “Search Mailbox” item in the Apple Mail application.

An example of a view item that stretches vertically is the Separator standard toolbar item. When we insert a tall RGB Color custom item into the toolbar, the Separator item adds more dots to itself, but the image item and the non-stretchable view item don’t change (the toolbar merely centers them vertically):







