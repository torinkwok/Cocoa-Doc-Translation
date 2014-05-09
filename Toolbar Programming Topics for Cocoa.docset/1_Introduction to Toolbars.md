# Introduction to Toolbars

NSToolbar and NSToolbarItem provide you with a standard way to display a toolbar for a titled window below its title bar. These classes also provide users with a standard way to customize toolbars and save those customizations.

# Toolbars介绍

NSToolbar和NSToolbarItem提供给你一个在标题栏窗口中，在其标题栏下方显示工具栏的标准途径。这些类也提供给用户定制工具栏并保存那些定制的标准途径。



## Organization of This Document

This programming topic describes how to use toolbars. It contains the following articles:

* “How Toolbars Work” gives basic information on toolbars.

* “Toolbar Management Checklist” describes what happens when you create a toolbar.

* “Adding and Removing Toolbar Items” describes managing toolbar items, and the role of the NSToolbar delegate.

* “Setting a Toolbar Item’s Representation” describes the different ways a toolbar item can be represented and how to set them.

* “Validating Toolbar Items” describes how to set whether a toolbar item is clickable or not.

* “Setting a Toolbar Item’s Size” describes how to set a toolbar item’s minimum and maximum size.

* “Selectable Toolbar Items” describes how to support selectable toolbar items.

* “Subclassing NSToolbarItem” describes the methods to override when subclassing NSToolbarItem.

* “Techniques for Toolbar Management” describes how to determine if a toolbar has items in the overflow menu and how to calculate
toolbar height.

## 这份文档的组织方式

这份变成主题描述了如何使用工具栏。它包含以下几篇文章：

* “工具栏如何工作” 提供了toolbars的基本信息。

* “工具栏管理清单” 描述了当你创建一个工具栏时发生了什么。

* “添加和移除工具栏项” 描述了管理工具栏项，以及NSToolbar delegate所扮演的角色（即其所起到的作用）。

* “设置工具栏项的表现形式” 描述了一个工具栏项可以被展现成的不同的形式以及如何设置它们。

* “验证工具栏项” 描述了如何设置某一个工具栏项是否是可点击的。

* “设置工具栏项的尺寸” 描述了如何设置一个工具栏项的最大和最小尺寸。

* “可选中的工具栏项” 描述了如何支持可选中的工具栏项。

* “子类化NSToolbarItem” 描述了当子类化NSToolbarItem时需要重写的方法。

* “工具栏管理技术” 描述了如何决定一个工具栏是否有被添加到*溢出菜单*中的项，以及如何计算工具栏的高度。


## See Also

The following sample code is available through Apple Developer Connection:

* [ iSpend ]( https://developer.apple.com/library/mac/samplecode/iSpend/Introduction/Intro.html#//apple_ref/doc/uid/DTS10003625 ) shows how to add basic toolbar support to an application.

* [ ToolbarSample ]( https://developer.apple.com/library/mac/samplecode/ToolbarSample/Introduction/Intro.html#//apple_ref/doc/uid/DTS10000413 ) implements an example toolbar including using custom views in a toolbar item.

## 另请参阅

下面的示例通过Apple Developer Connection可用：

* [ iSpend ]( https://developer.apple.com/library/mac/samplecode/iSpend/Introduction/Intro.html#//apple_ref/doc/uid/DTS10003625 ) 展示了如何为一个app添加基本的工具栏支持。

* [ ToolbarSample ]( https://developer.apple.com/library/mac/samplecode/ToolbarSample/Introduction/Intro.html#//apple_ref/doc/uid/DTS10000413 ) 实现了一个在toolbar项中使用custom视图的示例