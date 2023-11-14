Not sure how to do this yet.
There are two conflicting truths:
- An Apps Script [[Function]] called from a [[Formula]] cannot open another spreadsheet.
- An Apps Script [[Function]] called from a [[Creating Menu Items|Menu Item]] cannot output the result as conveniently as a [[Formula]].
So with a formula we can easily control where the output should go, just write the formulate there.
But we can't generate the output because functions called from a formula cannot open other spreadsheets.
So with a menu item we can open the other spreadsheet,
but writing the result to the correct cell is difficult because we have no way to identify which cell the value should go to.
We can hard-code it, but I don't like that much.
We can use indirect look-ups through named ranges defined somewhere else in the sphreadsheet,
but I don't like that much either.

We can read data from other spreadsheets.
To do that we need to know either the URL or the ID of the other spreadsheet.
the ID is the long hex-string in the URL.
For example, the bold part in:  
https://docs.google.com/spreadsheets/d/ **15ifD3Phi5DV-ErK1_kV1-8uUQgD5f565gk8BZ99O-os** /edit#gid=0

```js
const ss = SpreadsheetApp.openByUrl('https://docs.google.com/spreadsheets/d/${ID}$/edit');
var ss = SpreadsheetApp.openById("${ID}");
```
# References

- [_Class Spreadsheet_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet)
- [_Class SpreadsheetApp_ by Google @ developers.google.com](https://developers.google.com/apps-script/reference/spreadsheet/spreadsheet-app)

