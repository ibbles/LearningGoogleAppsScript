If we have a bunch of values in an array then we can write those values to a range of cells.
Though beware of [[Permission Restrictions]].
The array must be two-dimensional and the size must match that of the range.


```js
/** @customfunction */
function myFunction() {
	const array = [[11,12], [21, 22], [31, 32]]; // Three rows, each with two column.
	const range = SpreadsheetApp.getActiveSheet().getRange("E3:F5"); // Three rows (3, 4, 5), each with two columns (E, F).
	range.setValues(array);
}
```

See also [[Reading Multiple Cells Into An Array]].