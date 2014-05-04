# Creating Software Products for the Mac Platform

Apps are the most common type of Mac software, but there are many other types of software that you can create, too. The following sections introduce the range of software products you can create for the Mac platform and suggest when you might consider doing so.

# 为Mac平台开发软件

Apps是Mac软件中最常见的类型，但是你还是可以创建很多除App之外的其他类型的的软件。下面的章节介绍了你可以为Mac平台开发的软件产品的范围以及一些当你考虑做这些的时候的建议。

## Apps

Apps are by far the predominant type of software created for Mac, or for any platform. You use Cocoa to build new Mac apps. To learn more about the features and frameworks available in Cocoa, see “Cocoa Application Layer.”

In general, there are three basic styles of Mac apps:

* **The single-window utility app.** A single-window utility app helps users perform the primary task within one window. Although a single-window utility app might also open an additional window—such as a preferences window—the user remains focused on the main window. Calculator is an example of a single-window utility app.
* **The single-window “shoebox” app.** The defining characteristic of a shoebox app is the way it gives users an app-specific view of their content. For example, iPhoto users don’t find or organize their photos in the Finder; instead, they manage their photo collections entirely within the app.
* **The multiwindow document-based app.** A multiwindow document-based app, such as Pages, opens a new window for each document the user creates or views. This style of app does not need a main window (although it might open a preferences or other auxiliary window).

Regardless of the app style you choose, your goal is probably to get your app into the Mac App Store. The development process that helps you achieve this goal includes a mix of coding and administrative tasks. Some of these tasks are:

Becoming a Mac developer
Deciding whether you need to code sign your app (apps that use iCloud or are sandboxed must be code signed)
Configuring your Xcode project
Taking advantage of the latest Mac technologies
Submitting your app to Apple for approval
This document gives you an overview of Mac technologies that you can incorporate into your app. To learn more about the other tasks involved in the development process, read Developing for the App Store.


## Apps

Apps是到目前为止为Mac亦或是其他任何平台创建的软件的最常见类型。你可以使用Cocoa去构建新的Mac应用。要了解Cocoa更多的特性和可用的框架，参阅“[ Cocoa Application Layer ]( https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/OSX_Technology_Overview/CocoaApplicationLayer/CocoaApplicationLayer.html#//apple_ref/doc/uid/TP40001067-CH274-SW1 )”。

一般而言，Mac应用具有几个基本风格：

* **单一窗口工具型app.** 一个单一窗口的工具型app能在一个窗口中帮助用户执行首要的任务。即使一个单一窗口工具型app可能也会打开一些额外的窗口——比如一个`偏好设置`窗口——但是用户的焦点也是一直在主窗口上的。Calculator.app就是一个单一窗口工具型app的例子。
* **单一窗口“shoebox”型app** “shoebox”型app的定义特征是给用户的内容一个apps指定的视图。比如iPhoto.app的用户不会在Finder中查找和管理他们的照片，取而代之的是他们完全在iPhoto这个应用中去管理他们的照片集合。
* **多窗口基于文档型app** 像Pages.app这样的就是一个多窗口的基于文档的app，它为用户创建或浏览的每一份文档都单独地打开一个窗口。这种风格的app不需要主窗口（即使它可能打开一个偏好设置或者其他什么辅助窗口）。

不管你为你的app选择哪一种风格，你的最终目标可能都是想让你的app能够进入Mac App Store去销售。










