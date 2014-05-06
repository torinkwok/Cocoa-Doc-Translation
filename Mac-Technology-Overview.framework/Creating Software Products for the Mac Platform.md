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

* Becoming a Mac developer
* Deciding whether you need to code sign your app (apps that use iCloud or are sandboxed must be code signed)
* Configuring your Xcode project
* Taking advantage of the latest Mac technologies
* Submitting your app to Apple for approval

This document gives you an overview of Mac technologies that you can incorporate into your app. To learn more about the other tasks involved in the development process, read Developing for the App Store.


## Apps

Apps是到目前为止为Mac亦或是其他任何平台创建的软件的最常见类型。你可以使用Cocoa去构建新的Mac应用。要了解Cocoa更多的特性和可用的框架，参阅“[ Cocoa Application Layer ]( https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/OSX_Technology_Overview/CocoaApplicationLayer/CocoaApplicationLayer.html#//apple_ref/doc/uid/TP40001067-CH274-SW1 )”。

一般而言，Mac应用具有几个基本风格：

* **单一窗口工具型app.** 一个单一窗口的工具型app能在一个窗口中帮助用户执行首要的任务。即使一个单一窗口工具型app可能也会打开一些额外的窗口——比如一个`偏好设置`窗口——但是用户的焦点也是一直在主窗口上的。Calculator.app就是一个单一窗口工具型app的例子。
* **单一窗口“shoebox”型app** “shoebox”型app的定义特征是给用户的内容一个apps指定的视图。比如iPhoto.app的用户不会在Finder中查找和管理他们的照片，取而代之的是他们完全在iPhoto这个应用中去管理他们的照片集合。
* **多窗口基于文档型app** 像Pages.app这样的就是一个多窗口的基于文档的app，它为用户创建或浏览的每一份文档都单独地打开一个窗口。这种风格的app不需要主窗口（即使它可能打开一个偏好设置或者其他什么辅助窗口）。

不管你为你的app选择哪一种风格，你的最终目标可能都是想让你的app能够进入Mac App Store去销售。帮助你实现这一目标的开发流程包括编码和管理工作的结合。要做的一些工作是：
* 成为一名Mac开发者
* 决定你是否需要签名机制认证你的app（使用了iCloud或者沙箱机制的app必须进行代码签名）。
* 配置你的Xcode项目
* 利用最新的Mac开发技术
* 向Apple公司提交你的app并等待审核比准。

这份文档给了你一份关于你可以并入你的app的Mac开发技术的概览。想要了解开发流程中牵涉到的更多工作细节，参阅*Developing for the App Store*。


## Other Types of Software

There are many other types of software you can develop for Mac. Most of these software products have no user interface (UI) and instead provide services that extend the capabilities of other software, such as third-party apps or the system itself.

### Frameworks
A framework is a special type of bundle used to distribute shared resources, including library code, resource files, header files, and reference documentation. Frameworks offer a more flexible way to distribute shared code—for example, image files and localized strings—that you might otherwise put into a dynamic shared library. Frameworks also have a version control mechanism that makes it possible to distribute multiple versions of a framework in the same framework bundle.

Apple uses frameworks to distribute the public interfaces of OS X (and iOS), which are packaged in software development kits. A software development kit (SDK) collects the frameworks, header files, tools, and other resources necessary for developing software targeted at a specific version of a platform. You, too, can use frameworks to distribute public code and interfaces that you create, or to develop private shared libraries to embed in your apps.

```
Note: Although OS X also supports the concept of an “umbrella” framework, which encapsulates multiple subframeworks in a single package, this mechanism is used primarily for the distribution of Apple software. The creation of umbrella frameworks by third-party developers is not recommended.
```

## 其他软件类型

你还可以为Mac开发很多其他类型的软件。大多数这样的软件产品都是没有用户界面的（UI）并且它们的用途是扩展其他的诸如第三方apps或者系统自带apps的软件功能。

### 框架（Frameworks）
框架其实是一种用于分发共享资源的特殊类型的bundle，其中包括了库代码，资源文件，头文件，以及参考文献等。框架为分发共享代码提供了更灵活的方式——比方说图片文件和本地化字符串文件——你都可以将它们放到一个动态的共享库中。框架同时还提供了将多版本的框架部署到同一个框架bundle中的**版本控制机制**。

Apple工具使用框架来部署公开的OS X（以及iOS）编程接口，他们都被打包在**软件开发套件（SDK）**中。一个SDK集合了为一个平台的特定版本开发软件所需的所有框架，头文件，开发工具以及其他的各类资源。你也可以使用你自己创建的框架去部署公共代码和接口，或者开发嵌入到你自己的apps中的私有共享库。


```
注意：即使OS X也提供了将多个子框架封装到一个单个包中的所谓的“包罗”框架机制，但是这个机制主要是用于Apple公司内部软件的部署。并不赞成第三方开发者创建包罗框架。
```

You can use any programming language to create your own frameworks, but it’s best to choose a language that makes it easy to update the framework later. Apple frameworks generally export programmatic interfaces in either ANSI C or Objective-C. Both of these languages have a well-defined export structure that makes it easy to maintain compatibility between different revisions of the framework.

To learn about the structure and composition of frameworks, see [ Framework Programming Guide ](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPFrameworks/Frameworks.html#//apple_ref/doc/uid/10000183i ). That document also describes how to use Xcode to create public and private frameworks.

你可以使用任何编程语言去创建你自己的框架，但是最好选择一种能够使后续的框架更新变得最容易的语言。Apple公司的框架通常都是以ANSI C或者Objective-C两种语言中的一种来导出可编程接口的。这两种语言都具有定义明确的倒出结构，可以使框架的不同修订版之间保持良好的兼容性。

想要了解更多关于框架的结构和组成的话，参阅[ Framework Programming Guide ](https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPFrameworks/Frameworks.html#//apple_ref/doc/uid/10000183i )。该文档还描述了如何使用Xcode去创建公开和私有的框架。

### Plug-ins
Plug-ins are the standard way to extend many apps and system behaviors. A plug-in is a bundle whose code is loaded dynamically into the runtime of an app. Because it’s loaded dynamically, a plug-in can be added and removed by the user.

The app and system plug-ins listed below represent some of the many opportunities for developing plug-ins.

* **Address Book action plug-ins.** An Address Book plug-in lets you add custom actions that act on the data in a person’s Address Book card. For example, the existing Large Type action displays the selected phone number in large type. Each action plug-in performs a single action, which can open a simple window within the Address Book app. If an action needs to do anything else, it must launch your app to perform the action. To learn how to create an Address Book action plug-in, see “[ Creating and Using Address Book Action Plug-ins ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AddressBook/Tasks/Actions.html#//apple_ref/doc/uid/20001681 )”.

* **App plug-ins.** An app plug-in can extend the features of any app that supports a plug-in model. In addition to third-party apps, several Apple apps also support plug-ins, such as iTunes, Final Cut Pro, and Aperture. For information about developing plug-ins for Apple apps, visit the [ Apple Developer website ]( https://developer.apple.com/ ).

* **Automator plug-ins.** Using an Automator plug-in, you can expand the default set of actions available in Automator, a utility app that lets users assemble complex scripts using a palette of predefined actions. Automator plug-ins can be written in AppleScript or Objective-C, so you can write them for your own app’s features or for the features of other scriptable apps. (It’s a good idea to provide Automator plug-ins for your app’s most common tasks because doing so gives users more ways to interact with your app.) To learn how to write an Automator plug-in, see [ Automator Programming Guide ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/AutomatorConcepts/Automator.html#//apple_ref/doc/uid/TP40001450 ).

* **Core Audio plug-ins.** A Core Audio plug-in can support the manipulation of audio streams during most processing stages. For example, you can use plug-ins to generate, process, or receive an audio stream or to interact with new types of audio-related hardware devices. To begin learning about Core Audio, read [ Core Audio Overview ]( https://developer.apple.com/library/mac/documentation/MusicAudio/Conceptual/CoreAudioOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40003577 ).

* **Image units.** An image unit is a type of plug-in that you can use with the Core Image and Core Video technologies. An image unit consists of a collection of filters—each of which implements a specific manipulation for image data—packaged together in a single bundle. For example, you could write a set of filters that perform different kinds of edge detection and package them as one image unit. To learn how to create an image unit, see “Packaging Filters as Image Units”.

* **Input methods.** A common example of an input method is an interface for typing Japanese or Chinese characters using multiple keystrokes. Other examples of input methods include spelling checkers and pen-based gesture recognition systems. You can create input methods using Input Method Kit (InputMethodKit.framework). For information on how to use this framework, see [ Input Method Kit Framework Reference ]( https://developer.apple.com/library/mac/documentation/Cocoa/Reference/InputMethodKitFrameworkRef/_index.html#//apple_ref/doc/uid/TP40006154 ).

* **Metadata importers.** Spotlight relies on metadata importers to gather information about the user’s files and to build a systemwide index. Spotlight uses this index to help users find information by searching on attributes that make sense to them, such as the duration of a video or the dimensions of an image. If your app defines a custom file format, you should always provide a metadata importer for that file format. (If your app relies on commonly used file formats, such as JPEG, RTF, or PDF, the system provides a metadata importer for you.) To learn how to create metadata importers, see [ Spotlight Importer Programming Guide ]( https://developer.apple.com/library/mac/documentation/Carbon/Conceptual/MDImporters/MDImporters.html#//apple_ref/doc/uid/TP40001267 ).

* **Quartz Composer plug-ins.** Quartz Composer supports a plug-in mechanism that allows you to create a custom patch and make it available in the Quartz Composer workspace and to most Quartz Composer clients. (A patch is processing unit that performs a specific task, such as processing a string or rendering an OpenGL texture.) To learn how to create a Quartz Composer plug-in, see [ Quartz Composer Custom Patch Programming Guide ]( https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/QuartzComposer_Patch_PlugIn_ProgGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004787 ).

* **Quick Look plug-ins.** A Quick Look plug-in—also known as a Quick Look generator—converts a document from its native format into a format that Quick Look can display to users. If your app creates documents of a nonstandard or private type, it’s a good idea to provide a Quick Look generator so that users can get previews of these documents in Quick Look. To learn how to create a Quick Look plug-in, see [ Quick Look Programming Guide ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/Quicklook_Programming_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005020 ).

* **Safari plug-ins.** Safari supports the Netscape-style plug-in model for incorporating additional types of content in the web browser. In Safari in OS X v10.7 and later, these plug-ins run in their own process, which improves the stability and security of Safari. Netscape-style plug-ins include support for onscreen drawing, event handling, and networking and scripting functions.

```
Note: Beginning in OS X v10.7, Safari does not support WebKit plug-ins because they are not compatible with the new process architecture. Going forward, you must convert WebKit plug-ins to Netscape-style plug-ins or Safari Extensions
```



### 插件（Plug-ins）

插件是对众多apps和系统行为进行扩展的标准方式。一个插件其实就是一个可以由一个app在运行时动态加载的bundle。因为它是被动态加载的，所以用户可以直接添加或者移除一个插件。

下方列出的app和系统插件向你展示了开发插件的众多可能性：

* **地址簿动作插件。** 一个地址簿动作插架允许你添加能够作用于某一个人的地址簿卡片数据的行为。举个例子：已经存在的*Large Type*动作就以large type的形式去显示用户选中的电话号码。如果需要任何其他动作，必须运行你的app来执行该动作。想要了解如何创建地址簿动作插件，参阅“[ Creating and Using Address Book Action Plug-ins ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AddressBook/Tasks/Actions.html#//apple_ref/doc/uid/20001681 )”。

* **App插件。** App插件可以扩展任何支持插件模型的app的功能。除了第三方应用之外，几个Apple公司的app也同样支持插件，比如iTunes.app， Final Cut Pro.app，以及Aperture.app。想了解更多有关为Apple的应用开发插件的信息，请访问[ Apple Developer website ]( https://developer.apple.com/ )站点。

*  **Automator插件。** 使用Automator插件，你可以扩展Automator默认支持的动作集，一个工具型app通常都允许用户通过与定义的动作调板组合各种复杂的脚本。Automator插件可以使用AppleScript或者Objective-C编写，所以你可以为你自己的app或者其他支持脚本apps添加特性编写它们。（为你的app的最通用的功能提供Automator插件是一个很棒的注意，因为这样可以给予用户更多的与你的app交互的方式）。想了解如果编写Automator插件，参阅[ Automator Programming Guide ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/AutomatorConcepts/Automator.html#//apple_ref/doc/uid/TP40001450 )。

*  **Core Audio插件** Core Audio插件可以提供在大多数处理阶段中对音频流的操作。举个例子：你可以使用Core Audio插件去生成，处理或者接收一个音频流或者与一个音频相关的硬件设备进行交互。想要了解Core Audio，参阅 [ Core Audio Overview ]( https://developer.apple.com/library/mac/documentation/MusicAudio/Conceptual/CoreAudioOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40003577 )。

* **图像单元。** 图像单元可以与Core Image和Core Video技术一起使用的插件类型。一个图像单元由一个过滤器集合组成，每个过滤器实现了一个针对图像数据的特性的处理方式，最后将它们打包在一个独立的bundle中。举个例子：你可以编写一系列执行不同种类边界检测的过滤器并且将它们打包成一个图像单元。想要了解如何创建一个图像单元，参阅“*Packing Filters as Image Units*”。

* **输入法。** 一个输入法的常见例子就是使用多键输入的日文或中文输入接口。输入法的其他例子还包括拼写检查和基于钢笔的手势识别系统。你可以使用输入法套件（InputMethodKit.framework）创建输入法。关于如何使用这个框架的信息，参阅[ Input Method Kit Framework Reference ]( https://developer.apple.com/library/mac/documentation/Cocoa/Reference/InputMethodKitFrameworkRef/_index.html#//apple_ref/doc/uid/TP40006154 )。

* **元数据导入器。** Spotlight依赖于元数据导入器来收集关于用户文件的信息并根据此来构建一个系统范围的索引。Spotlight使用这个索引并通过对诸如一段视频的长度或者一幅图像的尺寸这类用户能够理解的属性进行搜索来帮助用户定位信息。如果你的app定义了一个定制文件格式，你应该总是为这个文件格式提供元数据导入器。（你过你的app依赖于诸如JPEG，RTF，或者PDF这类通常使用的文件格式，系统则已经为你提供了元数据导入器。）想要了解如何创建元数据导入器，参阅[ Spotlight Importer Programming Guide ]( https://developer.apple.com/library/mac/documentation/Carbon/Conceptual/MDImporters/MDImporters.html#//apple_ref/doc/uid/TP40001267 )。

* **Quartz组合器插件。** Quartz组合器插件提供了一个插件机制，它允许你创建自定义的补丁并且使该补丁在Quartz组合器的工作空间和大多数的Quartz组合器的客户端中都可用。（一个补丁其实是一个用于执行诸如处理字符串或者渲染OpenGL纹理之类的特定任务的处理单元。）要想了解如何创建Quartz组合器插件，参阅[ Quartz Composer Custom Patch Programming Guide ]( https://developer.apple.com/library/mac/documentation/GraphicsImaging/Conceptual/QuartzComposer_Patch_PlugIn_ProgGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004787 )。

* **Quick Look插件。** Quick Look插件又名：Quick Look生成器——它将一个文档的原始格式转化成Quick Look可以显示给用户的格式。如果你的app创建了非标准或者私有类型的文档，那么提供一个Quick Look生成器以便于用户可以在Quick Look中获取这些文档的预览是一个很棒的注意！。要想了解如何创建Quick Look插件，参阅[ Quick Look Programming Guide ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/Quicklook_Programming_Guide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40005020 )。

* **Safari插件。** Safari提供了Netscape风格的插件模型以便你将额外类型的内容并入web浏览器。在OS X 10.7之后版本中的Safari中，插件都是运行在其自己的进程中，这提升了Safari的稳定性和安全性，Netscape风格的插件提供了包括屏幕绘制，事件处理，网络及脚本函数等功能。

```
注意： 从OS X 10.7开始，Safari不再支持Webkit插件，因为它们与新的进程架构不再兼容。在后续的开发中，你必须将你的Webkit风格插件转换成Netscape风格插件，或者直接开发Safari扩展。
```

### Safari Extensions
Use Safari extensions to add features both to the Safari web browser and to the content that Safari displays. For example, you can add custom buttons to the browser’s toolbar, reformat webpages, block unwanted sites, and create contextual menu items. Extensions let you inject scripts and style sheets into pages of web content.

A Safari extension is a collection of HTML, JavaScript, and CSS files with support for both HTML5 and CSS3. Safari extensions are supported in both OS X and Windows systems running Safari 5.0 and later.

To learn more about Safari extensions, read Safari Extensions Development Guide in the [ Safari Developer Library ]( https://developer.apple.com/library/safari/navigation/index.html ).

### Safari扩展（Safari Extensions）
使用Safari扩展以向Safari浏览器和Safari浏览器显示的页面添加新的特性。举个例子：你可以向浏览器的工具栏中添加定制按钮，可以重写格式化网页，可以屏蔽有害网站，并且还可以创建上下文菜单项。扩展使得你可以向web页面注入脚本和样式表。

一个Safari扩展其实就是一个HTML，JavaScript以及CSS文件的集合，它支持HTML 5和CSS3，Safari扩展同时被OS X和Windows上运行的Safari 5.0之后的版本所支持。

要了解更多关于Safari扩展的内容，参阅[ Safari Developer Library ]( https://developer.apple.com/library/safari/navigation/index.html )。

### Dashboard Widgets
A Dashboard widget is a lightweight web app that helps users perform a common task, such as checking a stock price or getting a weather report. Widgets reside in the Dashboard environment, which can appear over the user’s current desktop or as a separate space. OS X includes several built-in widgets, and users can download third-party widgets from [ Apple - Downloads - Dashboard ]( http://www.apple.com/downloads/dashboard/ ).

In effect, widgets are HTML-based apps with optional JavaScript code to provide dynamic behavior. Dashboard uses WebKit to provide the environment for displaying the HTML and running the JavaScript code. Your widgets can take advantage of several extensions provided by that environment, including a way to render content using Quartz-like JavaScript functions.

The Dashcode app provides a streamlined environment for developing widgets and includes several templates that help you get started. To learn how to use Dashcode, see [ Dashcode User Guide ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Dashcode_UserGuide/Contents/Resources/en.lproj/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004692 ). To learn more about the technologies you can use in a widget, see [ Dashboard Programming Topics ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Dashboard_ProgTopics/Introduction/Introduction.html#//apple_ref/doc/uid/TP40002837 ).

### Dashboard窗件（Dashboard Widgets）
Dashboard窗件是帮助用户执行诸如查询股票价格或者获取天气预报之类的通用任务的轻量级web应用。窗件（Widgets）存在于Dashboard环境中，该环境可以展示在用户的当前桌面或者分隔空间中。OS X内置了几款窗件，并且用户可以从[ Apple - Downloads - Dashboard ]( http://www.apple.com/downloads/dashboard/ )下载第三方窗件。

实际上，窗件是基于HTML的app，并且可以选择使用JavaScript代码为其提供动态行为。Dashboard使用WebKit来提供显示HTML和运行JavaScript代码的环境。你的窗件可以利用该环境提供的几个扩展，包括使用累Quartz的JavaScript函数渲染内容。

Dashcode.app提供了一个简化的用于开发窗件的环境，并且还囊括了几个帮助你开始开发的模版。要了解如何使用Dashcode.app，参阅[ Dashcode User Guide ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Dashcode_UserGuide/Contents/Resources/en.lproj/Introduction/Introduction.html#//apple_ref/doc/uid/TP40004692 )。要了解更多你可以在窗件中使用的技术，参见[ Dashboard Programming Topics ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/Dashboard_ProgTopics/Introduction/Introduction.html#//apple_ref/doc/uid/TP40002837 )。

### Agent Applications
An agent is a special type of application that typically runs in the background, providing information as needed to the user or to another app. For example, the Dock is an agent application that is run by OS X.

An agent can be launched by the user but is more likely to be launched by the system or another app. As a result, agents do not show up in the Dock or the window displayed by the Force Quit menu command. Although agents might occasionally come to the foreground and display a user interface, they do not have a menu bar for choosing commands. All user interaction with an agent application is brief and focused on a specific goal, such as setting preferences or requesting information.

To create an agent application, you create a bundled app and include the LSUIElement key in its information property list (Info.plist) file. For more information on using this key, see [ Information Property List Key Reference ]( https://developer.apple.com/library/mac/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247 ).

### 应用程序代理（Agent Applications）
代理其实是一种运行在后台，按需向用户或者其他app提供信息的特殊类型的app。举个例子：Dock就是一个由OS X运行的应用程序代理。

一个代理可以由用户启动，但是更多的可能是被系统或者其他app启动。因此，代理不会在通过强制退出菜单命令出现在Dock或者正在显示的窗口中。即使代理偶尔可能会浮现在前台并显示它的用户界面，但是它们没有选择命令的菜单栏。所有用户与代理应用程序之间的交互都是很简短并且很有针对性的，比如设置偏好或者请求信息。

要想创建一个代理app，你应该创建一个打包的app并且在它的信息属性列表文件（Info.plist）中包含LSUIElment键。想要了解更多关于使用该键的信息，参阅[ Information Property List Key Reference ]( https://developer.apple.com/library/mac/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247 )。


### Screen Savers
Screen savers are small programs that take over the screen after a certain period of idleness. Screen savers provide entertainment and also prevent the screen image from being burned into the surface of a display. OS X supports both slideshows and programmatically generated screen-saver content.

A slideshow is a simple type of screen saver that does not require any code to implement. To create a slideshow, you create a bundle with an extension of .slideSaver. Inside this bundle, you place a Resources directory that contains the images you want to display in your slideshow. Your bundle should also include an information property list that specifies basic information about the bundle, such as its name, identifier string, and version.

OS X includes several slideshow screen savers you can use as templates for creating your own. These screen savers are located in /System/Library/Screen Savers. You should put your own slideshows in either /Library/Screen Savers or in the ~/Library/Screen Savers directory of a user.

A programmatic screen saver is a screen saver that continuously generates content to appear on the screen. You can use this type of screen saver to create animations or to create a screen saver with user-configurable options. The bundle for a programmatic screen saver ends with the .saver extension.

You create programmatic screen savers using Cocoa and the Objective-C language. Specifically, you create a custom subclass of [ ScreenSaverView ]( https://developer.apple.com/library/mac/documentation/UserExperience/Reference/ScreenSaver/Classes/ScreenSaverView_Class/Reference/Reference.html#//apple_ref/occ/cl/ScreenSaverView ) that provides the interface for displaying the screen saver content and options. The information property list of your bundle provides the system with the name of your custom subclass. For information on creating programmatic screen savers, see[ Screen Saver Framework Reference ]( https://developer.apple.com/library/mac/documentation/UserExperience/Reference/ScreenSaver/ObjC_classic/_index.html#//apple_ref/doc/uid/20001822 ).

### 屏幕保护程序（Screen Savers）
屏幕保护程序是一个在系统一段时间闲置后对屏幕进行接管的小程序。***Screen savers provide entertainment and also prevent the screen image from being burned into the surface of a display.（这一句求翻译）***OS X支持幻灯片和以编程的方式生成屏幕保护程序的内容。

幻灯片是一种不用任何代码就可以实现的简单的屏幕保护程序类型。要创建一个幻灯片，你应该创建一个扩展名为.slideSaver的bundle。在这个bundle中，你应该放置一个包含你想在幻灯片中显示的图像的资源列表。你的bundle也应该包含一个指定了诸如名称，标识字符串和版本等基本信息的Info.plist文件。

OS X囊括了几个幻灯片保护程序，你可以在创建自己的屏幕保护程序时将它们用作模板。这些屏幕保护程序位于`/System/Library/Screen Savers`。你应该将你自己的幻灯片放到`/Library/Screen Savers`或者某个用户的`~/Library/Screen Savers`中。

一个编程式的屏幕保护程序是一个持续在屏幕上生成内容的屏幕保护程序。你可以使用这种类型的屏幕保护程序来创建动画或者带有创建用户可配置选项的屏幕保护程序。编程式的屏幕保护程序的bundle以扩展名.saver结尾。

你应该使用Cocoa和Objective-C语言来创建编程式的屏幕保护程序。尤其是，你需要创建一个[ ScreenSaverView ]( https://developer.apple.com/library/mac/documentation/UserExperience/Reference/ScreenSaver/Classes/ScreenSaverView_Class/Reference/Reference.html#//apple_ref/occ/cl/ScreenSaverView )的子类，该类提供了用于显示屏幕保护程序内容和选项的界面。你的bundle中的Info.plist文件将你定制的子类的名字提供给系统。想要了解更多关于创建编程式屏幕保护程序的信息，参见[ Screen Saver Framework Reference ]( https://developer.apple.com/library/mac/documentation/UserExperience/Reference/ScreenSaver/ObjC_classic/_index.html#//apple_ref/doc/uid/20001822 )。

### Services
Services are not separate programs that you write; instead, they are features exported by your app for the benefit of other apps. Services let you share the resources and capabilities of your app with other apps in the system. Users access services through the Services menu that is available in every app’s application menu. (Services replace the contextual menu plug-in functionality that was available in earlier versions of OS X.)

A service typically acts on the currently selected data. When the user initiates a service, the app that holds the selected data places it on the pasteboard. The app whose service was selected then takes the data, processes it, and puts the results (if any) back on the pasteboard for the original app to retrieve. For example, a user might select a folder in the Finder and choose a service that compresses the folder contents and replaces them with the compressed version. Services can represent one-way actions as well. For example, a service could take the currently selected text in a window and use it to create the content of a new email message. For information on how to provide and use services in your app, see [ Services Implementation Guide ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/SysServices/introduction.html#//apple_ref/doc/uid/10000101i ).

### 服务（Services）
服务并不是一个由你单独编写的应用程序，它们反而导出你的app的功能来惠及其他app。服务允许你在系统中和其他app共享你的app的资源和功能。用户可以通过`Services`菜单来访问服务，这个子菜单在所有app的应用程序菜单中都可用。（**服务**替换了OS X早前版本中可用的**上下文菜单插件功能**。）

服务通常作用于当前选中的数据。当用户初始化一个服务时，控制选中数据的app将选中数据放到剪贴板中。选择的服务所属的app会获取这些数据，处理它们，然后将结果（如果有的话）写回到剪贴板中来让最初的那个app取回。举个例子：用户可以选中Finder中的一个文件夹，然后选择压缩文件夹的系统服务并且使用压缩版本替代原始版本。服务也可以提供单向动作。举个例子：一个服务可以获取一个窗口中当前选中的文本，并且使用这些文本去创建一条email消息。要想了解如何在你的app中提供和使用系统服务，参阅：[ Services Implementation Guide ]( https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/SysServices/introduction.html#//apple_ref/doc/uid/10000101i )。

### Preference Panes
Preference panes are used primarily to modify system preferences for the current user. Preference panes are implemented as plug-ins and installed in /Library/PreferencePanes. App developers can also take advantage of these plug-ins to manage per-user app preferences; however, most apps provide their own UI to manage preferences.

You might need to create preference panes if you create:

* Hardware devices that are user configurable

* Systemwide utilities, such as virus protection programs, that require user configuration

If you're an app developer, you might want to reuse preference panes intended for the System Preferences app or use the same model to implement your app preferences. To learn how to create and manage preference panes, read [ Preference Pane Programming Guide ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/PreferencePanes/PreferencePanes.html#//apple_ref/doc/uid/10000110i ).

### 偏好设置面板（Preference Panes）
偏好设置面板主要用于修改当前用户的系统偏好设置。偏好设置面板以插件的形式实现并且安装在`/Library/PreferencePanes`中。App开发者也可以利用这些插件去管理每个用户的的app偏好，然而大多数apps都提供它们自己的UI去管理偏好设置。

如果你创建如下形式的程序，你可能需要创建偏好设置面板：

* 用户可配置的硬件设备

* 系统范围的工具，比如需要用户进行配置的病毒防护程序。

如果你是一名app开发者，你可能想要重用SystemPreference.app中的偏好设置面板，或者使用相同的模型去实现一个你的app的偏好设置面板。要了解如何创建和管理偏好设置面板，参阅[ Preference Pane Programming Guide ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/PreferencePanes/PreferencePanes.html#//apple_ref/doc/uid/10000110i )。

### Dynamic Websites and Web Services
OS X supports a variety of techniques and technologies for creating web content. In addition to “Identity Services” and “Dashboard Widgets,” dynamic websites and web services offer web developers ways to deliver their content quickly and easily.

OS X provides support for creating and testing dynamic content in web pages. If you are developing CGI-based web apps, you can create websites using a variety of scripting technologies, including Perl and the PHP Hypertext Preprocessor (a complete list of scripting technologies is provided in “Scripts”). You can also create and deploy more complex web apps using JBoss, Tomcat, and WebObjects. To deploy your webpages, use the built-in Apache HTTP web server.

Safari provides standards-compliant support for viewing pages that incorporate numerous technologies, including HTML, XML, XHTML, DOM, CSS, Java, and JavaScript. You can also use Safari to test pages that contain multimedia content created for QuickTime, Flash, and Shockwave.

The Simple Object Access Protocol (SOAP) is an object-oriented protocol that defines a way for programs to communicate over a network. XML-RPC is a protocol for performing remote procedure calls between programs. In OS X, you can create clients that use these protocols to gather information from web services across the Internet. To create these clients, you use technologies such as PHP, JavaScript, AppleScript, and Cocoa.

If you want to provide your own web services in OS X, use WebObjects or implement the service using the scripting language of your choice. You then post your script code to a web server, give clients a URL, and publish the message format your script supports.

For information on how to create client programs using AppleScript, see[ XML-RPC and SOAP Programming Guide ]( https://developer.apple.com/library/mac/documentation/AppleScript/Conceptual/soapXMLRPC/chapter1/soapXMLRPC_intro.html#//apple_ref/doc/uid/TP30001126 ). For information on how to create web services, see WebObjects Web Services Programming Guide.

### 动态网站和web服务（Dynamic Websites and Web Services）
OS X支持各种各样创建web内容的技巧和技术。除了*“Identity”*和*“Dashboard Widgets”*之外提供这些外，动态网站和web服务也提供给开发者们很多快速简易途径。

OS X为创建和测试web页面中的动态内容提供了支持。如果你正在开发基于CGI的web应用，你可以使用各种各样的脚本技术来创建网站，包括Perl和PHP超文本预处理器（*“Scripts”*一节中提供了一分可用的脚本技术的完整列表）。你还可以使用JBoss，Tomcat和WebObjects来创建和部署更多的复杂的web应用。要部署你的网页，可使用内置的Apache HTTP web服务器。

Safari为查看包含许多技术的页面提供了与标准兼容的支持，包括HTML，XML，XHTML，DOM，CSS，Java和JavaScript。你还可以使用Safari去测试包含为QuickTime，Flash和Shockware创建的多媒体内容的页面。

简单对象存取协议（SOAP）是一个面向对象协议，该协议定义了程序之间通过网络进行通信的方式。XML-RPC是一个在程序之间执行远程程序调用的协议。在OS X中，你可以创建使用这些协议的客户端，跨越因特网去从web服务中收集信息。要创建这些客户端，你可以使用诸如PHP，JavaScript，AppleScript和Cocoa等技术。

如果你想在OS X中提供你自己的web服务，可以使用WebObjects或者使用你所选择的脚本语言去实现。随后你可以将你的脚本代码发布到web服务器上，给客户端一个URL，然后发布你的脚本支持的信息格式。

要了解如何使用AppleScript创建客户端程序，参阅[ XML-RPC and SOAP Programming Guide ]( https://developer.apple.com/library/mac/documentation/AppleScript/Conceptual/soapXMLRPC/chapter1/soapXMLRPC_intro.html#//apple_ref/doc/uid/TP30001126 )。要了解如何创建web服务，参阅*WebObjects Web Services Programming Guide*。

### Mail Stationery
The Mail app provides templates that give users prebuilt email messages that are easily customized. Because templates are HTML based, they can incorporate images and advanced formatting to give the user’s email a much more stylish and sophisticated appearance.

Developers and web designers can create custom template packages for external or internal users. Each template consists of an HTML page, a property list file, and a set of images which are packaged together in a bundle and then stored in the Mail app’s stationery folder. The HTML page and images define the content of the email message and can include drop zones for custom user content. The property list file gives Mail information about the template, such as its name, ID, and the name of its thumbnail image. To learn how to create new stationery templates, see [ Mail Programming Topics ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/MailArticles/Introduction/Introduction.html#//apple_ref/doc/uid/TP40006071 ).

### Mail Stationery
Mail.app提供了给用户预先构建容易定制的email消息的模板。因为这些模板时基于HTML的，所以它们可以包含图像和其他高级格式以此来给用户的邮件提供更加现代化和精致的内容展示。

开发者和web设计师可以为外部或内部的用户创建定制模板包。每个模板由一个HTML页面，一个plist文件，和一组一起被打包到bundle中的图像，它们随后应该存储在Mail.app的stationery文件夹中。HTML页面和图像定义了email消息的内容，并且还可以为定制用户内容而包含拖拽区域。plist文件用于给Mail.app提供关于这个模板的信息，比如模板的名字，ID和模板中缩略图的名字。要了解如何创建新的stationery模板，参阅[ Mail Programming Topics ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/MailArticles/Introduction/Introduction.html#//apple_ref/doc/uid/TP40006071 )。

### Command-Line Tools
Command-line tools are simple programs that manipulate data through a text-based interface. These tools do not use windows, menus, or other user interface elements traditionally associated with apps. Instead, they run from the command-line environment of the Terminal app. Because command-line tools require less explicit knowledge of the system to develop, they are often simpler to write than many other types of software. However, command-line tools are best suited to technically savvy users who are familiar with the conventions and syntax of the command-line interface.

Xcode supports the creation of command-line tools from several initial code bases. For example, you can create a simple and portable tool using standard C or C++ library calls, or you can create a tool more specific to OS X using frameworks such as Core Foundation, Core Services, or Cocoa Foundation.

### 命令行工具
命令行工具是一通过基于文本的界面来操纵数据的简易程序。这些工具不会使用与apps所关联的那些常见的窗口，菜单或者其他用户界面元素。取而代之的是，它们从Terminal.app的命令行环境中运行。因为命令行工具对于开发来说相对更少地需要与特定系统相关的知识，所以它们通常要比其他类型的软件更容易编写。然而，命令行工具对那些熟悉命令行界面约定和语法的技术用户却是最好的工具。

Xcode支持几个初始库来创建命令行工具。比如说你可以通过调用标准的C或C++库来创建一个简单的可移植的工具，或者你也可以使用更多针对OS X的框架来创建命令行工具，比如Core Foundation，Core Services，或者Cocoa Foundation。

### Launch Items and Daemons
Launch items are special programs that launch other programs or perform one-time operations during startup and login periods. Daemons are programs that run continuously and act as servers for processing client requests. You typically use launch items to launch daemons or perform periodic maintenance tasks, such as checking the hard drive for corrupted information.

Launch items should not be confused with the login items found in the Accounts system preferences. Login items are typically agent applications that run within a given user’s session and can be configured by that user. Launch items are not user-configurable.

Few developers should ever need to create launch items or daemons. These programs are reserved for special situations in which you need to guarantee the availability of a particular service. For example, OS X provides a launch item to run the DNS daemon. Similarly, a virus-detection program might install a launch item to launch a daemon that monitors the system for virus-like activity. In both cases, the launch item would run its daemon in the root session, which provides services to all users of the system. To learn more about launch items and daemons, see[ Daemons and Services Programming Guide ]( https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html#//apple_ref/doc/uid/10000172i ).

### 启动项和守护进程（Launch Items and Daemons）
启动项是在系统启动和登录期间启动其他程序或执行一次性草堆的特殊程序。守护进程是在系统中持续运行并且作为服务器来处理客户端请求的程序。你通常使用启动项去启动守护进程或者执行周期性的维护任务，比如说检查硬盘驱动器的损坏信息。

不应该混淆启动项与Accounts系统偏好中的登录项。登录项通常是运行在给定用户空间中的代理应用程序，其可以由用户配置。启动项则不是用户可配置的。

少数开发者需要创建启动项或者守护进程。这些程序是为你需要保证特定服务可用性的特殊情况下保留的。比如说OS X提供了一个启动项以运行DNS守护进程。类似地，一个病毒侦测程序可以安装一个启动项去启动一个监视系统中病毒活动的守护进程。在这两种情况中，启动项将会在root会话中运行他的守护进程，以将服务提供给系统的所有用户。要了解更多的关于启动项和守护进程的信息，参阅[ Daemons and Services Programming Guide ]( https://developer.apple.com/library/mac/documentation/MacOSX/Conceptual/BPSystemStartup/Chapters/Introduction.html#//apple_ref/doc/uid/10000172i )。

















