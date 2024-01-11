A named range is a [[Range]] of cells in a [[Sheet]] that  has been given a name.
The [[Range]] can be accessed in Apps Script code using that name.
A named range is created by:
- Select the cells to be named.
- Top Menu Bar > Data > Named Ranges > Add A Range.
- Write the name.

My own convention is to use `snake_case` names for named ranges,
to separate them from `camelCase` regular JavaScript variables.

In Apps Script we read the value of the [[Range]] using a combination of `getRangeByName` and `getValue` or `getValues`.
If the [[Range]] covers a single cell then use `getValue`.
If the [[Range]] covers multiple cells then use `getValues` to get a 2D JavaScript array.

```js
function useNamedRange() {
	const range = SpreadsheetApp.getActive().getRangeByName("my_named_range");
	const value = range.getValue();
	const values = range.getValues();
}
```

Get a list of all named ranges with `Spreadsheet.getNamedRanges`:
```js
// The code below logs the name of the first named range.
var namedRanges = SpreadsheetApp.getActiveSpreadsheet().getNamedRanges();
for (var i = 0; i < namedRanges.length; i++) {
	Logger.log(namedRanges[i].getName());
}
```
