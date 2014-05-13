# About the Cocoa Document Architecture

In OS X, a Cocoa subsystem called the document architecture provides support for apps that manage documents, which are containers for user data that can be stored in files locally and in iCloud.

# 关于Cocoa文档架构

在OS X中，一个被称作文档架构（document architecture）的子系统为app管理文档提供支持，它是一个可以被存储在本地文件或者iCloud中的用户数据的容器。

![ Cocoa Document Architexture - 1 ]( http://i.imgbox.com/HbABfOKN.png)


## At a Glance

Document-based apps handle multiple documents, each in its own window, and often display more than one document at a time. Although these apps embody many complex behaviors, the **document architecture** provides many of their capabilities “for free,” requiring little additional effort in design and implementation.

## 概览

Document-based应用程序处理多个文档，每个文档都在其自己的窗口中，并且经常在同一时间显示多个文档。尽管这些应用程序包含了很多复杂的行为，但是**文档架构**“免费”提供很多他们的功能，在设计和只需要做一点额外的努力即可。

---

### The Model-View-Controller Pattern Is Basic to a Document-Based App
The Cocoa document architecture uses the **Model-View-Controller** (MVC) design pattern in which model objects encapsulate the app’s data, view objects display the data, and controller objects act as intermediaries between the view and model objects. A document, an instance of an NSDocument subclass, is a controller that manages the app’s data model. Adhering to the MVC design pattern enables your app to fit seamlessly into the document architecture.

> Relevant Chapters: [“Designing a Document-Based App”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/Designing/Designing.html#//apple_ref/doc/uid/TP40011179-CH2-SW3) and [“The Classes That Support Document-Based Apps”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)

### 模型-视图-控制器模式是Document-Based应用的基础
Cocoa文档架构使用**模型-视图-控制器**(MVC)设计模式，其中的模型对象用于封装应用程序的数据，视图对象用于显示数据，以及控制器对象扮演在视图和模型对象之间的媒介。一个文档，即一个NSDocument子类的实例，就是一个管理应用程序数据模型的控制器。遵循MVC设计模式可以使你的应用程序无缝地融入到文档架构中去。

> 相关章节：[“Designing a Document-Based App”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/Designing/Designing.html#//apple_ref/doc/uid/TP40011179-CH2-SW3)和[“The Classes That Support Document-Based Apps”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)

---

### Xcode Supports Coding and Configuring Your App
Taking advantage of the support provided by Xcode, including a document-based application template and interfaces for configuring app data, you can create a document-based app without having to write much code. In Xcode you design your app’s user interface in a graphical editor, specify entitlements for resources such as the App Sandbox and iCloud, and configure the app’s property list, which specifies global app keys and other information, such as document types.

> Relevant Chapter: [“App Creation Process Overview”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ApplicationCreationProcess/ApplicationCreationProcess.html#//apple_ref/doc/uid/TP40011179-CH6-SW5)

### Xcode支持编码及配置你的App
利用Xcode提供的包括document-based应用程序模板及配置应用数据的界面等支持，你不用写很多代码就可以创建一个document-based应用程序。在Xcode中，你可以在一个图形化的编辑器中设计你的app的用户界面，指定App沙箱和iCloud等资源的权限，以及配置app的用于指定全局app键和诸如文档类型之类的其他信息的属性列表。

> 相关章节：[“App Creation Process Overview”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ApplicationCreationProcess/ApplicationCreationProcess.html#//apple_ref/doc/uid/TP40011179-CH6-SW5)

---

### You Must Subclass NSDocument
Document-based apps in Cocoa are built around a subclass of NSDocument that you implement. In particular, you must override one document reading method and one document writing method. You must design and implement your app’s data model, whether it is simply a single text-storage object or a complex object graph containing disparate data types. When your reading method receives a request, it takes data provided by the framework and loads it appropriately into your object model. Conversely, your writing method takes your app’s model data and provides it to the framework’s machinery for writing to a document file, whether it is located only in your local file system or in iCloud.

> Relevant Chapters: [“Creating the Subclass of NSDocument”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ManagingLifecycle/ManagingLifecycle.html#//apple_ref/doc/uid/TP40011179-CH4-SW1) and [“The Classes That Support Document-Based Apps”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)

### 你必须子类化NSDocument
Cocoa中的Document-based应用程序是建立在你实现的NSDocument子类之上的。尤其是你必须重写一个文档读取方法和一个文档写入方法。你必须设计并实现你的app的数据模型，该模型可以是一个单一的文本存储对象，亦或是一个复杂的包含各种数据类型的对象图。当你的读取方法获得一个请求时，它会获得由框架提供的数据，并且适当地加载到你的对象模型中。相反，你的写入方法会获取你的app的模型数据，并将其提供给框架机制以将数据写入到文档文件中，被写入的文档文件可以仅仅在你的本地文件系统中，也可以在iCloud中。

> 相关章节：[“Creating the Subclass of NSDocument”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ManagingLifecycle/ManagingLifecycle.html#//apple_ref/doc/uid/TP40011179-CH4-SW1)和[“The Classes That Support Document-Based Apps”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)








