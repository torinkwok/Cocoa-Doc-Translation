# Information property list

An information property list is structured text specifying configuration details for an application or other bundled executable. The operating system extracts data from an information property list at runtime and processes it in suitable ways. For example, when they list applications in the Home screen or in the Finder, iOS and OS X (respectively) get these names from the information property lists of installed applications.

The contents of an information property list are structured in a special form of XML where the root node is always a dictionary. The dictionary contains a series of key-value pairs, or properties, where the key is a key element and the value is an element that indicates the data type of the value.

# 信息属性列表

信息属性列表是用于指定应用程序或其他可执行bundle的配置细节的结构化文本。操作系统会在运行时从一个信息属性列表中提取数据并使用适当的方式处理它。例如，当它们在Home屏幕或者Finder中列出应用程序时，iOS和OS X（分别地）会从已安装的应用程序的信息属性列表中过去这些名称。

信息属性列表的内容使用一种根节点总是词典的特殊XML形式进行结构化。词典中包含了一连串的键值对（key-value pairs），或者属性（properties），键是一个键元素并且值是一个标明值的数据类型的元素。

---