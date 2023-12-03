We can display HTML dialog boxes, including interaction with our JavaScript code.
This is done through the HTML Service, named `HtmlServer` in Apps Script.

The HTML to display is created as a separate file in the Files panel.
Click the + button, select HTML, type a name for the HTML file, excluding the `.html` suffix which is added automatically.
For this example we use the name `HelloWorld`.
This will produce a HTML document with some boilerplate code.
Add your content within the `<body>` tag.

`HelloWorld.html`:
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <p>Hello, World!</p>
  </body>
</html>
```

Create a function to display the HTML page in a dialog.
Dialog windows created this way can only be shown from interactive contexts such as from a menu item.
They cannot be used from a [[Formula]] or using the Run button from the Apps Script IDE.
```js
function onLoad() {
	SpreadsheetApp.getUi().createMenu("My Menu")
		.addItem("Show HTML Dialog", "showHtmlDialog")
		.addtoUi();
}

function showHtmlDialog() {
	SpreadsheetApp.getUi().showModalDialog(
		HtmlService.createTemplateFromFile("HelloWorld").evaluate(),
		"My Dialog Title");
}
```

The above produces a HTML dialog with the title `My Dialog Title`, a close button, and the text `Hello, World!`.

From the Google Sheets document select Top Menu Bar > My Menu > Shove HTML Dialog.
A dialog windows opens, displaying the text `Hello, World!`.

# Scriptlet

A scriptlet is a small JavaScript snippet embedded in the HTML document.
The script is evaluated server-size before the HTML is sent to the client.
This means that the scriptlet is only run once.
A scriptlet is introduced with the `<?` tag start and ended with the `?>` tag end.
There are a few different types of scriptlet tag starts:
- `<?`: Only run the script, does not by itself have any effect on the HTML document.
- `<?=`: Evaluate the expression, convert the result to a string and embed into the HTML document.
- `<?!=`: Not sure. Something about unconditional evaluation. More reading required.

The following HTML page shoes the Hello, World! text in all-lowercase, i.e. `hello, world!`.
The JavaScript code to display it is the same as above.
`HelloWorld.html`:
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <p><?= "Hello, World!".toLowerCase() ?></p>
  </body>
</html>
```


# Call Apps Script Function From Scriptlet

We can call our Apps Script functions from a scriptlet.

`HelloWorld.html`:
```html
<html>
  <head>
    <base target="_top">
  </head>
  <body>
    <p><?= getGreeting() ?></p>
  </body>
</html>
```

```js
function onLoad() {
	SpreadsheetApp.getUi().createMenu("My Menu")
		.addItem("Show HTML dialog", "showHtmlDialog")
		.addtoUi();
}

function showHtmlDialog() {
	SpreadsheetApp.getUi().showModalDialog(
		HtmlService.createTemplateFromFile("HelloWorld").evaluate(),
		"My Dialog Title");
}

function getGreeting() {
	return "Hello, World!";
}
```


# Interactive Element - Button

The HTML page can contain interactive elements, such as buttons, and those interactive elements can call our Apps Script functions.
To access the Apps Script library of functions we must prefix their names with `google.script.run.`.
Otherwise symbol lookup is done within the scope of the HTML page and its JavaScript context.
In the following example:
- `onButtonClicked` is the function within the `<script>` tag. 
- `google.script.run.onButtonClicked` is the Apps Script function.

`Button.html`:
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onButtonClicked(event) {
        google.script.run.onButtonClicked();
      }
    </script>
  </head>
  <body>
    <button type="button" onclick="onButtonClicked()">My Button</button>
  </body>
</html>
```

```js
function onLoad() {
	SpreadsheetApp.getUi().createMenu("My Menu")
		.addItem("Show HTML dialog", "showHtmlDialog")
		.addtoUi();
}

function showHtmlDialog() {
  SpreadsheetApp.getUi().showModalDialog(
    HtmlService.createTemplateFromFile("Button").evaluate(),
    "My Button");
}

function onButtonClicked() {
  Logger.log("Button clicked.");
}
```

In the Apps Script IDE open the Execution Log.
In the Google Sheets document select Top Menu Bar > My Menu > Show HTML Dialog.
After some delay a window with a button opens.
Click the button however many times you want.
Each time a new entry is created for `onButtonClicked` in the execution log.

# Communicating Back To The HTML

Apps Script functions called from the HTLM page cannot directly return anything.
The `google.script.run` "function" doesn't propagate the return value.
In fact, the function is run asynchronously (I think.) which means that the return value doesn't even exist by the time the HTML-page script continues executing.
We can register a callback function to give us the return later, when it is ready.
```js
// This is a JavaScript function in the HTML document.
function onHtmlEvent() {
	google.script.run.withSuccessHandler(myCallback).myAppsScriptFunction();
	function myCallback(returnValue) {
		// Use the return value to do something.
	}
}
```

Here is an example that adds an Apps Script generated entry to an HTML list every time a button is pressed.

`Page.html`:
```html
<!DOCTYPE html>
<html>
  <head>
    <base target="_top">
    <script>
      function onButtonClicked(event) {
        google.script.run.withSuccessHandler(onListItemReceived).queueGenerateNextListItem();
        function onListItemReceived(listItem) {
          var ul = document.getElementById("myList");
          var li = document.createElement("li");
          li.appendChild(document.createTextNode(listItem));
          ul.appendChild(li);
        }
      }
    </script>
  </head>
  <body>
    <button type="button" onclick="onButtonClicked()" >My Button</button>
    <ul id="myList">
    </ul>
  </body>
</html>
```

`Code.gs`:
```js
function onLoad() {
	SpreadsheetApp.getUi().createMenu("My Menu")
		.addItem("Show HTML dialog", "showHtmlDialog")
		.addtoUi();
}

function showHtmlDialog() {
  SpreadsheetApp.getUi().showModalDialog(
    HtmlService.createTemplateFromFile("Page").evaluate(),
    "Title");
}

function queueGenerateNextListItem() {
  return `Button clicked on ${new Date()}`;
}
```

Each time the button is clicked a new row is added to the HTML dialog displaying the time at which the button was pressed.


# References

- [_HTML Service: Templated HTML_ by Google @ developers.google.com](https://developers.google.com/apps-script/guides/html/templates)
