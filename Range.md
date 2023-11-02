A range is a way to identify a cell or a contiguous range of cells.
They are specified either using A1 notation or integer indices.

A1 notation uses letters to identify columns and number to identify rows.
The A1 cell is in the top-left.
The B1 cell is one cell to the right of A1.
The A2 cell is cone cell below A1.
We can designate a rectangular contiguous range of cells by giving two cells separated by :.
This will designate a range including all cells on the rows on or between the rows of the two given cells
and columns on or between the columns of the two given cells.
For example, A1:C10 starts at A1 and ends at, including, C10.

Integer indexing is one-based, meaning the top-left cell is (1, 1).
The order is (row, column), meaning that cell (1, 2) is to the right of (1, 1).
Cell (2, 1) is below (1, 1).
Multi-cell ranges are specified by giving the number of rows and number of columns to extend down and right from the (row, column) cell.
For example, (2, 3, 10, 20) designate a range starting at row 2, column 3,  extending 10 rows down and 20 column to the right.
The number of rows and columns count the number of rows and column, not steps.
So (2, 3, 1, 1) selects the single cell at (2, 3), since it selects one row and one column.
So (2, 3, 2, 2) selects a 2x2 block of cells with the top-left corner at (2, 3).

# References

- [_App Script Editor Tutorial - Google Sheets - Excel VBA Equivalent - Read & Write to Ranges & Cells_ by Learn Google Sheets & Excel Spreadsheets @ youtube.com 2017](https://www.youtube.com/watch?v=aPJ-2U45BpA&list=PLv9Pf9aNgemv62NNC5bXLR0CzeaIj5bcw)
