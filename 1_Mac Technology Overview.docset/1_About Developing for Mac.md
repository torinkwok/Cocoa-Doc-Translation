# About Developing for Mac
The OS X operating system combines a stable core with advanced technologies to help you deliver world-class products on the Mac platform. Knowing what these technologies are, and how to use them, can help streamline your development process, while giving you access to key OS X features.

# 关于Mac开发
OS X操作系统结合了稳定的内核和先进的技术，以帮助你在Mac平台上去实现**世界级**的产品。了解这些技术是什么以及如何使用它们，可以帮助你在接触OS X的关键特性时简化开发流程。

![ Mac ]( http://cl.ly/image/1s3t0D3E1Z40/MacBookProDesktop_2x.png )

## At a glance
This guide introduces you to the range of possibilities for developing Mac software, describes the many technologies you can use for software development, and points you to sources of information about those technologies. It does not describe user-level system features or features that have no impact on software development.

## 概述
这份指南向你介绍了Mac程序开发的各种可能性，描述了很多你会使用到的开发技术，并且向你指出关于这些技术信息的来源。这份指南不会描述**用户层的**的系统特性或者与软件开发无关的特性。


### OS X Has a Layered Architecture with Key Technologies in Each Layer
It’s helpful to view the implementation of OS X as a set of layers. The lower layers of the system provide the fundamental services on which all software relies. Subsequent 
layers contain more sophisticated services and technologies that build on (or complement) the layers below.

### OS X拥有一个分层的体系结构
将OS X实现视为一系列的层次对于学习它很有帮助。底层的系统提供了其他软件所赖以为生的基本服务。随后的层次包含了更高级的依赖于更低层的服务和技术。

![ Layers of OS X ]( http://cl.ly/image/0103100H1u1W/osx_architecture-layers_2x.png )

The lower the layer a technology is in, the more specialized are the services it provides. Generally, technologies in higher layers incorporate lower-level technologies to provide common app behaviors. A good rule of thumb is to use the highest-level programming interface that meets the goals of your app. Here is a brief summary of the layers of OS X.

* The Cocoa (Application) layer includes technologies for building an app’s user interface, for responding to user events, and for managing app behavior.
* The Media layer encompasses specialized technologies for playing, recording, and editing audiovisual media and for rendering and animating 2D and 3D graphics.
* The Core Services layer contains many fundamental services and technologies that range from Automatic Reference Counting and low-level network communication to string manipulation and data formatting.
* The Core OS layer defines programming interfaces that are related to hardware and networking, including interfaces for running high-performance computation tasks on a computer’s CPU and GPU.
* The Kernel and Device Drivers layer consists of the Mach kernel environment, device drivers, BSD library functions (libSystem), and other low-level components. The layer includes support for file systems, networking, security, interprocess communication, programming languages, device drivers, and extensions to the kernel.


> Relevant Chapters: “Cocoa Application Layer,” “Media Layer,” “Core Services Layer,” “Core OS Layer,” “Kernel and Device Drivers Layer”


技术越底层，提供的服务就越有针对性。通常地，较高层的技术涵盖较低层的技术以提供通用的app行为。一个好的经验法则是尽量使用能够达到你的app的目的的众多编程接口中层次最高的那一个。如下是一个关于OS X分层的小结：

* ***Cocoa（Application)***层涵盖了创建app的用户界面，响应用户事件以及管理app行为的各种技术。
* ***媒体层（Media)***包含了专门针对播放，录制，编辑视听媒体以及渲染2D和3D图形以及制作2D和3D动画的各种技术。
* ***核心服务层（Core Services)***包含了从 **自动引用技术（ARC）**和底层网络通信技术到字符串操作和数据格式处理等许多基本的服务和技术。
* ***核心操作系统层（Core OS）***定义了与硬件和网络相关的编程接口，包括使用CPU和GPU执行高性能计算任务的编程接口。
* ***内核和设备驱动层（Kernel and Device Drivers）***由Mach内核环境，设备驱动，BSD库函数（libSystem），以及其他底层组件等组成。这一层包含了对文件系统，网络，安全，进程间的通信，编程语言，设备驱动，以及内核扩展的支持。


> 相关章节： “Cocoa Application Layer,” “Media Layer,” “Core Services Layer,” “Core OS Layer,” “Kernel and Device Drivers Layer”


### You Can Create Many Different Kinds of Software for Mac
Using the developer tools and system frameworks, you can develop a wide variety of software for Mac, including the following:

* __Apps.__ Apps help users accomplish tasks that range from creating content and managing data to connecting with others and having fun. OS X provides a wealth of system technologies that you can use to extend the capabilities of your apps and enhance the experience of your users.
* __Frameworks and libraries.__ Frameworks and libraries enable code sharing among apps.
* __Command-line tools and daemons.__ Command-line tools allow sophisticated users to manipulate data in the command-line environment of the Terminal app. Daemons typically run continuously and act as servers for processing client requests.
* __App plug-ins and loadable bundles.__ Plug-ins extend the capabilities of other apps; bundles contain code and resources that apps can dynamically load at runtime.
* __System plug-ins.__ System plug-ins, such as audio units, kernel extensions, I/O Kit device drivers, preference panes, Spotlight importers, and screen savers, extend the capabilities of the system.


> Relevant Chapter: “Creating Software Products for the Mac Platform”


### 你可以为Mac创建很多不同类型的软件
使用SDK和系统框架，你可以为Mac开发五花八门的软件，包括下面这些：

* __Apps.__  Apps帮助用户完成从创建内容和管理数据到与其他用户连接计算机进行娱乐等各种任务。OS X提供了大量你可以用于扩展apps功能以及增强用户体验的技术。
* __Frameworks and libraries.__ 框架和库允许在不同app之间共享代码。
* __Command-line tools and daemons.__ 命令行工具允许经验丰富的高级用户在Terminal.app的命令行环境中操纵数据。守护进程通常持续运行并且以服务器的形式响应客户端的请求。
* __App plug-ins and loadable bundles.__ Plug-ins扩展其他apps的功能。Bundles包含apps在运行时动态加载的代码和资源。
* __System plug-ins__ 像音频装置，内核扩展，I/O组件，设备驱动，偏好设置面板，Spotlight导入器以及屏幕保护等插件扩展了系统的功能。



> 相关章节： “Creating Software Products for the Mac Platform”


### When Porting a Cocoa Touch App, Be Aware of API Similarities and Differences
The technology stacks on which Cocoa and Cocoa Touch apps are based have many similarities. Some system frameworks are identical (or nearly identical) in each platform, including Foundation, Core Data, and AV Foundation. This commonality of API makes some migration tasks—for example, porting the data model of your Cocoa Touch app—easy.

Other migration tasks are more challenging because they depend on frameworks that reflect the differences between the platforms. For example, porting controller objects and revising the user interface are more demanding tasks because they depend on AppKit and UIKit, which are the primary app frameworks in the Cocoa and CocoaTouch layers, respectively.


> Relevant Chapter: “Migrating from Cocoa Touch”


### 当移植一个Cocoa-Touch应用时，要了解API之间的异同
Cocoa和Cocoa-Touch有许多相似之处。甚至一些系统框架在两个平台上时完全相同（或几乎相同）的，包括Foundation，Core Data以及AV Foundation框架。两个API之间的共性使得迁移工作——比如移植你的Cocoa-Touch应用的数据模型——变得很容易。

其他的迁移工作更具有挑战性，因为它们依赖于能反映出平台差异的框架。比方说，移植控制器对象和校正用户界面都是很吃力的工作，因为它们分别依赖于Cocoa和CocoaTouch层各自的首要app框架：AppKit和UIKit。


> 相关章节： “Migrating from Cocoa Touch”


## See Also

Apple provides developer tools and additional information that support your development efforts.

Xcode, Apple’s integrated development environment, helps you design, create, debug, and optimize your software. You can download Xcode from the Mac App Store.

For an overview of the developer tools for OS X, see the [ Xcode 5 Apple Developer webpage ]( https://developer.apple.com/xcode/ ). To learn how to use Xcode 5, read [ Xcode Overview ](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215 ).

The OS X Developer Library contains the documentation, sample code, tutorials, and other information you need to write OS X apps. You can access the OS X Developer Library from the [ Apple Developer website ]( https://developer.apple.com/library/mac/navigation/ ) or from Xcode. In Xcode, choose *Help* > *Documentation and API Reference* to view documents and other resources in the Organizer window.

In addition to the OS X Developer Library, there are other sources of information on developing different types of software for Mac:

* **Apple Open Source.** Apple makes major components of OS X—including the UNIX core—available to the developer community. To learn about Apple’s commitment to Open Source development, visit Open Source Development Resources. To learn more about some specific Open Source projects, such as Bonjour and WebKit, visit Mac OS Forge.
* **BSD.** Berkeley Software Distribution (BSD) is an essential UNIX-based part of the OS X kernel environment. Several excellent books on BSD and UNIX are available in bookstores. But you can also find additional information on any of the websites that cover BSD variants—for example, The FreeBSD Project.
* **Third-party books.** Several excellent books on Mac app development can be found online and in the technical sections of bookstores.

## 另请参阅
Apple提供了支持你开发工作的开发工具和更多的信息。

Xcode，Apple公司的**集成开发环境（IDE）**，帮助你设计，创建，调试，优化你的软件。你可以从App Store下载Xcode。

关于OS X开发工具的概述，请参阅[ Xcode 5 Apple Developer webpage ]( https://developer.apple.com/xcode/ )。要学习如何使用Xcode 5，请阅读[ Xcode Overview ](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215 )。

OS X开发者库包含了文档，事例代码，指导，以及其他你编写OS X应用时所需的信息。你可以从[ Apple Developer website ]( https://developer.apple.com/library/mac/navigation/ )或者Xcode访问OS X开发者库。在Xcode中，选择*Help* > *Documentation and API Reference* 以在Organizer窗口中查看文档和其他资源。

除了OS X开发者库之外，下面是其他关于为Mac开发软件的信息的不同类型资源：

* **Apple Open Source.** Apple makes major components of OS X—including the UNIX core—available to the developer community. To learn about Apple’s commitment to Open Source development, visit Open Source Development Resources. To learn more about some specific Open Source projects, such as Bonjour and WebKit, visit Mac OS Forge.
* **BSD.** Berkeley Software Distribution (BSD) is an essential UNIX-based part of the OS X kernel environment. Several excellent books on BSD and UNIX are available in bookstores. But you can also find additional information on any of the websites that cover BSD variants—for example, The FreeBSD Project.
* **Third-party books.** Several excellent books on Mac app development can be found online and in the technical sections of bookstores.







