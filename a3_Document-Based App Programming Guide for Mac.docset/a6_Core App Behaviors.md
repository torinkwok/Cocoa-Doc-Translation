# Core App Behaviors

The Cocoa document architecture, and NSDocument in particular, provide support for many core behaviors of Mac apps.

# 核心应用行为
Cocoa文档架构，尤其是NSDocument，为Mac应用的核心行为提供了许多支持。



## Documents Are Automatically Saved

In OS X v10.7 and later, users don’t need to save documents explicitly or be concerned about losing unsaved changes. Instead, the system automatically writes document data to disk as necessary. Your NSDocument subclass opts into this behavior by overriding the *autosavesInPlace* class method to return YES. The ideal baseline for save-less documents is this: The document data that users see in an app window is identical to the document data on disk at all times. For practical reasons, the system does not attempt to save every change immediately, but it saves documents often enough and at the correct times to ensure that the document in memory and the one on disk are effectively the same.

Part of the implementation of save-less documents is file coordination, a mechanism that serializes access to files among processes to prevent inconsistencies due to non-sequential reading and writing. Apps use file coordination so that users don’t need to remember to save document changes before causing the document’s file to be read by another app. Document-based Cocoa apps use file coordination automatically.

## 文档被自动保存

在OS X 10.7和之后的版本中，用户不需要显式保存文档或者操心丢失为保存的更改。反而，系统会在必要时自动将文档数据写入到磁盘中。你的NSDocument子类可以通过覆写*autosavesInPlace*方法并返回YES来启用该行为。这会造成一种假象：用户任何时候在应用窗口中看到的文档数据与磁盘中的文档数据都是相同的。实际却是，系统并不会尝试立即保存每次更改，但是会足够频繁地保存文档并且会在正确的时间去这么做，以确保在内存中的文档和在磁盘中的文档实际相同。

save-less文档实现的一部分就是文件协调，这是一个在进程之间序列化文件访问的机制，其用于防止由于非连续性的读写而产生的不一致性。应用使用文件协调机制以便用户在使当前文档被另外一个程序读取时，不必记得去保存该文档。文档驱动型的Cocoa应用会自动使用文件协调机制。

---

### Autosaving in Place Differs From Autosaving Elsewhere
Automatic document saving is supported by the implementation of autosaving in place. Autosaving in place and autosaving elsewhere both protect against the user losing work due to app crashes, kernel panics, and power failures. However, autosaving in place differs from autosaving elsewhere in that it overwrites the actual document file rather than writing a new file next to it containing the autosaved document contents. (Autosaving in place performs a safe save by writing to a new file first, then moving it into the place of the document file when done.) Autosaving in place is illustrated in Figure 5-1.

**Figure 5-1**  Autosaving in place

The document architecture still uses autosaving elsewhere to save untitled documents that have content but have not been explicitly saved and named by the user. In this case, untitled documents are autosaved in ~/Library/Autosave Information. In addition, NSDocument saves earlier revisions of documents elsewhere, giving the user access to previous versions.

The saveless-documents model automates crash protection but preserves the ability for users to save documents explicitly. It also automates maintenance of multiple older versions. Users can save immediately in the traditional way (by choosing `File` > `Save a Version` or pressing Command-S). For an untitled document, an explicit `Save` command presents a dialog enabling the user to name the document and specify the location where it is to be written to disk.

You should not invoke the *autosavesInPlace* method to find out whether autosaving is being done. Instead, the document architecture passes one of two new autosaving-related enumerators as an NSSaveOperationType parameter to your overrides of the NSDocument methods beginning with save... and write..., and you can examine those values. The autosave enumerators are NSAutosaveInPlaceOperation and NSAutosaveElsewhereOperation. The old NSAutosaveOperation enumerator is equivalent to NSAutosaveElsewhereOperation and is deprecated in OS X v10.7.

### Autosaving in Place不同于Autosaving Elsewhere
自动文档保存由Autosaving in Place的实现支持。Autosaving in Place和Autosaving Elsewhere都是用于防止用户的工作由于应用崩溃，内核错误以及电源错误而丢失。然而Autosaving in Place不同于Autosaving Elsewhere，是因为其会覆写实际的文档文件而不是写入到紧挨着包含自动保存文档内容的文件旁边的文件中。（Autosaving in Place第一次会通过写入到一个新文件中来执行安全保存，然后会在完成时将其移动到文档文件的位置。）Figure 5-1中是Autosaving in Place的插图：

**Figure 5-1**  Autosaving in Place

文档架构仍会使用Autosaving Elsewhere来保存那些含有内容但是还没有由用户显式保存和命名的无标题文档。在这种情况下，无标题文档或被自动保存在*~/Library/Autosave Infomation*中。此外，NSDocument会在其他地方保存文档的早起版本，以给用户提供对之前版本的访问。

The saveless-documents model automates crash protection but preserves the ability for users to save documents explicitly（这一句求翻译）。它也会自动进行对多个旧版本的维护。用户可以使用传统的方式立刻保存文档（通过选择`File` > `Save a Version`或者键入Command-S）。对于一个无标题文档，一个显式的`Save`命令会提供一个对话框，该对话框允许用户命名文档并为该文档指定其被写入到的硬盘的位置。

你不应该调用*autosavesInPlace*方法来查询是否设置了自动保存。反之，文档架构会将两个新的与自动保存相关的枚举器作为NSSaveOperationType类型参数来传入到你的以*save...*和*write...*开头的NSDocument方法的覆写中，并且你可以检查这些值来判断文档是否开启了自动保存。自动保存枚举器其实是NSAutosaveInPlaceOperation和NSAutosaveElsewhereOperation。旧的NSAutosaveOperation枚举器等价于NSAutosaveElsewhereOperation并且其在OS X 10.7中已被废弃。

---

### Consider Autosaving Performance
Before you enable autosaving, consider the saving performance of your app. If your app saves quickly, there is little reason not to enable it. But if your app saves slowly, enabling autosaving could cause periodic blocking of your user interface while saving is happening. So, for example, if you have already implemented the autosaving behavior introduced in OS X v10.4 (sending *setAutosavingDelay:* to the NSDocumentController object with a nonzero value), then your app’s saving performance is probably acceptable, and opting into autosaving in place is as simple as overriding *autosavesInPlace* to return YES. Otherwise, you may first need to address any issues with your document model or saving logic that could hinder saving performance.

### 考虑自动保存的性能
当你启用自动保存之前，要考虑一下你的应用的保存性能。如果你的应用能快速保存，那就基本上没有不启用自动保存的原因。但是如果你的应用保存速度很慢，那么启动自动保存会导致在保存发生时你的用户界面的定期阻塞。所以，如果你已经实现了OS X10.4中引入的自动保存行为（使用一个非零值作为参数给NSDocumentController发送*setAutosavingDelay:*消息），那么你的应用的保存性能应该是可以接受的，并且启用Autosaving in Place就只有覆写*autosavesInPlace*并返回YES这么简单。否则，你可能首先需要解决你的文档模型和任何可能阻碍保存性能的保存逻辑上的问题。

---

### Safety Checking Prevents Unintentional Edits
When saving happens without user knowledge, it becomes easier for unintentional edits to get saved to disk, resulting in potential data loss. To help prevent autosaving unintentional edits, NSDocument performs safety checking to determine when a user has opened a document to read it, but not edit it. For example, if the document has not been edited for some period of time, it is locked for editing and opened only for reading. (The period after editing when the document is locked is an option in the Time Machine system preference.) NSDocument also checks for documents that are in folders where the user typically does not edit documents, such as the *~/Downloads* folder.

When an edit is made to the document, NSDocument offers the user the choice of canceling the change, creating a new document with the change, or allowing editing. A document that is preventing edits displays *Locked* in the title bar. The user can explicitly enable editing of the document by clicking on the *Locked* label and choosing *Unlock* in the pop-up menu. A document that has been changed since it was last opened and is therefore being actively autosaved in place displays *Edited* in the titlebar instead of *Locked*.

An app can programmatically determine when a document is locked in read-only “viewing mode” by sending it the *isInViewingMode* message. You can use this information to prevent certain kinds of user actions or changes when the user is viewing an old document revision. Another useful feature for managing locked documents is NSChangeDiscardable. You can use this constant to specify that a particular editing change is non-critical and can be thrown away instead of prompting the user. For example, changing the slide in a Keynote document would normally cause some data to be saved in the document, but Keynote declares that change to be discardable, so the user viewing a locked document can change slides without being prompted to unlock it.

### 安全检查可以阻止无意识的编辑
当保存操作在用户不知情的情况下发生时，它会很容易使无意识操作被保存到磁盘中，这会导致潜在的数据丢失。为了帮助组织自动保存无意识的编辑，NSDocument会执行安全检查来判断用户何时打开了一个文档阅读它而非编辑它。例如，如果该文档在一段时间间隔中都没有被编辑，该文档就会被锁定编辑，，并会开启只读。（当文档被锁定时编辑后的间隔时间是Time Machine系统偏好中的一个选项）NSDocument也会检查那些存在于用户通常不会编辑文档的文件夹中的文档，比如像*~/Downloads*文件夹。

当一个编辑操作作用于该文档时，NSDocument会提供给用户取消更改，使用更改创建一个新文档，或者允许编辑等选择。一个阻止编辑的文档会在标题栏中显式*Locked*。用户可以通过点击*Locked*标签并选择弹出菜单中的*Unlock*以显式启用文档的编辑状态。一个被在其最后一次被打开并激活了Autosave in Place的文档在标题栏中显式*Edited*而不是*Locked*。

一个应用可以以编程的方式通过向其发送*isInViewingMode*消息来判断文档何时被锁定在只读的“viewing mode”状态。你可以在用户正在浏览一个旧文档版本时，使用该信息以阻止某些类型的用户动作或更改。另一个管理锁定文档的有用特性是NSChangeDiscardable。你可以使用该常量以指定一个特定的编辑更改为非关键性的（non-critical），并且可以被丢弃而不是提醒用户。例如，在一个Keynote.app的文档中更改幻灯片通常会导致一些数据被保存在文档中，但是Keynote.app将更改声明为可丢弃，所以当用户查看一个锁定文档时可以更改幻灯片而不用被提醒解锁它。

---

## Document Saving Can Be Asynchronous

In OS X v10.7 and later, NSDocument can save asynchronously, so that document data is written to a file on a background thread. In this way, even if writing is slow, the app’s user interface remains responsive. You can override the method *canAsynchronouslyWriteToURL:ofType:forSaveOperation:* to return YES to enable asynchronous saving. In this case, NSDocument creates a separate writing thread and invokes *writeSafelyToURL:ofType:forSaveOperation:error:* on it. However, the main thread remains blocked until an object on the writing thread invokes the *unblockUserInteraction* method.

When *unblockUserInteraction* is invoked, the app resumes dequeueing user interface events and the user is able to continue editing the document, even if the writing of document data takes some time. The right moment to invoke *unblockUserInteraction* is when an immutable snapshot of the document’s contents has been taken, so that writing out the snapshot of the document’s contents can continue safely on the writing thread while the user continues to edit the document on the main thread.

## 文档保存可以是异步的（asynchronous）

在OS X 10.7和之后的版本中，NSDocument可以异步保存，以便文档数据可以在后台线程中被写入。这样，即使写入操作很慢，应用的用户界面也可以保持响应。你可以覆写*canAsynchronouslyWriteToURL:ofType:forSaveOperation:*方法并返回YES来启用异步保存。在这种情况下，NSDocument会创建一个独立的写线程并在其上调用*writeSafelyToURL:ofType:forSaveOperation:error:*。然而，主线程在调用*unblockUserInteraction*方法之前会一直保持阻塞。

当*unblockUserInteraction*方法被调用时，应用会继续处理用户界面事件并且用户可以继续编辑文档，即使文档数据的写操作会花费一些时间。当已经创建好文档内容的不可变快照之后，就是恰当的调用*unblockUserInteraction*的时刻，这样以便在用户继续在主线程上编辑文档时，还可以继续在写线程上安全地写出文档内容的快照。







 
