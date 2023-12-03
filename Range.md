A range is a way to identify a cell or a contiguous range of cells.
They are specified either using A1 notation or integer indices.

# A1 Notation

## Single Cell

A1 notation uses letters to identify columns and number to identify rows.
The A1 cell is in the top-left.
The B1 cell is one cell to the right of A1.
The A2 cell is cone cell below A1.

## Rectangular Regions

We can designate a rectangular contiguous range of cells by giving two cells separated by :.
This will designate a range including all cells on the rows on or between the rows of the two given cells
and columns on or between the columns of the two given cells.
For example, A1:C10 starts at A1 and ends at, including, C10.

# Integer Notation

## Single Cell

Integer indexing is one-based, meaning the top-left cell is (1, 1).
The order is (row, column), meaning that cell (1, 2) is to the right of (1, 1).
Cell (2, 1) is below (1, 1).
This is the opposite of A1 notation, which has the column first.
A10 = (10, 1).

## Rectangular Regions

Multi-cell ranges are specified by giving the number of rows and number of columns to extend down and right from the (row, column) cell.
For example, (2, 3, 10, 20) designate a range starting at row 2, column 3,  extending 10 rows down and 20 column to the right.
The number of rows and columns count the number of rows and column, not steps.
So (2, 3, 1, 1) selects the single cell at (2, 3), since it selects one row and one column.
So (2, 3, 2, 2) selects a 2x2 block of cells with the top-left corner at (2, 3).

# `getValues` And JavaScript Arrays

Calling `getValues` on a range returns a 2D JavaScript array.
JavaScript arrays use 0-based indexing, meaning the first element is at index 0.
Since Apps Script uses 1-based indexing for sheet rows and columns we may need to do `row - 1` and `column - 1` when indexing into the JavaScript arrays.
The 2D array is row-major, meaning that each element of the outer array is row.
`getValues[0]` gives you the first row, which is also an array.
`getValues[0][0]` gives you the first row, and the first element of that row, i.e. the top-left corner of the range.
`getValues[0][i]` where `i` is a counter walks along the first row, i.e. between columns.
`getValues[row][col]` gives you the element on row `row` and column `column`.

`getValues` returns a 2D array even if the range is 1D.
In that case one of the dimensions has size 1.
If the range is a column then the outer array has size `n` and the inner arrays has size `1`.
```js
// Looping over a column.
const range = spreadsheet.getRange("A2:A");
const values = range.getValues();
for (row of values) {  // Loop over the rows.
	const value = row[0];  // Read the only column on that row.
	Logger.log(value);
}
```
If the range is a row then the outer array has size `1` and the inner array has size `n`.
```js
# Looping over an array.
const range = spreadsheet.getRange("B1:1");
const values = range.getValues();
for (value of values[0]) {  // Loop over all values in the first, and only, row.
	Logger.log(value);
}
```
# References

- [_App Script Editor Tutorial - Google Sheets - Excel VBA Equivalent - Read & Write to Ranges & Cells_ by Learn Google Sheets & Excel Spreadsheets @ youtube.com 2017](https://www.youtube.com/watch?v=aPJ-2U45BpA&list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw)
