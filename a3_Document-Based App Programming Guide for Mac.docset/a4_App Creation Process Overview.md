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

**Table 3-1**  `File` Menu commands in the document-based app template

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

After a document has been saved for the first time, the `Save` command changes to `Save a Version`. In applications that have enabled autosaving in place, the `Save As` and `Save All` items in the `File` menu are hidden, and a `Duplicate` menu item is added. The template has similar ready-made connections for the `Edit`, `Format`, `View`, `Window`, and `Help` menus.

> **Warning:** If your app does not support any of the supplied actions, such as printing, for example, you must remove the associated menu items from the nib. Otherwise, when a user chooses the action, your app could raise an exception or crash.

For your app’s custom menu items that are not already connected to action methods in objects or placeholder objects in the nib file, there are two common techniques for handling menu commands in an OS X app:

* Connect the corresponding menu item to a first responder method.

* Connect the menu item to a method of your custom app object or your app delegate object.

Of these two techniques, the first is more common because many menu commands act on the current document or its contents, which are part of the responder chain. The second technique is used primarily to handle commands that are global to the app, such as displaying preferences or creating a new document. In addition to implementing action methods to respond to your menu commands, you must also implement the methods of the NSMenuValidation protocol to enable the menu items for those commands.

For more information about menu validation and other menu topics, see [Application Menu and Pop-up List Programming Topics.](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MenuList/MenuList.html#//apple_ref/doc/uid/10000032i)

## 回顾一下你的应用程序菜单栏命令

Table 3-1列出了存在于模板中的`文件`的First Responder动作链接。

**Table 3-1**  在文档驱动应用模板中的`文件`菜单命令

文件菜单命令                                      | First Responder动作
:---------------------------------------------- | :----------------------
新建（New）                                      | newDocument:
打开（Open）                                     | openDocument:
最近打开文档（Open Recent） > 清除菜单（Clear Menu）| clearRecentDocuments:
关闭（Close）                                    | performClose:
保存（Save）/ 保存一个版本（Save a Version）        | saveDocument:
还原文档（Revert Document）                       | revertDocumentToSaved:
页面设置（Page Setup）                            | runPageLayout:
打印（Print）                                    | printDocument:

当一个文档第一次被保存后，`保存`命令就会变成`保存一个版本`。在已经允许在适当处自动保存的应用程序中，`文件`菜单中的`另存为`和`全部保存`项会被隐藏，而会添加一个`拷贝`项（Duplicate）。对于`编辑`，`格式`，`视图`，`窗口`，以及`帮助`菜单来说，模板都提供了类似的现成的连接。

> **警告：** 如果你的应用没有提供任何自带菜单项中已提供动作的实现，比如打印，那么你必须从nib中移除关联的菜单项。否则，当用户选择该动作时，你的应用会抛出一个异常或者崩溃。

对于你的应用中的没有连接到对象或者占位符对象中的动作方法的定制菜单项来说，有两条在OS X应用中处理菜单命令的通用技巧：

* 将对应的菜单项连接到First Responder方法

* 将菜单项连接到你的自定义应用对象或者应用委托对象中的方法

在这两种技巧中，第一个更加常用，因为很多菜单命令都是作用于当前文档或者它的内容的，其属于响应者链的一部分。第二条技巧主要用于处理全局的应用命令，比如显示偏好设置或者创建新的文档。除了实现动作方法以响应你的菜单命令之外，你还必须实现NSMenuValidation协议的方法来为这些命令启用菜单项。

更多关于菜单验证的信息以及其他菜单主题，参阅[Application Menu and Pop-up List Programming Topics。](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/MenuList/MenuList.html#//apple_ref/doc/uid/10000032i)




## Complete the Information Property List

You need to configure the project’s information property list so that the app knows what kinds of documents it can handle. You specify this information in the Xcode information property list file, which is shown in Figure 3-2. The property list file is stored in the app’s bundle and named <appName>-Info.plist by default.

When the NSDocumentController object creates a new document or opens an existing document, it searches the property list for such items as the document class that handles a document type, the uniform type identifier (UTI) for the type, and whether the app can edit or only view the type. Similarly, Launch Services uses information about the icon file for the type and to know which app to launch when the user double-clicks a document file. Document type information is associated with the CFBundleDocumentTypes key as an array of dictionaries, each of which contains the key-value pairs that define the document type.

Xcode provides a property list file with every Mac app project. The property list editor appears when you select the Info.plist file in the project navigator or select the target and choose the `Info` pane of the project editor. In the `Info` pane, there’s a list of target properties. You can edit the property values and add new key-value pairs. By default, Xcode displays a user-friendly version of each key name. To see the actual key names that are in the Info.plist file, Control-click an item in the editor and choose `Show Raw Keys/Values` from the contextual menu that appears.

**Figure 3-2**  The information property list editor

![ Figure 3-2 ](http://i.imgbox.com/OdL6Ywd8.png)

For a new document-based app, you should create a document type with a name and extension that make sense for your app. You can add more types as well, one for each of the document types your app handles. The app’s most important document type must be listed first in the list of types. This is the type that NSDocumentController uses by default when the user asks for a new document.

The most important document type value is its Uniform Type Identifier (UTI), a string that uniquely identifies the type of data contained in the document for all apps and services to rely upon. A document’s UTI corresponds to the LSItemContentTypes key in the information property list. The UTI is used as the programmatic type name by NSDocument and NSDocumentController. By using UTIs, apps avoid much of the complexity previously required to handle disparate kinds of file-type information in the system, including filename extensions, MIME types, and HFS type codes (OS types).

A document UTI can be defined by the system, as shown in [“System-Declared Uniform Type Identifiers”](https://developer.apple.com/library/mac/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html#//apple_ref/doc/uid/TP40009259) in [Uniform Type Identifiers Reference](https://developer.apple.com/library/mac/documentation/Miscellaneous/Reference/UTIRef/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009257), or a document-based app can declare its own proprietary UTI. Such custom UTIs must also be exported to make the system aware of them, as described in *“Export Custom Document Type Information.”*

To declare a document type in Xcode, perform the following steps:

    1. Select the project in the project navigator.

    2. Select the target and click the Info tab.

    3. Click the Add (+) button at the bottom right of the editor area and choose Add Document Type from the pop-up menu.

    4. Click the triangle next to “Untitled” to disclose the property fields.

Alternatively, you can select the Info.plist file in the project navigator, click in the editor area, and choose `Editor` > `Add Item` to add document type properties directly to the property list file, as shown in Figure 3-2. Choose `Editor` > `Show Raw Keys & Values` to reveal the actual key names.

Add the properties shown in Table 3-2.

**Table 3-2**  Properties defining a document type (CFBundleDocumentTypes)

Key                     | Xcode field (Info.plist identifier)      | Value
:---------------------- | :--------------------------------------- | :-----------------------------------------------------
LSItemContentTypes      | Identifier                               | An array of UTI strings. Typically, only one is specified per document type. The UTI string must be spelled out explicitly.
NSDocumentClass         | Class (Cocoa NSDocument Class)           | A string specifying the NSDocument subclass name corresponding to this document type.
CFBundleTypeRole        | Role                                     | A string specifying the role the app with respect to this document type. Possible values are Editor, Viewer, Shell, Quick Look Generator, or None.
NSExportableTypes       | (Exportable Type UTIs)                   | An array of strings specifying UTIs that define a supported file type to which this document can export its content.
LSTypeIsPackage         | Bundle (Document is a package or bundle) | A Boolean value specifying whether the document is distributed as a bundle. If NO, omit this value.
CFBundleTypeIconFile    | Icon (Icon File Name)                    | A string specifying the name of the icon resource file (extension .icns) to associate with this document type. An icon resource file contains multiple images at different resolutions.
CFBundleTypeName        | Name (Document Type Name)                | A string specifying the abstract name of the document type.
LSHandlerRank           | Handler rank                             | A string specifying how Launch Services ranks this app among those that declare themselves editors or viewers of documents of this type. Possible values, in order of precedence, are Owner, Alternate, and None.

For more information about these and other document type keys, see “CFBundleDocumentTypes” in [Information Property List Key Reference.](https://developer.apple.com/library/mac/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247)

## 完善信息属性列表

你需要配置工程的信息属性列表一边应用程序知道它可以处理什么类型的文档。你应在Xcode信息属性列表文件中指定该信息，如Figure 3－2中所示。信息属性列表文件被存储在应用的bundle中，并且默认情况下命名为<appName>-Info.plist。

当NSDocumentController对象创建一个新的文档或者打开一个已存在的文档时，它就会搜索属性列表来获取诸如处理一个文档类型的文档类，某个类型的UTI，以及该应用是可以编辑该类型还是只能浏览等信息。同样地，启动服务（Launch Services）会使用关于某个类型的图标文件的信息以及去了解当用户双击一个文档文件时那一个应用会被启动。文档类型信息会作为一个词典数组与CFBundleDocumentTypes键关联，每个词典中包含定义文档类型的键值对。

Xcode为每个Mac应用工程提供一个属性列表文件。当你在工程导航器中或选中Info.plist文件，或者选中目标并选择工程编辑器的`Info`面板时，属性列表编辑器就会显示。在`Info`面板中，有一系列的目标属性。你可以编辑这些属性值以及添加新的键值对。默认情况下，Xcode会为每个键名称显示一个用户有好的版本。要查看在Info.plist文件中的实际的键名称，可以按下Control并单击编辑器中的一个项，并从显示的上下文菜单中选择`Show Raw Keys/Values`。

**Figure 3-2**  信息属性列表编辑器

![ Figure 3-2 ](http://i.imgbox.com/OdL6Ywd8.png)


对于一个新的文档驱动应用程序，你应该使用一个类型名和一个你的应用能够理解的扩展名来创建文档类型。你也可以添加更多的类型，每个类型都对应着你的应用可以处理的一个文档类型。应用的最重要的文档类型必须被列在类型列表中的首位。当用户请求一个新文档时，NSDocumentController就会默认使用该类型。

最重要的文档类型值是一它的**统一类型标识符（UTI）**，这是一个为所有应用和服务所依赖的，唯一标识包含在文档中的数据类型的字符串。一个文档的UTI对应于信息属性列表中的LSItemContentTypes键。UTI通过NSDocument和NSDocumentController被用作可编程的类型名。通过使用UTIs，应用避免了许多之前处理系统中的不同种类的文件类型信息的复杂性，包括文件扩展名，MIME类型，以及HFS类型代码（OS类型）。

一个文档UTI可以由系统定义，如[“System-Declared Uniform Type Identifiers”](https://developer.apple.com/library/mac/documentation/Miscellaneous/Reference/UTIRef/Articles/System-DeclaredUniformTypeIdentifiers.html#//apple_ref/doc/uid/TP40009259) in [Uniform Type Identifiers Reference](https://developer.apple.com/library/mac/documentation/Miscellaneous/Reference/UTIRef/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009257)所示，或者一个文档驱动应用定义它自己的专有UTI。这样定制的UTIs还必须被导出以创建它们的识别系统，如*“Export Custom Document Type Information.”*中所描述。

要在Xcode中声明一个文档类型，需执行如下步骤：

    1. 选择工程导航器中的工程。

    2. 选择目标，并点击Info标签。

    3. 点击编辑器区域底部右侧的Add(+)按钮，并从弹出菜单中选择Add Document Type。

    4. 点击下一个三角形展开属性域。

或者，你可以在工程导航器中选择Info.plist文件，点击编辑器区域，并选择`Editor` > `Add Item`以直接添加文档类型属性到属性列表文件中，如Figure 3-2所示。选择`Editor` > `Show Raw Keys & Values`以显示真正的键名。

Table 3-2中展示了添加属性

**Table 3-2**  定义文档类型（CFBundleDocumentTypes）的一些属性

键                      | Xcode域（Info.plist标识符）                | 值
:---------------------- | :--------------------------------------- | :----------------------------------------------------------
LSItemContentTypes      | Identifier                               | 一个UTI字符串数组。通常地，每个文档类型只被指定一个。UTI字符串必须清楚明确。
NSDocumentClass         | Class (Cocoa NSDocument Class)           | 该字符串指定了与该文档类型相对应的NSDocument子类的名称。
CFBundleTypeRole        | Role                                     | 该字符串指定了应用程序对该文档类型所扮演的角色。可能的值有Editor，Viewer，Shell，Quick Look Generator或者None。
NSExportableTypes       | (Exportable Type UTIs)                   | 该字符串数组指定了定义该文档可以导出其内容的支持文件的UTIs。
LSTypeIsPackage         | Bundle (Document is a package or bundle) | 该Boolean值指定了文档是否部署为一个bundle。如果值为NO，忽略该值。
CFBundleTypeIconFile    | Icon (Icon File Name)                    | 该字符串指定了与该文档类型相关联的图标资源文件（扩展名为.icns）。一个图标资源文件包含了不同分辨率的图像。
CFBundleTypeName        | Name (Document Type Name)                | 该字符串指定了文档类型的抽象名称。
LSHandlerRank           | Handler rank                             | 该字符串指定了启动服务（Launch Services）如何为那些声明为该类型文档的编辑器或查看器的应用程序排列优先级。可能的值为按优先级排序为Owner，Alternate以及None。

更多关于这些及其他文档类型键的信息，参阅[Information Property List Key Reference](https://developer.apple.com/library/mac/documentation/General/Reference/InfoPlistKeyReference/Introduction/Introduction.html#//apple_ref/doc/uid/TP40009247)中的“CFBundleDocumentTypes”。





