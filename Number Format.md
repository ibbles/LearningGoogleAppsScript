Set the number format of a cell with `setNumberFormat`.
Get the cell as a [[Range]].

```js
const cell = SpreadsheetApp.getActiveSheet().getRange("A1");
cell.setNumberFormat("yyyy-mm-dd hh:mm:ss");
```
