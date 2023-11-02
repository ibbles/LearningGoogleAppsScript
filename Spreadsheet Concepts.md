There is a hierarchy of data, each level containing multiple levels of the things below if.
- Sheets application. [[SpreadsheetApp|`SpreadsheetApp`]] in the API.
	- Spreadsheets. The documents.
		- Sheets. The tabs.
			- Cells. Organized in rows and columns.

Cells are identified using (column, row) coordinates.
Columns are lettered, rows are numbered.
The top-left cells is A1.
The neighbor to the right is B1.
The neighbor down is A2.
Cells are accessed as ranges.
A range is a continuous rectangular collection of cells.
Possibly a single one.
Identified as a start (upper-left) cell and an end (lower-right) cell.
A1:B2 is the 2x2 range consisting of A1, B1, A2, B2.
A1 is the range containing the single cell A1.

Unfortunately, when accessing cells with integer-only coordinates, 
i.e. (5, 3),
then the order is flipped,
i.e. (5, 3) is row 5, column 3,
while E3, E is the letter equivalent of 5, is column E row 3.

This structure is used when we access data from an [[Apps Script]].
For an example, see [[Accessing Arbitrary Cell Data]]

# References

- [_App Script Editor Tutorial - Google Sheets - Excel VBA Equivalent - Read & Write to Ranges & Cells_, _Spreadsheet Concepts_ by Learn Google Sheets & Excel Spreadsheets @ youtube.com 2017](https://youtu.be/aPJ-2U45BpA?list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw&t=241)
