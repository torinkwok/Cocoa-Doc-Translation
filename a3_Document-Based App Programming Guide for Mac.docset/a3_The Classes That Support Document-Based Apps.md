# The Classes That Support Document-Based Apps

There are three major classes in the document architecture: NSDocumentController, NSDocument, and NSWindowController. Objects of these classes divide and orchestrate the work of creating, saving, opening, and managing the documents of an app. They are arranged in a tiered one-to-many relationship, as depicted in Figure 2-1. An app can have only one NSDocumentController object, which creates and manages one or more NSDocument objects (one for each New or Open operation). In turn, an NSDocument object creates and manages one or more NSWindowController objects, one for each of the windows displayed for a document. In addition, some of these objects have responsibilities analogous to NSApplication and NSWindow delegates, such as approving major events like closing and quitting.

**Figure 2-1**  Relationships among NSDocumentController, NSDocument, and NSWindowController objects

# 支持文档驱动应用的类

在文档架构中有三个主要的类：NSDocumentController，NSDocument以及NSWindowController。这些类的对象对创建（creating），保存（saving），打开（opening）以及管理（managing）应用的文档进行了划分和详细规划。他们被安排为一个一对多的分层关系，就像Figure 2-1中描述的。一个应用只可以拥有一个NSDocumentController对象，其创建并管理一个或多个NSDocument对象（每个都支持新建或打开操作）。反过来，一个NSDocument对象创建并管理一个或多个NSWindowController对象，每个都对应一个显示文档的窗口。此外，这些对象中的一些拥有和NSApplication和NSWindow委托相似的责任，比如批准类似关闭（closing）和退出（quitting）之类的主事件。

**Figure 2-1** NSDocumentController，NSDocument以及NSWindowController对象之间的关系

![ Figure 2-1 ](http://i.imgbox.com/aZOHmhRO.png)


A Cocoa app includes a number of key objects in addition to the three major types of objects of the document architecture. Figure 2-2 shows how these objects fit into the overall Cocoa object infrastructure.

**Figure 2-2** Key objects in a document-based app

除了文档架构的三个主要对象之外，Cocoa应用还包含了若干个关键对象。Figure 2-2展示了这些对象如何融入到Cocoa对象的基础架构中。

**Figure 2-2** 在一个文档驱动应用中的关键对象

![ Figure 2-2 ](http://i.imgbox.com/dqVVolQG.png)








