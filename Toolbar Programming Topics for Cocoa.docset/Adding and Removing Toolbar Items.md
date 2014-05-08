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

**Listing 1**  Example *toolbarAllowedItemIdentifiers:* method implementation
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

**Figure 1**  Example toolbar item configuration

![ Figure 1 ](http://i.imgbox.com/8Ya6UAJn.gif)

The default set of toolbar items is returned by implementing the required method *toolbarDefaultItemIdentifiers:*. The implementation is expected to return an array of identifiers containing the specified toolbar's default items. If during the toolbar's initialization no overriding values are found in the user defaults (by having called *setAutosavesConfiguration:* with YES as the argument) these items are used as the default set for the toolbar. In addition, if the user chooses to revert to the default toolbar items the set returned by *toolbarDefaultItemIdentifiers:* will be used.

The example code in Listing 2 causes the default items to be configured as shown in Figure 2.

通过实现必要的委托方法*toolbarDefaultIdentifiers:*来返回工具栏的默认项集合。实现被期望返回一个包含一组指定工具栏默认项的队列。如果在工具栏初始化时，没有在user defaults中找到覆盖值（通过以YES为参数调用*setAutosavesConfiguration:*方法），这些项就会被用于工具栏的默认项。此外，如果用户选择重置为默认工具栏，*toolbarDefaultItemIndentifiers:*方法返回的集合也会被用到。

*Listing 2*  Example toolbarDefaultItemIdentifiers: method implementation
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
*Figure 2*  Example toolbar items configuration

![ Figure 2 ](http://i.imgbox.com/H5clCHoL.gif)





