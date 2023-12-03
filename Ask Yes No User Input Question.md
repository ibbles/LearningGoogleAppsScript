
Basic structure.
```js
var ui = SpreadsheetApp.getUi();
var response = ui.alert(
    'Question goes here.',
    ui.ButtonSet.YES_NO
);

if (response == ui.Button.YES) {
    // The user clicked yes.
}
```


Helper function.
```js
function askContinue(message) {
  const ui = SpreadsheetApp.getUi();
  const response = ui.alert(`${message} Continue?`, ui.ButtonSet.OK_CANCEL);
  return response == ui.Button.OK;
}

function doWork() {
	if (!askContinue("Show work be done?"))
		continue;

	// Do the work.
}
```


# References

- [_Yes/no user prompt to continue or stop the script_ by CristianCapsuna @ stackoverflow.com](https://stackoverflow.com/questions/45879224/yes-no-user-prompt-to-continue-or-stop-the-script)
