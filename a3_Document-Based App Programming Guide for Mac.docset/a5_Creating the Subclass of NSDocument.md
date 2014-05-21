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

---

### How to Override the Data-Based Reading Method
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

### 如何覆写基于数据（Data-Based）的读取方法
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

---

### It’s Easy to Support Concurrent Document Opening
A class method of NSDocument, *canConcurrentlyReadDocumentsOfType:*, enables your NSDocument subclass to load documents concurrently, using background threads. This override allows concurrent reading of multiple documents and also allows the app to be responsive while reading a large document. You can override *canConcurrentlyReadDocumentsOfType:* to return YES to enable this capability. When you do, *initWithContentsOfURL:ofType:error:* executes on a background thread when opening files via the `Open` dialog or from the Finder.

The default implementation of this method returns NO. A subclass override should return YES only for document types whose reading code can be safely executed concurrently on non-main threads. If a document type relies on shared state information, you should return NO for that type.

### 很容易支持并行文档打开
NSDocument的类方法*canConcurrentlyReadDocumentsOfType:*，允许你的NSDocument子类使用后台线程并行地加载文档。该覆写允许多文档的并行读取，并且还允许当读取一个大型文档时保持应用的响应。你可以覆写*canConcurrentlyReadDocumentsOfType:*方法返回YES以启用该功能。如果这样，当通过`打开`对话框或从Finder中打开文件时，*initWithContentsOfURL:ofType:error:*方法会在一个后台线程中执行。

该方法的默认实现返回NO。一个子类覆写应该只为其读取代码能够在非主线程中安全地并行执行的文档类型返回YES。如果一个文档类型依赖于共享状态信息，你应该为该类型返回NO。

---

### Don’t Rely on Document-Property Getters in Overrides of Reading Methods
Don’t invoke *fileURL*, *fileType*, or *fileModificationDate* from within your overrides. During reading, which typically happens during object initialization, there is no guarantee that NSDocument properties like the file’s location or type have been set yet. Your overridden method should be able to determine everything it needs to do the reading from the passed-in parameters. During writing, your document may be asked to write its contents to a different location or using a different file type.

If your override cannot determine all of the information it needs from the passed-in parameters, consider overriding another method. For example, if you see the need to invoke *fileURL* from within an override of *readFromData:ofType:error:*, you should instead override *readFromURL:ofType:error:* and use the passed-in URL value.

### 不要依赖于读取方法的覆写中的文档属性获取方法（Document-Property Getters）
不要在你的覆写中调用*fileURL*，*fileType*或者*fileModificationDate*方法。在读取期间，其通常会在对象的初始化时发生，这时无法保证像文件位置或者类型这样的NSDocument属性已经被设置。你的覆写方法应该限定为从传入的参数中获取它需要的任何事物。在写入期间，你的文档可能会被要求将它的内容写入到不同的位置或者使用不同的文件类型。

如果你的覆写不能从传入的参数中获取其所需要的全部信息，那么应该考虑覆写其他方法。例如，如果你发现需要在*readFromData:ofType:error:*方法的覆写中调用*fileURL*方法，那么你就应该覆写*readFromURL:ofType:error:*方法替换之，并使用其传入的URL值。

---

## Writing Document Data

In addition to implementing a document-reading method, you must implement a document-writing method to save your document data to disk. In the simplest case, you can override the data-based writing method, *dataOfType:error:*. If it works for your application, you should override *dataOfType:error:*. Overriding that method makes your work easier because it uses the default document-reading infrastructure provided by NSDocument. The responsibility of your override of the *dataOfType:error:* method is to create and return document data of a supported type, packaged as an NSData object, in preparation for writing that data to a file.

Listing 4-2 shows an example implementation of *dataOfType:error:*. As with the corresponding example implementation document-reading method, this example assumes that the app has an NSTextView object configured with an NSTextStorage object to hold the document’s data. The document object has an outlet property connected to the NSTextView object and named textView. The document object also has synthesized mString and setMString: accessors for the document’s NSAttributedString data model, declared as a property named mString.

**Listing 4-2**  Data-based document-writing method implementation
```
- (NSData *)dataOfType:(NSString *)typeName error:(NSError **)outError {
    NSData *data;
    [self setMString:[self.textView textStorage]]; // Synchronize data model with the text storage
    NSMutableDictionary *dict = [NSDictionary dictionaryWithObject:NSRTFTextDocumentType
                                                            forKey:NSDocumentTypeDocumentAttribute];
    [self.textView breakUndoCoalescing];
    data = [self.mString dataFromRange:NSMakeRange(0, [self.mString length])
                    documentAttributes:dict error:outError];
    if (!data && outError) {
        *outError = [NSError errorWithDomain:NSCocoaErrorDomain
                                code:NSFileWriteUnknownError userInfo:nil];
    }
    return data;
}
```
The override sends the NSTextView object a *breakUndoCoalescing* message when saving the text view’s contents to preserve proper tracking of unsaved changes and the document’s dirty state.

If your app needs access to document files, you can override *writeToURL:ofType:error:* instead. If your document data is stored in file packages, you can override *fileWrapperOfType:error:* instead. For information about overriding the other NSDocument writing methods, see *“Overriding the URL and File Package Writing Methods.”*

The actual flow of messages during this sequence of events is shown in detail in Figure 6-6.

## 写入文档数据

除了要实现一个文档读取方法之外，你还必须实现一个文档写入方法来将你的数据保存到磁盘。在最简单的情况中，你可以覆写基于数据的写入方法*dataOfType:error:*。如果适合你的应用程序，你就应该覆写*dataOfType:error:*方法。覆写该方法会使得你的工作更加简单，因为它使用了NSDocument提供的默认文档读取基础结构。你的*dataOfType:error:*方法覆写的责任就是创建并返回一个支持类型的文档数据，将其打包成一个NSData对象，并未将该NSData对象写入文件做准备。

Listing 4-2中展示了一个*dataOfType:error:*方法的范例实现。正如对应的文档写入方法的范例实现一样，该范例实现假设应用有一个配置了NSTextStorage对象以持有文档数据的NSTextView对象。文档对象还有一个连接到NSTextView对象并且命名为textView的插座属性。文档对象还拥有合成的用于文档的NSAttributedString数据模型的mString与setMString:存取器，其声明为mString属性。

**Listing 4-2**  基于数据的文档写入方法实现
```
- (NSData *)dataOfType:(NSString *)typeName error:(NSError **)outError {
    NSData *data;
    [self setMString:[self.textView textStorage]]; // Synchronize data model with the text storage
    NSMutableDictionary *dict = [NSDictionary dictionaryWithObject:NSRTFTextDocumentType
                                                            forKey:NSDocumentTypeDocumentAttribute];
    [self.textView breakUndoCoalescing];
    data = [self.mString dataFromRange:NSMakeRange(0, [self.mString length])
                    documentAttributes:dict error:outError];
    if (!data && outError) {
        *outError = [NSError errorWithDomain:NSCocoaErrorDomain
                                code:NSFileWriteUnknownError userInfo:nil];
    }
    return data;
}
```
当保存文本视图的内容时，该覆写会向NSTextView发送一个*breakUndoCoalescing*消息以保持对为保存的更改和文档的dirty状态的跟踪。

如果你的应用需要访问文档文件，那么你就应该覆写*writeToURL:error:*方法替换之。如果你的文档数据被存储在文件包中，你可以覆写*fileWrapperOfType:error:*方法替换之。关于覆写其他NSDocument写入方法的信息，参阅*“Overriding the URL and File Package Writing Methods。”*

在这一系列事件发生时，实际的消息流程如Figure 6-6中所示。



## Initializing a New Document

The *init* method of NSDocument is the designated initializer, and it is invoked by the other initializers *initWithType:error:* and *initWithContentsOfURL:ofType:error:*. If you perform initializations that must be done when creating new documents but not when opening existing documents, override *initWithType:error:*. If you have any initializations that apply only to documents that are opened, override *initWithContentsOfURL:ofType:error:*. If you have general initializations, override *init*. In all three cases, be sure to invoke the superclass implementation as the first action.

If you override *init*, make sure that your override never returns nil. Returning nil could cause a crash (in some versions of AppKit) or present a less than useful error message. If, for example, you want to prevent the creation or opening of documents under circumstances unique to your app, override a specific NSDocumentController method instead. That is, you should control this behavior directly in your app-level logic (to prevent document creation or opening in certain cases) rather than catching the situation after document initialization has already begun.

> Note: If you don’t want to open an untitled document when the app is launched or activated, implement the app delegate method *applicationShouldOpenUntitledFile:* to return NO. If you do want to open an untitled document when launched, but don't want to open an untitled document when the app is already running and activated from the dock, you can instead implement the delegate’s *applicationShouldHandleReopen:hasVisibleWindows:* method to return NO.

Implement *awakeFromNib* to initialize objects unarchived from the document’s window nib files (but not the document itself).

## 初始化一个新的文档

NSDocument的*init*方法是一个指定初始化器（designated initializer），并且它会被*initWithType:error:*和*initWithContentOfURL:ofType:error:*方法调用。如果你要执行一些在创建一个新的文档而非在打开已存在文档所执行的初始化，覆写*initWithType:error:*方法。如果你要执行一些只用于被打开文档的初始化动作，那么覆写*initWithContentsOfURL:ofType:error:*方法。如果你要执行一些泛型的初始化，覆写*init*方法。在全部三种情况中，都要确保将调用超类的实现作为第一步动作。

如果你覆写*init*，要确保你的覆写绝不会返回nil。返回nil会导致崩溃（在一些AppKit版本中）或者会提供一些没有多大用的错误信息。例如，如果你想提供在特定于你的应用的情况下的文档创建和打开操作，可以覆写特性的NSDocumentController方法。换言之，你应该在你的应用层逻辑中直接控制该行为（在某些类中提供文档创建或打开）而非在文档初始化已经开始之后才捕捉这种状况。

> 注意：如果你不想在应用被启动或激活时打开一个无标题文档，可以实现应用程序委托方法*applicationShouldOpenUntitledFile:*并返回NO。如果你确实向在启动时打开一个无标题文档，但是不想在应用已经运行和激活时从dock中打开无标题文档的话，你可以实现委托的*applicationShouldHandleReopen:hasVisibleWindows:*方法并返回NO。

实现*awakeFromNib*方法来初始化那些从文档的窗口nib文件（而非文档本身）中解归档出来的对象。



## Moving Document Data to and from iCloud

The iCloud storage technology enables you to share documents and other app data among multiple computers that run your document-based app. If you have an iOS version of your document-based app that shares the same document data formats, documents can be shared among iOS devices as well, as shown in Figure 4-1. Changes made to the file or directory on one device are stored locally and then pushed to iCloud using a local daemon. The transfer of files to and from each device is transparent to your app.

**Figure 4-1**  Sharing document data via iCloud

![ Figure 4-1 ](http://i.imgbox.com/HbABfOKN.png)

Access to iCloud is controlled using entitlements, which your app configures through Xcode. If these entitlements are not present, your app is prevented from accessing files and other data in iCloud. In particular, the container identifiers for your app must be declared in the **com.apple.developer.ubiquity-container-identifiers** entitlement. For information about how to configure your app’s entitlements, see *Developing for the App Store* and *Tools Workflow Guide for Mac.*

All files and directories stored in iCloud must be managed by an object that adopts the NSFilePresenter protocol, and all changes you make to those files and directories must occur through an NSFileCoordinator object. The file presenter and file coordinator prevent external sources from modifying the file at the same time and deliver relevant notifications to other file presenters. NSDocument implements the methods of the NSFilePresenter protocol and handles all of the file-related management for you. All your app must do is read and write the document data when told to do so. Be sure you override *autosavesInPlace* to return YES to enable file coordination in your NSDocument object.

## 将文档数据移动到iCloud或从iCloud中移出

iCloud存储技术使得你可以在多台运行你的文档驱动应用的计算机之间共享文档和其他应用数据。如果你有一个该应用的共享相同数据格式的iOS版本，文档也可以在iOS设备之间被共享，如Figure 4-1中所示。对某一台设备上的文件或目录的更改，会被存储到本地，并且还会使用本地的守护进程推送到iCloud。将文件从每台设备转移或转移到该设备的过程，对于你的应用来说都是透明的。

**Figure 4-1**  通过iCloud共享文档数据

![ Figure 4-1 ](http://i.imgbox.com/HbABfOKN.png)

对iCloud的访问是使用权限控制的，你的应用程序可以通过Xcode来配置该权限。如果没有提供这些权限，那么你的应用程序将会被阻止访问iCloud中的文件和其他数据。尤其是你的应用的容器标识符必须在**com.apple.developer.ubiquity-container-identifiers**权限中声明。关于如何配置应用程序的权限，参阅*Developing for the App Store*及*Tools Workflow Guide for Mac。*

所有存储在iCloud中的文件和目录都必须由采用NSFilePresenter协议的对象管理，并且你对这些文件和目录所做的改变都必须通过NSFileCoordinator对象发生。文件提供器（file presenter）和文件协调器（file coordinator）会防止外部来源同时修改文件，并且会转发相关的通知到其他的文件提供器。NSDocument实现了NSFilePresenter协议的方法并且会为你处理全部与文件相关的管理。你的应用所必须做的全部就是在被告知时读写文档数据。要确保覆写了*autosavesInPlace*方法并返回YES，以启用你的NSDocument对象中的文件协调。



## Determining Whether iCloud Is Enabled
Early in the execution of your app, before you try to use any other iCloud interfaces, you must call the NSFileManager method URLForUbiquityContainerIdentifier: to determine whether iCloud storage is enabled. This method returns a valid URL when iCloud is enabled (and the specified container directory is available) or nil when iCloud is disabled. URLForUbiquityContainerIdentifier: also returns nil if you specify a container ID that the app isn't allowed to access or that doesn't exist. In that case, the NSFileManager object logs a message to the console to help diagnose the error.

Listing 4-3 illustrates how to determine whether iCloud is enabled for the document’s file URL, presenting an error message to the user if not, and setting the value of the document’s destination URL to that of its iCloud container otherwise (in preparation for moving the document to iCloud using the setUbiquitous:itemAtURL:destinationURL:error: method).

**Listing 4-3**  Determining whether iCloud is enabled
```
NSURL *src = [self fileURL];
NSURL *dest = NULL;
NSURL *ubiquityContainerURL = [[[NSFileManager defaultManager]
                                 URLForUbiquityContainerIdentifier:nil]
                                 URLByAppendingPathComponent:@"Documents"];
    if (ubiquityContainerURL == nil) {
        NSDictionary *dict = [NSDictionary dictionaryWithObjectsAndKeys:
              NSLocalizedString(@"iCloud does not appear to be configured.", @""),
                              NSLocalizedFailureReasonErrorKey, nil];
        NSError *error = [NSError errorWithDomain:@"Application" code:404
                                         userInfo:dict];
        [self presentError:error modalForWindow:[self windowForSheet] delegate:nil
                             didPresentSelector:NULL contextInfo:NULL];
        return;
        }
        dest = [ubiquityContainerURL URLByAppendingPathComponent:
                                                          [src lastPathComponent]];
```

Because the message specifies nil for the container identifier parameter, URLForUbiquityContainerIdentifier: returns the first container listed in the com.apple.developer.ubiquity-container-identifiers entitlement and creates the corresponding directory if it does not yet exist. Alternatively, you could specify your app’s container identifier—a concatenation of team ID and app bundle ID, separated by a period for the app’s primary container identifier, or a different container directory. For example, you could declare a string constant for the container identifier, as in the following example, and pass the constant name with the message.

```static NSString *UbiquityContainerIdentifier = @"A1B2C3D4E5.com.domainname.appname";```

The method also appends the document’s filename to the destination URL.








 