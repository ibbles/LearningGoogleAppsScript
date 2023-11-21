While there are functions for writing to a cell or a range of cells,
I have not been able to get it to work.
The error is
```
Exception: You do not have permission to call setValue
```

According to a [reply on the support forums](https://support.google.com/docs/thread/202011707/spreadsheet-no-permission-for-setvalue?hl=en) this is by design:

> You have written `SWAPPOSTCODE()` as a [custom function](https://developers.google.com/apps-script/guides/sheets/functions).
> A custom function cannot modify cells directly, because that would require [authorization](https://developers.google.com/apps-script/guides/sheets/functions#advanced).
> Custom functions can only return values to display in the formula cell.

See also [_Custom Functions in Google Sheets_ > _Advanced_ by Google at developers.google.com 2023](https://developers.google.com/apps-script/guides/sheets/functions#advanced):

> Spreadsheet:
> Read only (can use most `get*()` methods, but not `set*()`).
> Cannot open other spreadsheets (`SpreadsheetApp.openById()` or `SpreadsheetApp.openByUrl()`).
>
> If your custom function throws the error message
>     `You do not have permission to call X service.`
> the service requires user authorization and thus cannot be used in a custom function.

There are some exceptions though.
One is when the writing function is triggered by a user action,
such as selecting an item from a menu, see [[Creating Menu Items]],
or when running the function from within the [[App Script Editor]].

