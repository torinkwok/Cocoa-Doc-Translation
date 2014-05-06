# Toolbar Management Checklist

## Before you begin coding:

* If you have image-based toolbar items, find or create the images (in the proper size and aspect ratio) and add them to your project as a resource.

* If you have view-based toolbar items, create each view in Interface Builder, specify an outlet for a custom controller object, and connect the view to the outlet.

* If the view is an off-the-shelf palette object, just make an outlet connection.

* Specify or (for default toolbar items) identify the unique string identifiers that you intend to use for toolbars and toolbar items.

* Add to an application menu (usually named View) the menu items Show Toolbar and Customize Toolbar..., connect these to the First Responder icon in the nib file window, and select the actions toggleToolbarShown: and runToolbarCustomizationPalette:. (Note that NSWindow automatically changes “Show Toolbar” to “Hide Toolbar” as appropriate.)

For further information, see “Adding and Removing Toolbar Items.”