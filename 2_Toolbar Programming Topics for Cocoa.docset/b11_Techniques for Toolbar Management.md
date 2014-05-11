# Techniques for Toolbar Management

You can determine the height of a toolbar and whether it has overflow items by following the procedures described below.

# 工具栏管理技术

你可以通过下面描述的过程来决定工具栏的高度以及其是否拥有溢出菜单项。

## Determining if a Toolbar Has Overflow Items

If a toolbar is unable to display all the user's currently configured toolbar items, it pushes the additional items into the overflow menu and displays the overflow menu icon as shown in Figure 1.

**Figure 1**  A toolbar indicating items in the overflow menu

## 决定一个工具栏是否拥有溢出菜单项

如果一个工具栏不能够显示用户当前配置的全部的工具栏项的话，其将会把多出的项放到溢出菜单中，然后像Figure 1中所示的那样显示溢出菜单的图标。

**Figure 1**  A toolbar indicating items in the overflow menu

![Figure 1](http://i.imgbox.com/gb6pv49f.gif)

An application can determine if a toolbar has overflow items by comparing the number of items returned by the method *items* with the number of items returned by the *visibleItems* method as shown in Listing 1. If these values differ, then the toolbar has items in the overflow menu.

**Listing 1**  Example code to test if a toolbar has overflow items

应用程序可以通过如Listing 1中所示的那样，比较*items*方法和*visibleItems*方法所返回的项列表的数目，来决定工具栏是否拥有溢出菜单项。如果这些值是不同的，那么工具栏的一些项将会存在于溢出菜单中。

**Listing 1**  测试一个工具栏是否拥有溢出菜单的范例代码
```
int numberOfItems=[[theToolbar items] count];
int numberOfVisibleItems=[[theToolbar visibleItems] count];
 
if (numberOfItems != numberOfVisibleItems) {
    // toolbar has overflow items
}
```

## Calculating a Toolbar’s Height

Although NSToolbar does not currently provide a method for returning a toolbar’s height, it is easy to compute that value. You subtract the height of the window’s content view from the window’s height.

The Objective-C function in Listing 2 calculates the height of the toolbar in a window, returning 0 if the toolbar is hidden.

**Listing 2*  Objective-C function to calculate toolbar height

## 计算工具栏的高度

即使NSToolbar当前不提供返回工具栏高度的方法，但是很容易去计算该值。只需从工具栏所在窗口的高度值中减去该窗口内容视图（content view）的高度值，即可得出工具栏的高度。

在Listing 2中的Objective-C函数，计算了一个窗口中的工具栏的高度，如果工具栏被隐藏了，那么返回0。

**Listing 2*  用于计算工具栏高度的Objective-C函数
```
float ToolbarHeightForWindow(NSWindow *window)
{
    NSToolbar *toolbar;
    float toolbarHeight = 0.0;
    NSRect windowFrame;
 
    toolbar = [window toolbar];
 
    if(toolbar && [toolbar isVisible])
    {
        windowFrame = [NSWindow contentRectForFrameRect:[window frame]
                                styleMask:[window styleMask]];
        toolbarHeight = NSHeight(windowFrame)
                        - NSHeight([[window contentView] frame]);
    }
 
    return toolbarHeight;
}
```







