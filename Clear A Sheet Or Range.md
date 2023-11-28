By clear I mean removing all the contents.

```js
function cleanSheet() {
	const sheet = SpreadsheetApp.getActiveSheet();
	const firstRow = 2; // Skip past headings.
	const firstColumn = 1;
	const lastRow = sheet.getLastRow();
	const lastColumn = sheet.getLastColumn();
	const range = sheet.getRange(firstRow, firstColumn, lastRow - firstRow + 1, lastColumn - firstColumn + 1);
	range.clear();
}
```