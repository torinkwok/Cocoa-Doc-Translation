# App Creation Process Overview

It is possible to put together a document-based app without having to write much code. You have only to create a document project, compose the human interface, complete the *information property list* for your document types, implement a subclass of NSDocument, and add any other custom classes or behavior required by your app.

If you intend to sell your app through the Mac App Store or use iCloud storage, you also need to create an explicit App ID, create provisioning profiles, and enable the correct entitlements for your app. These procedures are explained in [App Distribution Guide.](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582)

# 应用程序创建过程概述
不必编写很多代码就组装出一个文档驱动应用是有可能的。你只须创建一个文档项目，构建用户界面，完成*信息属性列表（information property list）*，实现NSDocument子类，并且添加任何你的应用所必需的定制类或行为。

如果你打算通过Mac App Store销售你的应用或者要使用iCloud进行存储，你还需要创建一个显示的App ID，创建供应配置文件（provisioning profiles），以及为你的应用设置正确的权限。这些过程在[App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582)中作了解释。

## Xcode Provides a Document-Based App Template

To expedite the development of document-based apps, Xcode provides a Cocoa Application template, which has the option to make the app document based. The template provides the following things:

* **A skeletal NSDocument subclass implementation.** The document subclass implementation (.m) file includes commented blocks for important methods, including an *init* method that initializes and returns self. This method provides a location for subclass-specific initialization. The template also includes a fully implemented windowNibName method that returns the name of the document window nib file. An override of windowControllerDidLoadNib: provides a place for code to be executed after the document’s window nib has finished loading. In addition, the template includes skeletal implementations of the dataOfType:error: and readFromData:ofType:error: basic writing and reading methods; these methods throw an exception if you don’t supply a working implementation. Finally, the template includes an override of the autosavesInPlace class method that returns YES to turn on automatic saving of changes to your documents.

* **A nib file for the app’s document.** This nib file is named with your NSDocument subclass name with the extension .xib. The subclass of NSDocument is made File’s Owner of the nib file. It has an outlet named window connected to its window object, which in turn has a delegate outlet connected to the File’s Owner, as shown in Figure 2-3. The window has only one user interface object in it initially, a text field with the words "Your document contents here".

* **The app’s menu bar nib file.** The menu bar nib file, named MainMenu.xib, contains an app menu (named with the app’s name), a File menu (with all of its associated document commands), an Edit menu (with text editing commands and Undo and Redo menu items), and Format, View, Window, and Help menus (with their own menu items representing commands). These menu items are connected to the appropriate first-responder action methods. For example, the About menu item is connected to the orderFrontStandardAboutPanel: action method that displays a standard About window.
See “Review Your App Menu Bar Commands” for more information about the menu bar nib file provided by the Xcode app templates.

* **The app's information property list.** The <appName>-Info.plist file contains placeholder values for global app keys, as well as for the CFBundleDocumentTypes key, whose associated value is a dictionary containing key-value pairs specifying information about the document types the app works with, including the NSDocument subclass for each document type.

The following sections describe the process of selecting and utilizing the document-based app template.

## Xcode提供了文档驱动应用模板










