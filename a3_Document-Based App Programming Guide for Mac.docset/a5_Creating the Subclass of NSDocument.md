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



## Reading Document Data

Opening existing documents stored in files is one of the most common operations document-based apps perform. Your override’s responsibility is to load the file data into your app’s data model.

If it works for your application, you should override the data-based reading method, *readFromData:ofType:error:*. Overriding that method makes your work easier because it uses the default document-reading infrastructure provided by NSDocument, which can handle multiple cases on your behalf.

> Note: You should disable undo registration during document reading.

## 读取文档数据

打开存储在文件中的已存在文档是文档驱动应用程序提供的最常见操作之一。你的该方法覆写的责任就是将文件数据加载到你的应用的数据模型中。

如果适合你的应用程序，那么你就应该覆写基于数据的读取方法*readFromData:ofType:error:*。覆写该方法会是你的工作更加容易，因为它使用了NSDocument提供的文档读取基础结构，其可以代替你处理很多情况。

> 注意：你应该在文档读取时禁用撤销注册。



## How to Override the Data-Based Reading Method
You can override the *readFromData:ofType:error:* method to convert an NSData object containing document data into the document’s internal data structures and display that data in a document window. The document architecture calls *readFromData:ofType:error:*, passing in the NSData object, during its document initialization process.

Listing 4-1 shows an example implementation of the *readFromData:ofType:error:* document-reading method. This example assumes that the app has an NSTextView object configured with an NSTextStorage object to hold the text view’s data. The NSDocument object has a *setMString:* accessor method for the document’s NSAttributedString data model, declared as a property named mString.

**Listing 4-1**  Data-based document-reading method implementation
```
- (BOOL)readFromData:(NSData *)data ofType:(NSString *)typeName
                                     error:(NSError **)outError {
    BOOL readSuccess = NO;
    NSAttributedString *fileContents = [[NSAttributedString alloc]
            initWithData:data options:NULL documentAttributes:NULL
            error:outError];
    if (!fileContents && outError) {
        *outError = [NSError errorWithDomain:NSCocoaErrorDomain
                                code:NSFileReadUnknownError userInfo:nil];
    }
    if (fileContents) {
        readSuccess = YES;
        [self setMString:fileContents];
    }
    return readSuccess;
}
```

If you need to deal with the location of the file, override the URL reading and writing methods instead. If your app needs to manipulate document files that are file packages, override the file-wrapper reading and writing methods instead. For information about overriding the URL-based and file-wrapper-based reading methods, see *“Overriding the URL and File Package Reading Methods.”*

The flow of messages during document data reading is shown in Figure 6-5.

## 如何覆写基于数据（Data-Based）的读取方法
你可以覆写*readFromData:ofType:error:*方法来将一个包含文档数据的NSData对象转换成文档的内部数据结构，并将该数据显示在文档窗口中。文档架构会在它的文档初始化过程中调用*readFromData:ofType:error:*方法，并传入NSData对象。

Listing 4-1展示了一个*readFromData:ofType:error:*文档读取方法的范例实现。该范例假设应用有一个配置了NSTextStorage对象以持有文本视图数据的NSTextView对象。该NSDocument对象对于文档的NSAttributedString数据模型有一个*setMString:*存取器方法，其声明为一个名为mString的属性。

**Listing 4-1**  基于数据的文档读取方法实现
```
- (BOOL)readFromData:(NSData *)data ofType:(NSString *)typeName
                                     error:(NSError **)outError {
    BOOL readSuccess = NO;
    NSAttributedString *fileContents = [[NSAttributedString alloc]
            initWithData:data options:NULL documentAttributes:NULL
            error:outError];
    if (!fileContents && outError) {
        *outError = [NSError errorWithDomain:NSCocoaErrorDomain
                                code:NSFileReadUnknownError userInfo:nil];
    }
    if (fileContents) {
        readSuccess = YES;
        [self setMString:fileContents];
    }
    return readSuccess;
}
```

如果你需要处理文件的位置，那么可以重写URL读写方法代替之。如果你的应用需要操纵作为文件包的文档文件，那么可以覆写文件包装器（file-wrapper）读写方法代替之。关于覆写基于URL的和基于文件包装器的读取方法，参阅*“Overriding the URL and File Package Reading Methods。”*

文档数据读取时的消息流程如Figure 6-5中所示。




