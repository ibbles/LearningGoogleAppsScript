Google Sheets is unreliable in the sense that changing the value in a cell may not trigger an update of cells that depend on that value.
The problem stems from the fact that recalculating all cells for every change is too costly,
and Google Sheets cannot predict / determine which cells a function will read from.
We must therefore tell it.
Every function that reads from the sheet MUST be passed the range of cells it reads as arguments in the cell formula.

# Pass Input Range

The following cell formula is bad because it doesn't communicate which cells the function may read:
```js
=myFuntionThatReadsCellValues()
```

The following cell formula is OK as long as the function does not read any cell outside of the given range:
```js
=myFunctionThatReadsCellValues(B5:D10)
```

The function does not have to read all values in the range.
Giving an unnecessarily large range can have a negative influence on performance since the function would be run for no reason whenever any value within the range is changed.

The risk of  not specifying correct ranges, or forgetting to update the range when the data layout changes, is high.
Which makes Apps Script unsuitable for high-value use-cases.

# Force Refresh

If you cannot provide a range that reliably covers all possible cells the function may read,
the the second best thing is to create a force update button.
This is a button connected to a script that removes and re-enters the formula in the selected cell,
forcing a recalculation of its value.

The user of the sheet must:
- Know that a particular cell should get a new value.
- Select the cell.
- Click the button.

The risk of forgetting to do this make Apps Script unsuitable for high-value use-cases.

If you know that only formulas, not data such as number and strings, will be used, then the following functions can be used.
Add the following to the spreadsheet's script:
```js
function onOpen() {
  var ui = SpreadsheetApp.getUi();
  ui.createMenu("Learning Apps Script")
    .addItem("Force update selected cells", "forceUpdate")
    .addToUi();
}

function forceUpdate() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var range = sheet.getActiveRange();
  var formulas = range.getFormulas();
  range.clearContent();
  SpreadsheetApp.flush();
  // DANGER! Only formulas are preserved. Data such as numbers
  // and strings will be lost.
  range.setFormulas(formulas);
}
```

[[Clear A Sheet Or Range]]

Then restart / refresh the spreadsheets tab to re-run the `onOpen` callback.
This will add a Learning Apps Script menu to the Top Menu Bar and in that a Force Update Selected Cells item.
To use, select the cells with formulas that need re-evaluation and select Top Menu Bar > Learning Apps Script > Force Update Selected Cells.

If you want to preserve data as well then the following extended version of `forceUpdate` may work.
```js
function forceUpdate() {
  var sheet = SpreadsheetApp.getActiveSheet();
  var range = sheet.getActiveRange();
  var formulas = range.getFormulas();
  var values = range.getValues();
  range.clearContent();
  SpreadsheetApp.flush();

  // Sanity check.
  if (formulas.length != values.length) {
    SpreadsheetApp.getUi().alert("Formulas and values are not the same size, cannot continue.");
    return;
  }
  
  var numRows = formulas.length;
  if (numRows == 0) {
    return;
  }

  // Assuming that all rows have the same number of columns,
  // and that the values have the same number as the formulas.
  var numCols = formulas[0].length;
  if (numCols == 0) {
    return;
  }

  // Update each and every cell in the range.
  // Write a formula if there was one,
  // otherwise write a value.
  for (var row = 0; row < numRows; ++row) {
    for (var col = 0; col < numCols; ++col) {
      var formula = formulas[row][col];
      var value = values[row][col];
      // Note that arrays (formulas and values) use zero-based indexing,
      // while cells use one-based indexing. So we must add one to got
      // from array index to cell index.
      if (formula != "") {
        range.getCell(row+1, col+1).setFormula(formula);
      }
      else {
        range.getCell(row+1, col+1).setValue(value);
      }
    }
  }
}
```

# References

- [_Google App Function - Recalculate/Refresh values_ by Tanaike @ stackoverflow.com 2019](https://stackoverflow.com/questions/56462700/google-app-function-recalculate-refresh-values)
- [Reply to _My Function is not refreshing when cells are updated_ by --Hyde @ support.google.com 2022](https://support.google.com/docs/thread/55874976?hl=en&msgid=56034420)
