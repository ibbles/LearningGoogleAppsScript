When editing a sheet manually we can repeat a formula by selecting the cell and dragging the corner handle.
This will update cell references, incrementing the row number for every row we drag vertically and incrementing the column letter for every column we drag horizontally.
We can do the same from an App Script.
```js
/** @customfunction */
function myFunction() {
	sourceCell = SpreadsheetApp.getActiveSheet().getRange("A1");
	fillRange = SpreadsheetApp.getActiveSheet().getRange("A2:A10");
	sourceCell.copyTo(fillRange);
}
```

# References

- [_Google Sheets - Apps Script Fill Down Formula (Set a Fromula & Copy Down AutoFill) Tutorial - Part 9_ by Learn Google Sheets & Excel Spreadsheets 2017](https://www.youtube.com/watch?v=cCBtsQGtzoQ&list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw&index=9)
- 