# Creating the Subclass of NSDocument

The NSDocument subclass provides storage for the model and the ability to load and save document data. It also has any outlets and actions required for the user interface. The NSDocument object automatically creates an NSWindowController object to manage that nib file, but the NSDocument object serves as the File’s Owner proxy object for the nib file.

When you subclass NSDocument, you must override certain key methods and implement others to do at least the following things:

* Read data of existing documents from files

* Write document data to files

* Initialize new documents

* Put documents into iCloud and remove them

In particular, you must override one reading and one writing method. In the simplest case, you can override the data-based reading and writing methods, *readFromData:ofType:error:* and *dataOfType:error:*.

# 创建NSDocument子类

NSDocument子类为模型提供存储功能，并且提供了加载和保存文档数据的功能。它还拥有用户界面所需要的任何插座（outlets）和动作（actions）。NSDocument对象会自动创建一个NSWindowController对象以管理该nib文件，但是由NSDocument对象来充当该nib文件的File's Owner代理对象。

当你子类化NSDocument时，你必须覆写某个关键方法并实现其他方法以至少做到如下事情：

* 从文件中读取已存在的数据

* 将文档数据写入到文件中

* 初始化新的文档

* 将文档放入iCloud以及移除它们

尤其是你必须覆写一个读取和一个写入方法。在最简单的情况中，你可以覆写基于数据的读写方法*readFromData:ofType:error:*和*dataOfType:error:*方法。



