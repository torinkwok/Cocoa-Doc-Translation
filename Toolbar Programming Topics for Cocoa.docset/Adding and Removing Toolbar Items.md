# Adding and Removing Toolbar Items

The delegate of an NSToolbar instance is responsible for providing the identifiers specifying the toolbar items that are allowed in a toolbar, as well as the default items visible in a new toolbar.

# 添加和移除工具栏项

NSToolbar实例的委托负责提供指定一组工具栏中可用项的标识符，也提供在一隔新的工具栏中默认要显示的一组项。



## Allowed and default toolbar items

The required delegate method *toolbarAllowedItemIdentifiers:* returns an array of identifiers specifying the toolbar items that can be displayed by the specified NSToolbar instance. By default, a new toolbar instance does not assume any items are allowed, not even the separator item.

The example implementation shown in Listing 1 configures the toolbar to allow a selection of the standard Cocoa toolbar items as well as two application specific toolbar items. The resulting toolbar is shown in Figure 1.


## 被允许的和默认的工具栏项

必要的委托方法*toolbarAllowedItemIdentifiers:* 返回一组标识符，用于指定可以通过制定工具栏实例被显示的项。默认情况下，一个工具栏实例不会假设任何项被允许，甚至连分隔器项也不会。

在Listing 1中展示的事例，配置工具栏以允许一组标准的Cocoa工具栏项，以及两个在特定应用程序中的工具栏项。工具栏的结果如Figure 1中所示：

**Listing 1**  *toolbarAllowedItemIdentifiers:*方法实现范例
```
- (NSArray *) toolbarAllowedItemIdentifiers: (NSToolbar *) toolbar {
    return [NSArray arrayWithObjects: SaveDocToolbarItemIdentifier,
        NSToolbarPrintItemIdentifier,
        NSToolbarShowColorsItemIdentifier,
        NSToolbarShowFontsItemIdentifier,
        NSToolbarCustomizeToolbarItemIdentifier,
        NSToolbarFlexibleSpaceItemIdentifier,
        NSToolbarSpaceItemIdentifier,
        NSToolbarSeparatorItemIdentifier, nil];
}
```

**Figure 1**  工具栏想项配置范例

![ Figure 1 ](http://i.imgbox.com/8Ya6UAJn.gif)

The default set of toolbar items is returned by implementing the required method *toolbarDefaultItemIdentifiers:*. The implementation is expected to return an array of identifiers containing the specified toolbar's default items. If during the toolbar's initialization no overriding values are found in the user defaults (by having called *setAutosavesConfiguration:* with YES as the argument) these items are used as the default set for the toolbar. In addition, if the user chooses to revert to the default toolbar items the set returned by *toolbarDefaultItemIdentifiers:* will be used.

The example code in Listing 2 causes the default items to be configured as shown in Figure 2.

通过实现必要的委托方法*toolbarDefaultIdentifiers:*来返回工具栏的默认项集合。实现被期望返回一个包含一组指定工具栏默认项的队列。如果在工具栏初始化时，没有在user defaults中找到覆盖值（通过以YES为参数调用*setAutosavesConfiguration:*方法），这些项就会被用于工具栏的默认项。此外，如果用户选择重置为默认工具栏，*toolbarDefaultItemIndentifiers:*方法返回的集合也会被用到。

在Listing 2中的范例代码引起默认项被配置，如Figure 2中所示。

**Listing 2**  *toolbarDefaultItemIdentifiers:*方法实现范例
```
- (NSArray *) toolbarDefaultItemIdentifiers: (NSToolbar *) toolbar {
    return [NSArray arrayWithObjects: SaveDocToolbarItemIdentifier,
        NSToolbarPrintItemIdentifier,
        NSToolbarSeparatorItemIdentifier,
        NSToolbarShowColorsItemIdentifier,
        NSToolbarShowFontsItemIdentifier,
        NSToolbarFlexibleSpaceItemIdentifier,
        NSToolbarSpaceItemIdentifier,
        SearchDocToolbarItemIdentifier, nil];
}
```
**Figure 2**  工具栏想项配置范例

![ Figure 2 ](http://i.imgbox.com/H5clCHoL.gif)



## Creating new toolbar items when requested

An implementation of the required method *toolbar:itemForItemIdentifier:willBeInsertedIntoToolbar:* returns an NSToolbarItem instance as specified by the toolbar item identifier. The item may not be immediately added to the toolbar, as this method is also called when the customization sheet is created.

The example code in Listing 3 creates a simple NSToolbarItem instance for the application's custom toolbar item, SaveDocToolbarItemIdentifier. This item appears as an icon in the toolbar using the default NSToolbarItem rendering.

一个*toolbar:itemForItemIdentifier:willBeInsertedIntoToolbar:*方法的实现返回一个按照给定的工具栏项标识符创建的NSToolbarItem实例。该项可能不会立即添加到工具栏中，因为该方法在定制窗口创建时也会被调用（译注：在定制窗口中的工具栏项并不一定真的显示在工具栏中，这取决于用户的设置）。

Listing 3中的范例代码为app的定制工具栏项（SaveDocToolbarItemIdentifier)创建了一个简单的NSToolbarItem实例。这个项使用默认的NSToolbarItem渲染在工具栏中表现为一个图标。

**Listing 3**  一个*toolbar:itemForItemIdentifier:willBeInsertedIntoToolbar:*方法的实现，用于创建一个简单的NSToolbarItem实例
```
- (NSToolbarItem *) toolbar:(NSToolbar *)toolbar
      itemForItemIdentifier:(NSString *)itemIdentifier
  willBeInsertedIntoToolbar:(BOOL)flag
{
    NSToolbarItem *toolbarItem = [[[NSToolbarItem alloc] initWithItemIdentifier: itemIdentifier] autorelease];
 
    if ([itemIdentifier isEqual: SaveDocToolbarItemIdentifier]) {
    // Set the text label to be displayed in the
    // toolbar and customization palette
    // 设置要在工具栏和定制调板中显示的文本标签。
    [toolbarItem setLabel:@"Save"];
    [toolbarItem setPaletteLabel:@"Save"];
 
    // Set up a reasonable tooltip, and image
    // you will likely want to localize many of the item's properties
    // 创建一个合理的工具提示和图像
    // 你很可能会想要本地化很多项的属性
    [toolbarItem setToolTip:@"Save Your Document"];
    [toolbarItem setImage:[NSImage imageNamed:@"SaveDocumentItemImage"]];
 
    // Tell the item what message to send when it is clicked
    // 告诉新创建的项当它被点击时，会发送什么消息。
    [toolbarItem setTarget:self];
    [toolbarItem setAction:@selector(saveDocument:)];
    } else  {
    // itemIdentifier referred to a toolbar item that is not
    // provided or supported by us or Cocoa
    // Returning nil will inform the toolbar
    // that this kind of item is not supported
    // 当itemIdentifier指的是我们或者Cocoa都不曾提供的项时...
    // 返回nil将通知工具栏：不支持该项的类型
    toolbarItem = nil;
    }
    return toolbarItem;
}
```

Returning a toolbar item that creates a custom view is somewhat more complicated. In addition to specifying the information required for a simple toolbar item, the application must also explicitly set the view that should be used to draw the item, the minimum size that the view requires to display properly, and the maximum size that the custom toolbar item can be resized.







