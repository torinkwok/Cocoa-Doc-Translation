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

### Cocoa Uses the Model-View-Controller Design Pattern
The Cocoa document architecture and many other technologies throughout Cocoa utilize the Model-View-Controller (MVC) design pattern. **Model objects** encapsulate the data specific to an app and manipulate and process that data. **View objects** display data from the app’s model objects and enable the editing of that data by users. **Controller objects** act as intermediaries between the app’s view objects and model objects. By separating these behaviors into discrete objects, your app code tends to be more reusable, the object interfaces are better defined, and your app is easier to maintain and extend. Perhaps most importantly, MVC-compliant app objects fit seamlessly into the document architecture.

### Cocoa使用模型（Model）-视图（View）-控制器（Controller）设计模式
Cocoa文档架构和许多其他的技术中到处都在使用模型-视图-控制器（MVC）设计模式。**模型对象**封装了特定于应用的数据并负责操作和处理这些数据。**视图对象**负责从应用的模型对象来显示数据并且允许用户编辑这些数据。**控制器对象**则在应用的视图对象和模型对象之间担任媒介。通过将这些行为分离到具体的对象中，你的应用的代码会更加趋于可重用，对象接口会被更好地定义，以及你的应用会更容易去维护和扩展。可能最重要的是，遵循MVC模式的应用程序会无缝地融合到文档架构中。

---

### A Data Model Corresponds to a Document Type
A document object is a controller dedicated to managing the objects in the document’s data model. Each document object is a custom subclass of NSDocument designed specifically to handle a particular type of data model. Document-based apps are able to handle one or more types of documents, each with its own type of data model and corresponding NSDocument subclass. Apps use an information property list file, which is stored in the app’s bundle and named, by default, <appName>-Info.plist, to specify information that can be used at runtime. Document-based apps use this property list to specify the document types the app can edit or view. For example, when the NSDocumentController object creates a new document or opens an existing document, it searches the property list for such items as the document class that handles a document type, the uniform type identifier (UTI) for the type, and whether the app can edit or only view the type. For more information about creating a property list for types of documents, see “Complete the Information Property List.”

### 一个数据模型对应于一个文档类型








