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

* **Create new documents**. The first time the user chooses to save a new document, it presents a dialog in which the user names and saves the document in a disk file in a user-chosen location.

* **Open existing documents stored in files.** A document-based app specifies the types of document files it can read and write, as well as read-only and write-only types. It can represent the data of different document types internally and display the data appropriately.

* **Automatically save documents.** Document-based apps can adopt autosaving in place, and its documents are automatically saved at appropriate times so that the data the user sees on screen is effectively the same as that saved on disk. Saving is done safely, so that an interrupted save operation does not leave data inconsistent. To avoid automatic saving of inadvertent changes, old files are locked from editing until explicitly unlocked by the user.

* **Asynchronously read and write document data.** Reading and writing are done asynchronously on a background thread, so that lengthy operations do not make the app’s user interface unresponsive. In addition, reads and writes are coordinated using the NSFilePresenter protocol and the NSFileCoordinator class to reduce version conflicts.

* **Manage multiple versions of documents.** Autosave creates versions at regular intervals, and users can manually save a version whenever they wish. Users can browse versions and revert the document’s contents to a chosen version using a Time Machine–like interface. The version browser is also used to resolve version conflicts from simultaneous iCloud updates.

* **Print documents.** Users can specify various page layouts in the print dialog and page setup dialog.

* **Track changes and set the document’s edited status.** The document manages its edited status and implements multilevel undo and redo.

* **Validate menu items.** The document enables or disables menu items automatically, depending on its edited status and the applicability of the associated action methods.

* **Handle app and window delegation.** Notifications are sent and delegate methods called at significant life cycle events, such as when the app terminates.

Cocoa’s document architecture implements most of its capabilities in three classes. These classes interoperate to provide an extensible app infrastructure that makes it easy for you to create document-based apps. Table 1-1 briefly describes these classes.









