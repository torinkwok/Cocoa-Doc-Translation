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


## NSDocument Presents and Stores Document Data

NSDocument is the base class for document objects in the app architecture—you must create an NSDocument subclass for each type of document your app handles. When your app is running, it has an NSDocument-based object for each open document. In the MVC design pattern, NSDocument is a **model controller** because it manages the data model, that is, the persistent data associated with its document. An NSDocument object has the following responsibilities:

* Manages the display and capture of the data in its windows (with the assistance of its window controllers)

* Loads and stores (that is, reads and writes) the persistent data associated with its document

* Responds to action messages to save, print, revert, and close documents

* Runs and manages the `Save` and `Page Setup` dialogs


A fully implemented NSDocument object also knows how to track its edited status, perform undo and redo operations, print document data, and validate its menu items. Although these behaviors aren’t completely provided by default, the NSDocument object does assist the developer in implementing each, in the following ways:

* For tracking edited status, NSDocument provides a method for updating a change counter.

* For undo and redo operations, NSDocument lazily creates an NSUndoManager instance when one is requested, responds appropriately to `Undo` and `Redo` menu commands, and updates the change counter when undo and redo operations are performed.

* For printing, NSDocument facilitates the display of the `Page Setup` dialog and the subsequent modification of the NSPrintInfo object used in printing. To do this, subclasses of NSDocument must override *printOperationWithSettings:error:*.

* To validate menu items, NSDocument implements *validateUserInterfaceItem:* to manage the enabled state and titles of the menu items `Revert Document` and `Save` (which becomes `Save a Version` after the document is first saved). If you want to validate other menu items, you can override this method, but be sure to invoke the superclass implementation. For more information on menu item validation, see [NSUserInterfaceValidations Protocol Reference.](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Protocols/NSUserInterfaceValidations_Protocol/Reference/Reference.html#//apple_ref/doc/uid/TP40004183)

When designing your document objects, you should always maintain a clean separation between these data-handling activities of the document object itself and the code for managing the visual presentation of that data. The document object is responsible for the data, including the reading and writing of that data to disk. The visual presentation of that data is the responsibility of the associated window controller object. Keeping a clean separation between these two activities makes for a more modular design that can be updated more easily in the future.

Nonetheless, managing the document’s data and its user interface are closely related, which is why the document object owns and manages its window controllers. The document object also manages its menu, which is part of the user interface, because the state of its user commands—what commands are available and whether they are enabled—is determined by the state of the document data.

An NSDocument object should not contain or require the presence of any objects that are specific to the app’s user interface. Although a document can own and manage NSWindowController objects—which present the document visually and allow the user to edit it—it should not depend on these objects being there. For example, it might be desirable to have a document open in your app without having it visually displayed.

For details about subclassing NSDocument, see *“Creating the Subclass of NSDocument.”*

If you have a large data set or require a managed object model, you may want to use NSPersistentDocument, a subclass of NSDocument, to create a document-based app that uses Core Data. For more information, see *Core Data Starting Point.*



## NSDocument提供并存储文档数据

NSDocument是应用程序架构中的文档对象的基类——你必须为你的应用处理的每个文档类型都创建一个NSDocument子类。当你的应用运行时，它会为每个打开的文档创建一个基于NSDocument的对象。在MVC设计模式中，NSDocument是一个**模型控制器**，因为它管理数据模型，即与它的文档相关联的持久化数据。一个NSDocument对象拥有如下的责任：

* 管理数据在其窗口中（用它的窗口控制器来辅助）的显示和捕捉

* 加载和存储（即读取和写入）与它的文档相关联的持久化数据

* 响应动作消息以保存，打印，还原，以及关闭文档

* 运行和管理`保存`和`页面设置`对话框

一个完整的NSDocument实现应该还知道如何跟踪它的编辑状态，制定撤销（undo）和重做（redo）操作，打印文档数据，以及验证它的菜单项。尽管缺省情况下这些行为并不被完整提供，但是NSDocument对象使用一下几种途径来帮助开发者实现每一个功能：

* 对于跟踪编辑状态，NSDocument提供了一个用于更新**更改计数器（change counter）**的方法

* 对于撤销和重做操作，NSDocument会在其第一次被请求时惰性创建一个NSUndoManager实例，妥当响应`撤销`和`重做`菜单命令，并且当撤销和重做操作被执行时更新**更改计数器**

* 对于打印，NSDocument使`页面设置`对话框和NSPrintInfo对象的随后的更改被用于打印都变得很容易。为此，NSDocument的子类必须覆写*printOperationWithSettings:error:*方法

* 对于验证菜单项，NSDocument实现了*validateUserInterfaceItem:*方法以管理菜单项`还原文档`和`保存`（其在文档第一次被保存后会变成`保存一个版本`）的启用状态及标题。如果你想要验证其他菜单项，你可以覆写该方法，但是要保证调用其超类实现。更多关于菜单项验证的信息，参阅[NSUserInterfaceValidations Protocol Reference.](https://developer.apple.com/library/mac/documentation/Cocoa/Reference/ApplicationKit/Protocols/NSUserInterfaceValidations_Protocol/Reference/Reference.html#//apple_ref/doc/uid/TP40004183)


当设计你的文档对象时，你应该总是在**这些文档对象自身的数据操作行为**与**该数据的可视化展现的管理代码**之间保持清晰的分离。文档对象负责数据，包括在磁盘中对该数据的读操作和写操作。该数据的可视化展现则负责与窗口控制器对象关联。在这两个行为之间保持清晰的分离，有助于更加模块化的设计，这种设计会使未来的更新变得更容易。

尽管如此，管理文档的数据和它的用户界面还是莫切相关的，这就是为什么文档对象拥有并管理它的窗口控制器。文档对象也管理它的菜单，其菜单作为用户界面的一部分，这是因为它的用户命令的状态——哪个命令可用以及它们是否被启用——是由文档数据的状态来决定的。

一个NSDocument对象不应该包含或者需要任何特定于应用程序用户界面的对象存在，尽管一个文档对象可以拥有并管理NSWindowController对象——其以可视化的方式提供了文档并且允许用户去编辑文档——但是它不应该依赖于这些对象。例如，你的应用拥有一个打开的文档但是并没有可视化的显示也是合理的。

关于子类化NSDocument的详细信息，参阅*“Creating the Subclass of NSDocument。”*

如果你拥有一个庞大的数据集或者需要一个托管对象模型，你可能想要使用NSPersistentDocument，一个NSDocument的子类，用于创建使用Core Data的文档驱动应用程序。更多的信息参阅*Core Data Starting Point.*







