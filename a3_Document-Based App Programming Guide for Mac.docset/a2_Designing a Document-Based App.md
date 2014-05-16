# Designing a Document-Based App

Documents are containers for user data that can be stored in files locally and in iCloud. In a document-based design, the app enables users to create and manage documents containing their data. One app typically handles multiple documents, each in its own window, and often displays more than one document at a time. For example, a word processor provides commands to create new documents, it presents an editing environment in which the user enters text and embeds graphics into the document, it saves the document data to disk or iCloud, and it provides other document-related commands, such as printing and version management. In Cocoa, the document-based app design is enabled by a subsystem called the **document architecture**, which is part of of the AppKit framework.

# 设计Document-Based应用

文档是可以被存储在本地文件中和iCloud中的用户数据的容器。在document-based设计中，app使得用户能够创建和管理包含他们数据的文档。一个app通常会处理多个文档，每个文档都处在其自己的窗口中，并且经常在同一时间显示多个文档。比如说：一个字处理程序就提供了用于创建新文档的命令，其提供了一个用户向文档中输入文本及嵌入图像得编辑环境，该程序还将文档数据保存到磁盘或者iCloud中，并且它还提供了其他文档相关的命令，比如打印（printing）和版本管理（version managment）。在Cocoa中，document-based应用设计通过一个被叫做**文档架构**得子系统来实现，该架构也是AppKit框架得一部分。



## Documents in OS X

There are several ways to think of a document. Conceptually, a document is a container for a body of information that can be named and stored in a file. In this sense, the document is an object in memory that owns and manages the document data. To users, the document is their information—such as text and graphics formatted on a page. In the context of Cocoa, a document is an instance of a custom NSDocument subclass that knows how to represent internally persistent data that it can display in a window. This document object knows how to read document data from a file and create an object graph in memory for the document data model. It also knows how to modify that data model consistently and write the document data back out to disk. So, the document object mediates between different representations of document data, as shown in Figure 1-1.

**Figure 1-1**  Document file, object, and data model

Using iCloud, documents can be shared automatically among a user’s computers and iOS devices. The system synchronizes changes to the document data without user intervention. See **“Storing Documents in iCloud”** for more information.

## OS X中的文档

有几种理解文档的方式。从概念上说，一个文档就是一个可以被命名和存储在文件中的信息体的容器。从这个意义上说，文档是一个内存中的对象，其拥有并管理文档数据。对于用户而言，文档是他们的信息——比如一个格式化文本和图像的页面。在Cocoa环境中，一个文档是一个自定义的NSDocument子类的实例，该实例知道如何在内部展现可以被显示在窗口中的持久化数据。该文档对象知道如何从一个文件中读取文档数据并在内存中为文档数据模型创建对象图。它还知道如何一致地修改数据模型并将文档数据写回到磁盘中。所以，文档对象在文档数据不同的表现形式之间进行协调，如Figure 1-1所示。

使用iCloud，文档可以自动在用户的计算机和iOS设备之间共享。系统会无须用户干涉地同步更改到文档数据。参阅**“Storing Documents in iCloud”**以了解更多信息。

**Figure 1-1**  文档文件，对象以及数据模型

![Figure 1-1](http://i.imgbox.com/PsIRvNJm.png)

使用iCloud使得文档能够在用户的计算机和iOS设备之间自动地被共享。系统会在不需要用户干预的情况下同步更改到文档数据。更多信息请参阅**“Storing Documents in iCloud”**。



## The Document Architecture Provides Many Capabilities for Free

The document-based style of app is one design choice among several that you should consider when you design your app. Other choices include single-window utility apps, such as Calculator, and library-style “shoebox” apps, such as iPhoto. It’s important to choose the basic app style early in the design process because development takes quite different paths depending on that choice. If it makes sense for your users to create multiple discrete sets of data, each of which they can edit in a graphical environment and store in files, then you should plan to develop a document-based app.

The Cocoa document architecture provides a framework for document-based apps to do the following things:

* **Create new documents.** The first time the user chooses to save a new document, it presents a dialog in which the user names and saves the document in a disk file in a user-chosen location.

* **Open existing documents stored in files.** A document-based app specifies the types of document files it can read and write, as well as read-only and write-only types. It can represent the data of different document types internally and display the data appropriately.

* **Automatically save documents.** Document-based apps can adopt autosaving in place, and its documents are automatically saved at appropriate times so that the data the user sees on screen is effectively the same as that saved on disk. Saving is done safely, so that an interrupted save operation does not leave data inconsistent. To avoid automatic saving of inadvertent changes, old files are locked from editing until explicitly unlocked by the user.

* **Asynchronously read and write document data.** Reading and writing are done asynchronously on a background thread, so that lengthy operations do not make the app’s user interface unresponsive. In addition, reads and writes are coordinated using the NSFilePresenter protocol and the NSFileCoordinator class to reduce version conflicts.

* **Manage multiple versions of documents.** Autosave creates versions at regular intervals, and users can manually save a version whenever they wish. Users can browse versions and revert the document’s contents to a chosen version using a Time Machine–like interface. The version browser is also used to resolve version conflicts from simultaneous iCloud updates.

* **Print documents.** Users can specify various page layouts in the print dialog and page setup dialog.

* **Track changes and set the document’s edited status.** The document manages its edited status and implements multilevel undo and redo.

* **Validate menu items.** The document enables or disables menu items automatically, depending on its edited status and the applicability of the associated action methods.

* **Handle app and window delegation.** **Notifications** are sent and **delegate** methods called at significant life cycle events, such as when the app terminates.

Cocoa’s document architecture implements most of its capabilities in three classes. These classes interoperate to provide an extensible app infrastructure that makes it easy for you to create document-based apps. Table 1-1 briefly describes these classes.

Table 1-1  Primary classes in the document architecture

Class                | Purpose
-------------------- | --------------------------------------------------
NSDocument           | Creates, presents, and stores document data
NSWindowController   | Manages a window in which a document is displayed
NSDocumentController | Manages all of the document objects in the app

> See [“The Classes That Support Document-Based Apps”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2) for more detailed information.

## 文档架构免费提供了许多功能

应用程序的document-based风格是当你在设计app时应该考虑的几种设计选择中的一个。其他的选择包括像Calculator.app这样的单一窗口（single-window）工具型app，以及像iPhoto.app这样的图书馆风格（library-style)“shoebox”应用。在设计早起选择基本的app风格是很重要的，开发工作会因为选中的不同的风格而进入完全不同的轨道。如果你的用户可以创建多个分散的数据集合，并且每个数据集合都可以由用户在图形化的环境中进行编辑并存储在文件中，那么你应该考虑开发document-based应用。

Cocoa文档架构为document-based应用提供了一个框架以做到如下事情：

* **创建新文档。** 第一次用户选择保存一个新的文档，其提供了一个对话框的用户名并将文档以磁盘文件的形式保存在用户选择的位置。

* **打开存储在文件中的已存在文档** 一个document-based应用会指定其可以读写的文档文件类型，以及只读（read-only)和只写（write-only）的文档文件类型。它可以在内部展示不同文档类型的数据并且合理地显示这些数据。

* **自动保存文档。** Document-based应用可以在适当的地方采用自动保存，并且它的文档在适当的时间会被自动保存，以便用户在屏幕上看到的数据与磁盘中的数据是一致的。保存是操作安全的，所以一个被打断的的保存操作不会留下不一致的数据。为避免无意操作的自动保存，旧的文件在编辑开始时会被锁定直到用户显示地解锁。

* **异步读写文档数据。**  读取和写入是在后来线程中异步完成的，这是为了长时间的操作不会使得用户界面失去响应。此外，使用NSFilePresenter协议和NSFileCoordinator类来协调读写操以减少版本冲突。

* **管理文档的多个版本。** 自动保存会在定期创建版本，并且用户可以随时手动保存版本。用户可以使用类似Time Machine的界面来浏览版本以及将文档内容还原到选中的历史版本。版本浏览器还用于从同步的iCloud更新中解决版本冲突。

* **打印文档。** 用户可以在打印对话框和页面设置对话框中指定不同的页面布局。

* **跟踪改变以及设置文档的编辑状态。** 文档管理它的编辑状态并实现了多层次的撤掉和重做。

* **验证菜单项。** 文档会自动启用或禁用菜单项，这取决于文档的编辑状态以及与菜单项关联的动作（action）方法的适用性。

* **处理应用和窗口委托。** 在诸如应用终止这类重要的生命周期事件发生时，会发送**通知**以及调用**委托**方法。

在三个类中实现了Cocoa的文档架构大部分的功能。这些类互相操作以提供一个可扩展的应用架构，其使得创建document-based应用很容易。表1-1中简要地描述了这些类。

表1-1 文档架构中的主要类

类（class）           | 用途（purpose）
-------------------- | -----------------------
NSDocument           | 创建，提供以及存储文档数据
NSWindowController   | 管理用于显示文档的窗口
NSDocumentController | 管理app中所有的文档对象

> 更多详细信息参见：[“The Classes That Support Document-Based Apps”。](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)



## Storing Documents in iCloud

The iCloud storage technology enables you to share documents and other app data among multiple computers that run your document-based app. If you have a corresponding iOS version of your app, you can share your documents and app data with your iOS devices as well. Once your app sets up the proper connections, iCloud automatically pushes documents and changes to all the devices running an instance of your app with no explicit user intervention.

There are two kinds of storage in iCloud: **document storage** and **key-value data storage**. Document storage is designed for storing large amounts of data such as that in a document file. Key-value storage is designed for small amounts of app data such as configuration data. For example, you might store the text and illustrations for a book in **document storage**, and you might store the reader’s page location in **key-value storage**. That way, whenever the user opens the document on any device, the correct page is displayed.

Documents and key-value data designated for storage in iCloud are transferred to iCloud and to the user’s other computers as soon as possible. On iOS devices, only file metadata is transferred from iCloud to devices as soon as possible, while the file data itself is transferred on demand. Once data has been stored initially in iCloud, only changes are transferred thereafter, to make synchronization most efficient.

**NSDocument** implements file coordination, version management, and conflict resolution among documents, so it provides the easiest path to using iCloud. For details explaining how to handle document storage in iCloud, see [“Moving Document Data to and from iCloud.”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ManagingLifecycle/ManagingLifecycle.html#//apple_ref/doc/uid/TP40011179-CH4-SW2)

## 在iCloud中存储文档

iCloud存储技术使得你可以在多台运行你的document-based应用的计算机之间共享文档和其他应用程序数据。如果你有一个你的app对应的iOS版本，那么你也可以使用你的iOS设备来共享你的文档和应用程序数据。一旦你的应用程序创建了适当的连接，iCloud会自动推送文档，并且会在没有用户干预的情况下改变所有运行你的app的设备。

iCloud中有两种类型的存储：**文档存储**和**键值数据存储**。文档存储被设计为存储像文档文件这样的大量数据。键值数据存储被设计为存储像配置文件这类的应用程序的小量数据。举个例子，你可以将一本书中的文本和插图存储到**文档存储**中，并且可以将阅读器的页面位置存储在**键值存储**中。那样，用户在任何时间任何地点打开该文档时，都会显示正确的页面。

被指定为存储在iCloud中的文档和键值数据会被尽快地转存到iCloud和用户的其他计算机中。在iOS设备上，当文件数据自己被转存时，只有文件元数据会被尽快地从iCloud转存到设备中。一旦数据被第一次存储在iCloud中，从那以后只有改变会被转存，以做到最有效的同步。

**NSDocument**实现了文件协调，版本管理以及文档之间的冲突解决，所以它提供了使用iCloud最简单的途径。关于如何在iCloud中处理文档存储的详细解释，参阅：[“Moving Document Data to and from iCloud.”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ManagingLifecycle/ManagingLifecycle.html#//apple_ref/doc/uid/TP40011179-CH4-SW2)



## The Document Architecture Supports App Sandbox

The document architecture helps document-based apps adopt App Sandbox, an access control technology that provides a last line of defense against stolen, corrupted, or deleted user data if malicious code exploits your app. The **NSDocument** class automatically works with Powerbox to make items available to your app when the user opens and saves documents or uses drag and drop. **NSDocument** also provides support for keeping documents within your sandbox if the user moves them using the Finder. For more information about App Sandbox, see [App Sandbox Design Guide.](https://developer.apple.com/library/mac/documentation/Security/Conceptual/AppSandboxDesignGuide/AboutAppSandbox/AboutAppSandbox.html#//apple_ref/doc/uid/TP40011183)

## 文档架构支持应用沙箱（App Sandbox）

文档架构帮助document-based应用采用应用沙箱（App Sandbox）——一个当恶意代码利用的你app时，提供防止偷窃，损坏或者删除用户数据的最后一道防线的访问控制技术（access control technology）。当用户打开和保存文档或者使用拖放功能时，**NSDocument**类会自动地和Powerbox一起工作以使项可用于你的应用。如果用户使用Finder来移动文档，**NSDocument**也提供了在你的沙箱中保持这些文档的支持。更多关于应用沙箱的信息，参阅：[App Sandbox Design Guide。](https://developer.apple.com/library/mac/documentation/Security/Conceptual/AppSandboxDesignGuide/AboutAppSandbox/AboutAppSandbox.html#//apple_ref/doc/uid/TP40011183)



## Considerations for Designing Your Document Data Model

Your document data model is an object or graph of interconnected objects that contain the data displayed and manipulated by your document objects.

## 考虑设计你的文档数据模型（Document Data Model）

你的文档数据模型（document data model）是一个对象或者互相连接的对象图，其包含由你的文档对象显示和操作的数据。

---

### Cocoa Uses the Model-View-Controller Design Pattern
The Cocoa document architecture and many other technologies throughout Cocoa utilize the Model-View-Controller (MVC) design pattern. **Model objects** encapsulate the data specific to an app and manipulate and process that data. **View objects** display data from the app’s model objects and enable the editing of that data by users. **Controller objects** act as intermediaries between the app’s view objects and model objects. By separating these behaviors into discrete objects, your app code tends to be more reusable, the object interfaces are better defined, and your app is easier to maintain and extend. Perhaps most importantly, MVC-compliant app objects fit seamlessly into the document architecture.

### Cocoa使用模型（Model）-视图（View）-控制器（Controller）设计模式
Cocoa文档架构和许多其他的技术中到处都在使用模型-视图-控制器（MVC）设计模式。**模型对象**封装了特定于应用的数据并负责操作和处理这些数据。**视图对象**负责从应用的模型对象来显示数据并且允许用户编辑这些数据。**控制器对象**则在应用的视图对象和模型对象之间担任媒介。通过将这些行为分离到具体的对象中，你的应用的代码会更加趋于可重用，对象接口会被更好地定义，以及你的应用会更容易去维护和扩展。可能最重要的是，遵循MVC模式的应用程序会无缝地融合到文档架构中。

---

### A Data Model Corresponds to a Document Type
A document object is a controller dedicated to managing the objects in the document’s data model. Each document object is a custom subclass of NSDocument designed specifically to handle a particular type of data model. Document-based apps are able to handle one or more types of documents, each with its own type of data model and corresponding NSDocument subclass. Apps use an information property list file, which is stored in the app’s bundle and named, by default, <appName>-Info.plist, to specify information that can be used at runtime. Document-based apps use this property list to specify the document types the app can edit or view. For example, when the NSDocumentController object creates a new document or opens an existing document, it searches the property list for such items as **the document class that handles a document type**, **the uniform type identifier (UTI) for the type**, and **whether the app can edit or only view the type**. For more information about creating a property list for types of documents, see [“Complete the Information Property List.”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ApplicationCreationProcess/ApplicationCreationProcess.html#//apple_ref/doc/uid/TP40011179-CH6-997699)

### 一个数据模型对应于一个文档类型
一个文档对象就是一个专用于管理文档数据模型的对象的控制器。每个文档对象都是一个NSDocument类自定义的子类，其专门被设计用于处理特定数据模型类型的。文档驱动型应用可以处理一个或多个文档类型，每个都有它自己的数据模型类型以及对应的NSDocument子类。应用使用一个被存储在应用的bundle中并且默认命名为*<appname>-Info.plist*的信息属性列表文件，用于在运行时指定会被使用到的信息。文档驱动型应用使用该属性列表以指定该应用程序可以编辑或浏览的文档类型。比如说：当NSDocumentController对象创建了一个新的文档或者打开了一个已存在的文档时，它会在属性列表中搜索**处理某一个文档类型的文档类**，**统一类型标识符（UTI）**，以及**该应用程序可以编辑还是只能浏览该类型的文档**等项。更多关于为文档类型创建属性列表的信息，参阅：[“Complete the Information Property List。”](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/ApplicationCreationProcess/ApplicationCreationProcess.html#//apple_ref/doc/uid/TP40011179-CH6-997699)

---

### Data Model Storage
Any objects that are part of the persistent state of a document should be considered part of that document’s model. For example, the Sketch sample app has a subclass of NSDocument named SKTDocument. Objects of this class have an array of SKTGraphic objects containing the data that defines the shapes Sketch can draw, so they form the data model of the document. Besides the actual SKTGraphic objects, however, the SKTDocument object contains some additional data that should technically be considered part of the model, such as the order of the graphics within the document’s array, which determines the front-to-back ordering of the SKTGraphic objects.

Like any document-based app, Sketch is able to write the data from its data model to a file and vice versa. The reading and writing are the responsibility of the SKTDocument object. Sketch implements the NSDocument data-based writing method that flattens its data model objects into an NSData object before writing it to a file. Conversely, it also implements the data-based NSDocument reading method to reconstitute its data model in memory from an NSData object it reads from one of its document files.

There are three ways you can implement data reading and writing capabilities in your document-based app:

* **Reading and writing native object types.** NSDocument has methods that read and write NSData and NSFileWrapper objects natively. You must override at least one writing method to convert data from the document model’s internal data structures into an NSData object or NSFileWrapper object in preparation for writing to a file. Conversely, you must also override at least one reading method to convert data from an NSData or NSFileWrapper object into the document model’s internal data structures in preparation for displaying the data in a document window. See *“Creating the Subclass of NSDocument”* for more details about document reading and writing methods.

* **Using Core Data.** If you have a large data set or require a managed object model, you may want to use NSPersistentDocument to create a document-based app that uses the Core Data framework. Core Data is a technology for object graph management and persistence. One of the persistent stores provided by Core Data is based on SQLite. Although Core Data is an advanced technology requiring an understanding of Cocoa fundamental design patterns and programming paradigms, it brings many benefits to a document-based app, such as:

    1. Incremental reading and writing of document data
    
    2. Data compatibility for apps with iOS and OS X versions
    
    For more information, see Core Data Starting Point.
    
* **Custom object formats.** If you need to read and write objects without using NSData and NSFileWrapper, you can override other NSDocument methods to do so, but your code needs to duplicate what NSDocument does for you. Naturally, this means your code will have greater complexity and a greater possibility of error.


### 数据模型存储
任何作为文档持续状态的一部分的对象，都应该被认为是文档模型的一部分。举个例子，Sketch事例应用就拥有一个叫做SKDocument的NSDocument子类。该类的对象拥有一个SKTGraphic对象的数组，该数组用来包含定义了Sketch可绘制形状的数据。然而除了实际的SKTGraphic对象，SKTDocument还包含了一些从技术上应该被考虑为模型的一部分的额外数据，比如像在文档的数组中图形的顺序，其决定了SKTGraphic对象从前到后的顺序。

就像任何文档驱动的应用一样，Sketch也允许将数据从数据模型写到文件中，反之亦然。读取和写入都是SKTDocument对象的责任。Sketch实现了NSDocument基于数据的写入方法，该方法在将数据模型写入到文件之前将它的数据模型冻结到一个NSData对象中。反过来，它也实现了基于数据的NSDocument读取方法，以在内存中将从它从文档文件中读取出来的NSData对象重建成它的数据模型。

你可以通过三种途径来在你的文档驱动应用中实现读写操作：

* **读取和写入原始对象类型。** NSDocument自带用于读写NSData和NSFileWrapper对象的方法。你必须覆写至少一个写方法以将数据从文档模型的内部数据结构转换成一个NSData对象或者NSFileWrapper对象，以此来为写入到文件做准备。反过来，你也必须实现至少一个读方法以将数据从NSData或者NSFileWrapper对象转换成文档模型的内部数据结构，以此来为将数据显示在文档窗口中来做准备。参阅*“Creating the Subclass of NSDocument”*以了解关于文档读写方法更详细的信息。

* **使用Core Data。** 如果你拥有一个庞大的数据集或者需要托管对象模型，你可能想要使用NSPersistentDocuemnt以创建使用Core Data框架的文档驱动应用。Core Data是一个用于对象图管理及持久化的技术。由Core Data提供的持久化存储技术中的一个，是基于SQLite的。尽管Core Data是一门需要对Cocoa基本的设计模式和编程范式有所了解的技术，但是它的确使文档驱动程序很受益，比如说：

    1. 文档数据的更多的读写方法。
    
    2. iOS版的和OS X版的应用之间的数据兼容性。
    
* **定制对象格式。** 如果你需要不使用NSData和NSFileWrapper来读写对象，你可以重写其他的NSDocument方法来做到，但是你的代码将会需要去重做很多NSDocument为你做过的事情。自然而然地，这意味着你的代码会拥有更多的复杂性和更多出错的可能。

---

### Handling a Shared Data Model in OS X and iOS
Using iCloud, a document can be shared between document-based apps in OS X and iOS. However, there are differences between the platforms that you must take into consideration. For an app to edit the same document in iOS and OS X, the document-type information should be consistent. Other cross-platform considerations for document-data compatibility are:

* Some technologies are available on one platform but not the other. For example, if you use rich text format (RTF) as a document format in OS X, it won’t work in iOS because its text system doesn’t have built-in support for rich text format (although you can implement that support in your iOS app).

* The default coordinate system for each platform is different, which can affect how content is drawn. See “Default Coordinate Systems and Drawing in iOS” in *Drawing and Printing Guide for iOS* for a discussion of this topic.

* If you archive a document’s model object graph, you may need to perform suitable conversions using NSCoder methods when you encode and decode the model objects.

* Some corresponding classes are incompatible across the platforms. That is, there are significant differences between the classes representing colors (UIColor and NSColor), images (UIImage and NSImage), and Bezier paths (UIBezierPath and NSBezierPath). NSColor objects, for example, are defined in terms of a color space (NSColorSpace), but there is no color space class in UIKit.

These cross-platform issues affect the way you store document data in the file that is shared between OS X and iOS as an iCloud document. Both versions of your app must be able to reconstitute a usable in-memory data model that is appropriate to its platform, using the available technologies and classes, without losing any fidelity. And, of course, both versions must be able to convert their platform-specific data model structures into the shared file format.

One strategy you can use is to drop down to a lower-level framework that is shared by both platforms. For example, on the iOS side, UIColor defines a CIColor property holding a Core Image object representing the color; on the OS X side, your app can create an NSColor object from the CIColor object using the *colorWithCIColor:* class method.

使用iCloud，一个文档可以在OS X和iOS上得文档驱动应用之间被共享。然而，在平台之间有一些你必须考虑到的不同。对于一个在iOS和OS X上编辑相同文档的应用，文档类型信息应该被考虑到。其他的一些关于文档格式兼容性的跨平台注意事项：

* 一些技术在一个平台上可用但是在另一个平台上却不可用。比如说，如果你使用富文本格式（rich text format, RTF）作为一个在OS X中的文档格式，它在iOS中将不会工作，因为iOS的文本系统没有提供对RTF格式的内置支持（尽管你可以在你的iOS应用中实现该支持）。

* 每个平台的默认做表系统都是不同的，这会影响到内容如何绘制。参阅*Drawing and Printing Guide for iOS*中的“Default Coordinate Systems and Drawing in iOS”以查看该主题的讨论。

* 如果你归档一个文本的模型对象图，当你编码（encode）或者解码（decode）模型对象时，你可能需要使用NSCoder方法执行适当的转换。

* 一些对应的类在跨平台时并不兼容。就是说，在类之间表现颜色（UIColor和NSColor），图像（UIImage和NSImage）以及贝塞尔路径（UIBezierPath和NSBezierPath）时，存在很重要的不同。比如说NSColor对象是依照一个色彩空间（NSColorSpace）定义的，但是在UIKit中不存在色彩空间类。

这些跨平台问题影响着你存储**被作为iCloud文档在OS X和iOS之间共享的文档数据**到文件中的方式。你的应用的两个版本都必须能使用可用的技术和类来重建一个可用的在内存中的并且适用于其所在平台的数据模型。并且，两个版本必须能够将它们的平台相关数据模型结构转换成共享文件格式。

一个你可以使用的策略就是，降低到更低层的可以被两个平台都支持的框架。比如说，在iOS这边，UIColor定义了一个CIColor属性控制了一个Core Image对象以展现色彩；在OS X这边，你的应用可以使用*colorWithCIColor:*方法从CIColor对象创建一个NSColor对象。








