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

* **Input methods.** A common example of an input method is an interface for typing Japanese or Chinese characters using multiple keystrokes. Other examples of input methods include spelling checkers and pen-based gesture recognition systems. You can create input methods using Input Method Kit (InputMethodKit.framework). For information on how to use this framework, see Input Method Kit Framework Reference.

* **Metadata importers.** Spotlight relies on metadata importers to gather information about the user’s files and to build a systemwide index. Spotlight uses this index to help users find information by searching on attributes that make sense to them, such as the duration of a video or the dimensions of an image. If your app defines a custom file format, you should always provide a metadata importer for that file format. (If your app relies on commonly used file formats, such as JPEG, RTF, or PDF, the system provides a metadata importer for you.) To learn how to create metadata importers, see Spotlight Importer Programming Guide.

* **Quartz Composer plug-ins.** Quartz Composer supports a plug-in mechanism that allows you to create a custom patch and make it available in the Quartz Composer workspace and to most Quartz Composer clients. (A patch is processing unit that performs a specific task, such as processing a string or rendering an OpenGL texture.) To learn how to create a Quartz Composer plug-in, see Quartz Composer Custom Patch Programming Guide.

* **Quick Look plug-ins.** A Quick Look plug-in—also known as a Quick Look generator—converts a document from its native format into a format that Quick Look can display to users. If your app creates documents of a nonstandard or private type, it’s a good idea to provide a Quick Look generator so that users can get previews of these documents in Quick Look. To learn how to create a Quick Look plug-in, see Quick Look Programming Guide.

* **Safari plug-ins.** Safari supports the Netscape-style plug-in model for incorporating additional types of content in the web browser. In Safari in OS X v10.7 and later, these plug-ins run in their own process, which improves the stability and security of Safari. Netscape-style plug-ins include support for onscreen drawing, event handling, and networking and scripting functions.

### 插件

插件是对众多apps和系统行为进行扩展的标准方式。一个插件其实就是一个可以由一个app在运行时动态加载的bundle。因为它是被动态加载的，所以用户可以直接添加或者移除一个插件。

下方列出的app和系统插件向你展示了开发插件的众多可能性：

* **地址簿动作插件。** 一个地址簿动作插架允许你添加能够作用于某一个人的地址簿卡片数据的行为。举个例子：已经存在的*Large Type*动作就以large type的形式去显示用户选中的电话号码。如果需要任何其他动作，必须运行你的app来执行该动作。想要了解如何创建地址簿动作插件，参阅“[ Creating and Using Address Book Action Plug-ins ]( https://developer.apple.com/library/mac/documentation/UserExperience/Conceptual/AddressBook/Tasks/Actions.html#//apple_ref/doc/uid/20001681 )”。

* **App插件。** App插件可以扩展任何支持插件模型的app的功能。除了第三方应用之外，几个Apple公司的app也同样支持插件，比如iTunes.app， Final Cut Pro.app，以及Aperture.app。想了解更多有关为Apple的应用开发插件的信息，请访问[ Apple Developer website ]( https://developer.apple.com/ )站点。

*  **Automator插件。** 使用Automator插件，你可以扩展Automator默认支持的动作集，一个工具型app通常都允许用户通过与定义的动作调板组合各种复杂的脚本。Automator插件可以使用AppleScript或者Objective-C编写，所以你可以为你自己的app或者其他支持脚本apps添加特性编写它们。（为你的app的最通用的功能提供Automator插件是一个很棒的注意，因为这样可以给予用户更多的与你的app交互的方式）。想了解如果编写Automator插件，参阅[ Automator Programming Guide ]( https://developer.apple.com/library/mac/documentation/AppleApplications/Conceptual/AutomatorConcepts/Automator.html#//apple_ref/doc/uid/TP40001450 )。

*  **Core Audio plug-ins.** 核心音频插件可以提供在大多数处理阶段中对音频流的操作。举个例子：你可以使用核心音频插件去生成，处理或者接收一个音频流或者与一个音频相关的硬件设备进行交互。想要了解Core Audio，参阅 [ Core Audio Overview ]( https://developer.apple.com/library/mac/documentation/MusicAudio/Conceptual/CoreAudioOverview/Introduction/Introduction.html#//apple_ref/doc/uid/TP40003577 )。












