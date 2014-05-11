# Selectable Toolbar Items

NSToolbar allows you to specify that certain items in the toolbar can indicate a selected state. This is often used in conjunction with an 
NSTabView that is configured to have no visible tabs. Figure 1 contains an example implementation similar to that of Safari and the Finder.

*Figure 1*  Selectable NSToolbar items used as preferences navigation

NSToolbar允许你将某个特定的项标记为选中状态。这通常和一个被配置成拥有不可见标签的NSTabView实例一同使用。Figure 1中包含了一个与Safari和Finder相似的范例实现。

*Figure 1*  用于偏好设置导航的可选工具栏项。

![Figure 1](http://i.imgbox.com/YFMXVcPA.gif)

Toolbars that need to indicate item selection must specify the items that can be selected by implementing the delegate method *toolbarSelectableItemIdentifiers:*. This method returns an array containing the identifiers of the items that can be selected. The example Listing 1in returns all the identifiers for the preferences implementation.

**Listing 1**  Example implementation of *toolbarSelectableItemIdentifiers:*

需要标记其某个项被选中的工具栏，必须通过实现委托方法*toolbarSelectableItemIdentifiers:*来指定这些项。该方法返回一个包含可以被选中的项的数组。范例Listing 1实现返回偏好设置面板所需的全部可选项的标识符。

**Listing 1**  *toolbarSelectableItemIdentifiers:*方法的范例实现：

```
- (NSArray *)toolbarSelectableItemIdentifiers: (NSToolbar *)toolbar;
{
    // Optional delegate method: Returns the identifiers of the subset of
    // toolbar items that are selectable. In our case, all of them
    // 可选委托方法： 返回被设为可选中的工具栏项的子集。
    // 在我们的例子中：返回全部
    return [NSArray arrayWithObjects:GeneralPreferences,
                                    AccountPreferences,
                                    AppearancePreferences,
                                    FontsAndColorsPreferences,
                                    AdvancedPreferences, nil];
}
```

Your application can specify the currently selected toolbar item using the method *setSelectedItemIdentifier:* passing the identifier for the desired toolbar item. The currently selected toolbar item is returned by the method *selectedItemIdentifier*. If there is no currently selected, nil is returned.

你的应用程序可以使用*setSelectedItemIdentifier:*方法并传入期望被选中的项的标识符来指定当前选中的工具栏项。当前选中的工具栏想会通过*selectedItemIdentifier*方法被返回。如果当前没有被选中的项，那么会返回nil。