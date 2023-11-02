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


# Getting The Active Cell

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


# Getting Any Range

We can access any arbitrary cell in a sheet using `getRange`, and access the data of that cell using `getValue`.
There are multiple overloads of `getRange`.
The following example uses integer indexing to read and return the value of the neighboring cell to the left,
i.e. with a column number one less than the active cell.
Make sure to not run this function when the active cell is on the far left of the sheet.
```js
function readNeighbor() {
  const sheet = SpreadsheetApp.getActiveSheet();
  const cell = sheet.getActiveCell();
  const row = cell.getRow(); // The integer index, one-based, of the current row.
  const col = cell.getCol(); // The integer index, one-based, of the current column.
  const neighbor = sheet.getRange(row, col - 1);
  return neighbor.getValue();
}
```
The rule regarding indexing is that whenever we talk to the API then it's one-based,
and whenever we talk to JavaScript arrays then it's zero-based.
Notice that the order to `getValue` is (row, column),
which is swapped compared to A1 notation, which has the column first and the row second.

A range can be more than a single cell.
By passing a third index parameter we select the number of rows to include down.
This makes the range a vertical line, selecting a range of a single column.
By passing a forth index parameter we extend the selection to the right, creating a rectangular selection.
```js
sheet.getRange(row, col, numRowsDown, numColsRight);
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

We can pass a range to `getRange` to select multiple cells.
```js
function readB5ToD10()
{
  var sheet = SpreadsheetApp.getActiveSheet();
  var cell = sheet.getRange("B5:D10");
  return cell.getValues();
}
```

Ranges one one-based and inclusive.
This means that the top-left cell is A1, there is no A0, and the D10 cell is included in the example above.
