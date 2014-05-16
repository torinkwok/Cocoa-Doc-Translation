# The Classes That Support Document-Based Apps

There are three major classes in the document architecture: NSDocumentController, NSDocument, and NSWindowController. Objects of these classes divide and orchestrate the work of creating, saving, opening, and managing the documents of an app. They are arranged in a tiered one-to-many relationship, as depicted in Figure 2-1. An app can have only one NSDocumentController object, which creates and manages one or more NSDocument objects (one for each New or Open operation). In turn, an NSDocument object creates and manages one or more NSWindowController objects, one for each of the windows displayed for a document. In addition, some of these objects have responsibilities analogous to NSApplication and NSWindow delegates, such as approving major events like closing and quitting.

**Figure 2-1**  Relationships among NSDocumentController, NSDocument, and NSWindowController objects

# 支持文档驱动应用的类

在文档架构中有三个主要的类：NSDocumentController，NSDocument以及NSWindowController。这些类的对象对创建（creating），保存（saving），打开（opening）以及管理（managing）应用的文档进行了划分和详细规划。他们被安排为一个一对多的分层关系，就像Figure 2-1中描述的。一个应用只可以拥有一个NSDocumentController对象，其创建并管理一个或多个NSDocument对象（每个都对应新建或打开操作）。依次下去，一个NSDocument对象创建并管理一个或多个NSWindowController对象，每个都对应一个显示文档的窗口。此外，这些对象中的一些拥有和NSApplication和NSWindow委托相似的责任，比如批准类似关闭（closing）和退出（quitting）之类的主事件。

**Figure 2-1** NSDocumentController，NSDocument以及NSWindowController对象之间的关系

![ Figure 2-1 ](http://i.imgbox.com/aZOHmhRO.png)


A Cocoa app includes a number of key objects in addition to the three major types of objects of the document architecture. Figure 2-2 shows how these objects fit into the overall Cocoa object infrastructure.

**Figure 2-2** Key objects in a document-based app

除了文档架构的三个主要对象之外，Cocoa应用还包含了若干个关键对象。Figure 2-2展示了这些对象如何融入到Cocoa对象的基础架构中。

**Figure 2-2** 在一个文档驱动应用中的关键对象

![ Figure 2-2 ](http://i.imgbox.com/dqVVolQG.png)


## NSDocumentController Creates and Manages Documents

An app’s NSDocumentController object manages the documents in an app. In the MVC design pattern, an NSDocumentController object is a **high-level controller.** It has the following primary responsibilities:

* Creates empty documents in response to the `New` item in the `File` menu

* Creates documents initialized with data from a file in response to the `Open` item in the `File` menu

* Tracks and manages those documents

* Handles document-related menu items, such as `Open Recent`

When a user chooses `New` from the `File` menu, the NSDocumentController object gets the appropriate NSDocument subclass from the app’s **Information property list** and allocates and initializes an instance of this class. Likewise, when the user chooses `Open`, the NSDocumentController object displays the Open dialog, gets the user’s selection, finds the NSDocument subclass for the file, allocates an instance of the class, and initializes it with data from the file. In both cases, the NSDocumentController object adds a reference to the document object to an internal list to help manage its documents.

Most of the time, you can use NSDocumentController as is to manage your app’s documents. NSDocumentController is hard-wired to respond appropriately to certain app events, such as when the app starts up, when it terminates, when the system is shutting down, and when documents are opened or printed. Alternatively, you can create a custom delegate object and implement the delegate methods corresponding to the same events (see [NSApplicationDelegate Protocol Reference](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/NSApplicationDelegate_Protocol/Reference/Reference.html#//apple_ref/doc/uid/TP40008592)).

## NSDocumentController用于创建和管理文档

应用的NSDocumentController对象管理着应用中的文档。在MVC设计模式中，一个NSDocumentController对象是一个**高层次控制器（high-level-controller）。**其拥有如下的主要责任：

* 创建空的文档以响应`文件`菜单中的`新建`项

* 创建文档对象并使用从文件中读取的数据进行初始化以响应`文件`菜单中的`打开`项

* 跟踪并管理那些文档

* 处理文档相关的菜单项，比如`最近打开的文档`

当一个用户从`文件`菜单中选择`新建`项时，NSDocumentController对象从应用的**Information property list**中获取适当的NSDocument子类，并分配及初始化一个该类的实例。同样地，当用户选择`打开`项时，NSDocumentController对象会显示打开对话框，获取用户的选择，从该文件中查找NSDocument的子类，分配一个该类的实例，并且使用从文件中读取的数据初始化该实例。在这两种情况中，NSDocumentController会向内部的列表中添加文档对象的引用以帮助其管理它的文档。

大多数时候，你可以使用NSDocumentController去管理你的文档。NSDocumentController是一个硬连接以妥善应对某些应用事件，比如当应用启动时，当应用终止时，当系统被关闭时，以及当文档被打开或者打印时。或者，你可以创建一个定制的委托对象并实现与同一个事件所对应的委托方法（参阅[NSApplicationDelegate Protocol Reference](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/NSApplicationDelegate_Protocol/Reference/Reference.html#//apple_ref/doc/uid/TP40008592)）。







