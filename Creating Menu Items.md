We can create menu items that trigger / run Apps Script functions.
Such functions run with elevated permissions and can do things functions called from cell [[Formula]] can't.
For example [[Writing To Cells]].

Use the `createMenu` and `addItem` functions to create menu items and bind them to callback functions.
The following creates a menu item that calls the `myFunction` function.
```js
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu("My Menu Label")
    .addItem("My Menu Item Label", "myFunction")
    .addToUi();
}

function myFunction() {
  // Do stuff here.
}
```

`onOpen` is a system function that Google Spreadsheet calls when opening a document.
You may need to close and reopen the document, or refresh the page (F5) for the menu items to update.