# Creating the Subclass of NSDocument

The NSDocument subclass provides storage for the model and the ability to load and save document data. It also has any outlets and actions required for the user interface. The NSDocument object automatically creates an NSWindowController object to manage that nib file, but the NSDocument object serves as the File’s Owner proxy object for the nib file.

When you subclass NSDocument, you must override certain key methods and implement others to do at least the following things:

* Read data of existing documents from files

* Write document data to files

* Initialize new documents

* Put documents into iCloud and remove them

In particular, you must override one reading and one writing method. In the simplest case, you can override the data-based reading and writing methods, *readFromData:ofType:error:* and *dataOfType:error:*.

