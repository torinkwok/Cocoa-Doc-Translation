# App Creation Process Overview

It is possible to put together a document-based app without having to write much code. You have only to create a document project, compose the human interface, complete the *information property list* for your document types, implement a subclass of NSDocument, and add any other custom classes or behavior required by your app.

If you intend to sell your app through the Mac App Store or use iCloud storage, you also need to create an explicit App ID, create provisioning profiles, and enable the correct entitlements for your app. These procedures are explained in [App Distribution Guide.](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582)

# 应用程序创建过程概述
不必编写很多代码就组装出一个文档驱动应用是有可能的。你只须创建一个文档工程，构建用户界面，完成*信息属性列表（information property list）*，实现NSDocument子类，并且添加任何你的应用所必需的定制类或行为。

如果你打算通过Mac App Store销售你的应用或者要使用iCloud进行存储，你还需要创建一个显示的App ID，创建供应配置文件（provisioning profiles），以及为你的应用设置正确的权限。这些过程在[App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582)中作了解释。

## Xcode Provides a Document-Based App Template

To expedite the development of document-based apps, Xcode provides a Cocoa Application template, which has the option to make the app document based. The template provides the following things:

* **A skeletal NSDocument subclass implementation.** The document subclass implementation (.m) file includes commented blocks for important methods, including an *init* method that initializes and returns self. This method provides a location for subclass-specific initialization. The template also includes a fully implemented *windowNibName* method that returns the name of the document window nib file. An override of *windowControllerDidLoadNib:* provides a place for code to be executed after the document’s window nib has finished loading. In addition, the template includes skeletal implementations of the *dataOfType:error:* and *readFromData:ofType:error:* basic writing and reading methods; these methods throw an exception if you don’t supply a working implementation. Finally, the template includes an override of the *autosavesInPlace* class method that returns YES to turn on automatic saving of changes to your documents.

* **A nib file for the app’s document.** This nib file is named with your NSDocument subclass name with the extension .xib. The subclass of NSDocument is made File’s Owner of the nib file. It has an outlet named *window* connected to its window object, which in turn has a delegate outlet connected to the File’s Owner, as shown in **Figure 2-3**. The window has only one user interface object in it initially, a text field with the words "Your document contents here".

* **The app’s menu bar nib file.** The menu bar nib file, named MainMenu.xib, contains an app menu (named with the app’s name), a `File` menu (with all of its associated document commands), an `Edit` menu (with text editing commands and `Undo` and `Redo` menu items), and `Format`, `View`, `Window`, and `Help` menus (with their own menu items representing commands). These menu items are connected to the appropriate first-responder action methods. For example, the `About` menu item is connected to the *orderFrontStandardAboutPanel:* action method that displays a standard `About` window.

See *“Review Your App Menu Bar Commands”* for more information about the menu bar nib file provided by the Xcode app templates.

* **The app's information property list.** The <appName>-Info.plist file contains placeholder values for global app keys, as well as for the CFBundleDocumentTypes key, whose associated value is a dictionary containing key-value pairs specifying information about the document types the app works with, including the NSDocument subclass for each document type.

The following sections describe the process of selecting and utilizing the document-based app template.

## Xcode提供了文档驱动应用模板

为了方便文档驱动应用的开发，Xcode提供了一个Cocoa应用模板，其拥有使应用成为文档驱动的选项。模板提供了如下事物：

* **一个NSDocument子类的骨架实现。** NSDocument子类的实现文件（.m)为重要的方法包含了注释块，包括一个执行初始化并返回self的*init*方法。该方法为特定于子类的初始化提供了位置。模板还包含了一个*windowNibName*方法的返回文档窗口nib文件名的完整实现。*windowControllerDidLoadNib:*的覆写为在文档窗口nib完成加载后要执行的代码提供了位置。此外，模板还包括了*dataOfType:error*和*readFromData:ofType:error:*基本读写方法的骨架实现；如果你没有提供一个可以工作的实现，这两个方法会抛出异常。最后，模板包含了一个*autosavesInPlace*方法的覆写，该实现返回YES以打开你的文档更改的自动保存。

* **一个为应用的文档提供的nib文件。** 该nib文件使用你的NSDocument子类加上.xib扩展名来命名。NSDocument子类被认为是该nib文件的File' Owner。其拥有一个名为*window*的插座连接到它的窗口对象，该窗口对象反过来拥有一个连接到File's Owner的委托插座，如**Figure 2-3**所示。窗口在初始时仅拥有一个用户界面对象，即一个显示“Your document contents here”字样的文本域（text filed）。

* **应用的菜单栏nib文件。** 菜单栏nib文件被命名为MainMenu.xib，其包含了一个应用菜单（以应用的名字命名），一个`文件`菜单（支持全部与文档相关联的命令），一个`编辑`菜单（支持文本编辑命令及`撤销`和`重做`菜单项），以及`格式`，`视图`，`窗口`，和`帮助`菜单（提供它们各自的展现命令的菜单项）。这些菜单项都被连接到First Responder的适当的动作方法上。例如`关于`菜单项就被连接到*orderFrontStandardAboutPanel:*用于显示标准`关于`窗口的动作方法上。

参阅*“Review Your App Menu Bar Commands”*以获得更多关于由Xcode应用模板提供的菜单nib栏文件（MainMenu）的信息。

* **应用的信息属性列表。** <appName>-Info.plist文件包含了针对全局应用键的占位符，以及CFBundleDocumentType键，其关联值是一个包含指定关于与应用一同工作的文档类型信息的键值对的字典，为每个文档类型提供了一个NSDocument子类。

下面的章节描述了选择和使用文档驱动应用模板的过程。



## Create the Project

To create your project in Xcode, choose `File` > `New` > `New Project`. Select the Cocoa Application icon from the OS X Application choices. In the next pane, select the `Create Document-Based Application` option, as shown in Figure 3-1. In this pane you also name your app, give your NSDocument subclass a prefix, and specify your documents’ filename extension, in addition to other options. If you intend to use Core Data for your data model, select the `Use Core Data` option, which automatically inserts NSPersistentDocument as the immediate superclass of your document subclass.

**Figure 3-1**  New Project dialog

The final pane of the `New Project` dialog enables you to place your project in the file system and create a source control repository if you wish. For more details about the Xcode project creation process, see [“Start a Project”](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/ProjectsWorkspaces/start_project.html#//apple_ref/doc/uid/TP40010215-CH2) in [Xcode Overview.](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215)

Without writing any additional code, you can compile and run the app. When you first launch the app, you see an untitled document with an empty window. The `File` menu commands all do something reasonable, such as bringing up a `Save` dialog or `Open` dialog. Because you have not yet defined any types or implemented loading and saving, you can't open or save anything, and the default implementations throw an exception.

要在Xcode中创建你的工程，需选择`File` > `New` > `New Project`。选择OS X应用程序选项中的Cocoa Application图标。在下一个面板中，选择`Create Document-Based Application`选项，如Figure 3-1所示。在该面板中除了其他选项，你还可以要命名你的应用，为你的NSDocument子类给定前缀，以及指定你的文档的文件扩展名。如果你打算为你的数据模型使用Core Data，选择`Use Core Data`选项，该选项会自动插入NSPersistentDocument来作为你的文档子类直接超类。

**Figure 3-1**  New Project对话框
![ Figure 3-1 ](http://i.imgbox.com/0xKaFG5q.png)

`New Project`对话框的最终面板允许你将你的工程放置到文件系统中，并且如果你希望还可以创建一个源代码控制仓库。更多关于Xcode工程创建过程的细节，参阅[Xcode Overview](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215)中的[“Start a Project”。](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/ProjectsWorkspaces/start_project.html#//apple_ref/doc/uid/TP40010215-CH2)

无须编写任何额外的代码，你就可以编译并运行该应用。当你第一次运行该应用时，你会看到一个使用空窗口的无标题文档。`文件`菜单命令全部都会做一些合理的事情，比如呼出`保存`或者`打开`对话框。因为你还没有定义任何类型或者实现加载与保存，所以你无法打开或保存任何事物，并且默认实现会抛出一个异常。



## Create Your Document Window User Interface

To create the user interface for your document window, in the project navigator area, click the nib file named with your NSDocument subclass name with the extension .xib. This opens the file in Interface Builder, an Xcode editor that provides a graphical interface for the creation of user interface files. You can drag user interface elements onto the document window representation from the Interface Builder Object library in the utility area. If the objects in the document window require outlets and actions, add them to your NSDocument subclass. Connect these actions and outlets via the File’s Owner icon in the list of placeholders in the Interface Builder dock. If your document objects interact with other custom objects, such as model objects that perform specialized computations, define those objects in Interface Builder and make any necessary connections to them.

Step-by-step instructions for connecting menu items to action methods in your code are given in [“Edit User Interfaces”](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/Edit_User_Interfaces/edit_user_interface.html#//apple_ref/doc/uid/TP40010215-CH6) in[Xcode Overview.](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215)

## 创建你的文档窗口用户界面

要为你的文档窗口创建用户界面，需在工程导航区域中点击以你的NSDocument子类加上.xib扩展名命名的nib文件。这会在Interface Builder中打开该文件，Interface Builder是一个Xcode中的为用户界面文件的创建提供图形化界面的编辑器。你可以将用户界面元素从工具区域的Interface Builder对象库中拖拽到文档窗口表示上。如果在文档窗口中的对象需要插座和动作，可以将它们添加到你的NSDocument子类中去。通过在Interface Builder的dock中的一列占位符中的File' Owner图标来连接这些动作和插座。如果你的文档对象要与其他定制对象交互，比如执行特定计算任务的模型对象，那么就在Interface Builder中定义这些对象，并且为它们创建任何需要的连接。

在[Xcode Overview.](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/About_Xcode/about.html#//apple_ref/doc/uid/TP40010215)的[“Edit User Interfaces”](https://developer.apple.com/library/mac/documentation/ToolsLanguages/Conceptual/Xcode_Overview/Edit_User_Interfaces/edit_user_interface.html#//apple_ref/doc/uid/TP40010215-CH6)中一步一步地指导你如何在你的代码中连接菜单项到动作方法。



## Review Your App Menu Bar Commands

Table 3-1 lists the `File` menu first-responder action connections that exist in the template.

**Table 3-1**  File Menu commands in the document-based app template

File menu command        | First-responder action
:----------------------- | :----------------------
New                      | newDocument:
Open                     | openDocument:
Open Recent > Clear Menu | clearRecentDocuments:
Close                    | performClose:
Save/Save a Version      | saveDocument:
Revert Document          | revertDocumentToSaved:
Page Setup               | runPageLayout:
Print                    | printDocument:

After a document has been saved for the first time, the `Save` command changes to `Save a Version`. In applications that have enabled autosaving in place, the `Save As` and `Save All` items in the File menu are hidden, and a `Duplicate` menu item is added. The template has similar ready-made connections for the `Edit`, `Format`, `View`, `Window`, and `Help` menus.

> **Warning:** If your app does not support any of the supplied actions, such as printing, for example, you must remove the associated menu items from the nib. Otherwise, when a user chooses the action, your app could raise an exception or crash.
For your app’s custom menu items that are not already connected to action methods in objects or placeholder objects in the nib file, there are two common techniques for handling menu commands in an OS X app:

* Connect the corresponding menu item to a first responder method.

* Connect the menu item to a method of your custom app object or your app delegate object.

Of these two techniques, the first is more common because many menu commands act on the current document or its contents, which are part of the responder chain. The second technique is used primarily to handle commands that are global to the app, such as displaying preferences or creating a new document. In addition to implementing action methods to respond to your menu commands, you must also implement the methods of the NSMenuValidation protocol to enable the menu items for those commands.

For more information about menu validation and other menu topics, see [Application Menu and Pop-up List Programming Topics.](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MenuList/MenuList.html#//apple_ref/doc/uid/10000032i)







