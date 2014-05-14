# Designing a Document-Based App

Documents are containers for user data that can be stored in files locally and in iCloud. In a document-based design, the app enables users to create and manage documents containing their data. One app typically handles multiple documents, each in its own window, and often displays more than one document at a time. For example, a word processor provides commands to create new documents, it presents an editing environment in which the user enters text and embeds graphics into the document, it saves the document data to disk or iCloud, and it provides other document-related commands, such as printing and version management. In Cocoa, the document-based app design is enabled by a subsystem called the document architecture, which is part of of the AppKit framework.

# 设计Document-Based应用

文档是可以被存储在本地文件中和iCloud中的用户数据的容器。在document-based设计中，app使得用户能够创建和管理包含他们数据的文档。一个app通常会处理多个文档，每个文档都处在其自己的窗口中，并且经常在同一时间显示多个文档。比如说：一个字处理程序就提供了用于创建新文档的命令，其提供了一个用户向文档中输入文本及嵌入图像得编辑环境，该程序还将文档数据保存到磁盘或者iCloud中，并且它还提供了其他文档相关的命令，比如打印（printing）和版本管理（version managment）。在Cocoa中，document-based应用设计通过一个被叫做**文档架构**得子系统来实现，该架构也是AppKit框架得一部分。

## Documents in OS X

There are several ways to think of a document. Conceptually, a document is a container for a body of information that can be named and stored in a file. In this sense, the document is an object in memory that owns and manages the document data. To users, the document is their information—such as text and graphics formatted on a page. In the context of Cocoa, a document is an instance of a custom NSDocument subclass that knows how to represent internally persistent data that it can display in a window. This document object knows how to read document data from a file and create an object graph in memory for the document data model. It also knows how to modify that data model consistently and write the document data back out to disk. So, the document object mediates between different representations of document data, as shown in Figure 1-1.

**Figure 1-1**  Document file, object, and data model

Using iCloud, documents can be shared automatically among a user’s computers and iOS devices. The system synchronizes changes to the document data without user intervention. See **“Storing Documents in iCloud”** for more information.

## OS X中的文档

有几种理解文档的方式。从概念上说，一个文档就是一个可以被命名和存储在文件中的信息体的容器。从这个意义上说，文档是一个内存中的对象，其拥有并管理文档数据。对于用户而言，文档是他们的信息——比如一个格式化文本和图像的页面。在Cocoa环境中，一个文档是一个自定义的NSDocument子类的实例，该实例知道如何在内部展现可以被显示在窗口中的持久化数据。该文档对象知道如何从一个文件中读取文档数据并在内存中为文档数据模型创建对象图。它还知道如何一致地修改数据模型并将文档数据写回到磁盘中。所以，文档对象在文档数据不同的表现形式之间进行协调，如Figure 1-1所示。

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
NSWindowController   | 管理文档被显示在的窗口
NSDocumentController | 管理app中的所有的文档对象

> 更多详细信息参见：[“The Classes That Support Document-Based Apps”。](https://developer.apple.com/library/mac/documentation/DataManagement/Conceptual/DocBasedAppProgrammingGuideForOSX/KeyObjects/KeyObjects.html#//apple_ref/doc/uid/TP40011179-CH3-SW2)












