We can create menu items that trigger / run Apps Script functions.
Such functions run with elevated permissions and can do things functions called from a cell [[Formula]] can't.
For example [[Writing To Cells]] or communicating with other Google Apps such as [[Calendar]].

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
You may need to close and reopen the spreadsheets document, or refresh the page (F5), for the menu items to update.

# Sub-menus

Sub-menus are created with `addSubMenu` and populated with the same `addItem` function.

```js
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu("My Menu Label")
    .addItem("Top Level Item 1", "topLevelFunction1")
    .addItem("Top Level Item 2", "topLevelFunction2")
    .addSubMenu(ui.createMenu("My Sub Menu")
	    .addItem("Nested Level Item 1", "nestedLevelFunction1")
	    .addItem("Nested Level Item 2", "nestedLevelFunction2"))
	.addItem("Top Level Item 3", "topLevelFunction3")
    .addToUi();
}

function topLevelFunction1() {
  // Do stuff here.
}

function topLevelFunction2() {
  // Do stuff here.
}

function nestedLevelFunction1() {
  // Do stuff here.
}

function nestedLevelFunction2() {
  // Do stuff here.
}

function topLevelFunction3() {
  // Do stuff here.
}
```