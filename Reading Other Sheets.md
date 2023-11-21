We are not limited to reading only from the active sheet. [[Accessing Arbitrary Cell Data Range]]
On a [[Spreadsheet]] object we can get the [[Sheet]] object for any sheet we know the name of.
This is done with `Spreadsheets.getSheetByName`.
```js
function namedSheet() {
	const app = SpreadsheetApp;
	const spreadsheets = app.getActiveSpreadsheet();
	const sheet = spreadsheets.getSheetByName("MySheet");
}
```

We can use this sheet as we would the [[Active Sheet]], including `getRange` followed by `getValue` or `setValue`.
