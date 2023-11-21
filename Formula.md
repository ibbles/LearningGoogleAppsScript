A formula is an expression in a cell.
A formula always starts with `=`.
An example formula:
```
=B1+2
```
The above formula reads the value in the `B1` cell, adds two, and then display the result in the cell holding the formula.

We can write a formula from App Script with the `Range.setFormula` function.
```js
/** @customfunction */
function myFunction() {
	const cell = SpreadsheetApp.getActiveSheet().getRange(1, 1);
	cell.setFormula("=B1+2");
}
```

