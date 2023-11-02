From an Apps Script we can get a hold of the context from which the call to our function was made.
That is, the cell that contains the expression that is currently being evaluated.
We need to traverse the spreadsheet hierarchy described in [[Spreadsheet Concepts]].

- Application - Google Sheets.
	- There is a global variable named `SpreadsheetApp` that represents the Google Sheets application as a whole.
- Spreadsheets - A single document.
	- We can get the current spreadsheet from `SpreadsheetApp` by calling `getActiveSpreadsheet`.
- Sheet - A tab within a spreadsheet document.
	- We can get the current sheet from the spreadsheet by calling `getActiveSheet`.
- Cell -
	- We can get the current cell from the sheet by calling `getActiveCell`.

Example getting the cell that triggered the current function evaluation:
```js
function getCellCoordinate() {
  var app = SpreadsheetApp;
  var spreadsheet = app.getActiveSpreadsheet();
  var sheet = spreadsheet.getActiveSheet();
  var cell = sheet.getActiveCell();
  var row = cell.getRow()
  var col = cell.getColumn();
  return [row, col];
}
```

A shorthand to get the active sheet is
```js
var sheet = SpreadsheetApp.getActiveSheet();
```

We can access any arbitrary cell in a sheet using `getRange`, and access the data of that cell using `getValue`.
The following example reads and returns the value of the neighboring cell to the left, i.e. with a column number one less than the active cell.
```js
function readNeighbor() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var cell = sheet.getActiveCell();
  var neighbor = sheet.getRange(cell.getRow(), cell.getColumn() - 1);
  return neighbor.getValue();
}
```

In addition to integer based cell indexing we can also use A1-based indexing.
```js
function readB5()
{
  var sheet = SpreadsheetApp.getActiveSheet();
  var cell = sheet.getRange("B5");
  return cell.getValue();
}
```

