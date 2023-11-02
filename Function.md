A function is a piece of code that can be run from a cell [[Formula]] and from other functions.

```js
function myFunction(input) {
  return "Hello, World!";
}
```

To call a function from a cell [[Formula]] simply supply the name followed by parenthesis:
```
=myFunction()
```

The return value of the function will be displayed instead of the [[Formula]].

Functions are (mostly) only executed once unless the inputs change.
The above function does not have any inputs, so it will not be rerun.
This is true even if the function reads other data that may change,
such as from other cells in the spreadsheet.
To solve this problem, make sure to always pass in one or more ranges that cover all the cells the function may read.
See [[Rerun Function When Input Cells Contents Change]].

# References

- [_Custom Functions in Google Sheets_ by Google @ developers.google.com](https://developers.google.com/apps-script/guides/sheets/functions)
