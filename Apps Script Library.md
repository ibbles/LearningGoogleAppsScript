An Apps Scrips Library is a collection of functions that can be used from multiple Sheets documents.
Is created similarly to any other document in Google Drive:
Google Drive folder > right-click > More > Apps Script.

To use the functions in an Apps Script Library in a [[Spreadsheet]] the library must be deployed and that spreadsheet must import the library.

# Using A Library

To use an Apps Script library in a [[Spreadsheet]] document you need to know the library's Script ID.
You can find this in [[App Script Editor]] > left panel > Project Settings > IDs > Script.

In the [[Spreadsheet]] that should use the library:
- Open the sheet-specific Apps Script Editor with Top Menu Bar > Extensions > Apps Script.
- From the left mode selector select the Editor mode.
- From the left panel click the `+` button next to Libraries.
- Paste the Script ID into the Script ID box.
- Click Look Up.
- Select the deployed version to use.
	- Either a fixed version or HEAD.
- Make sure Identifier is the name of the Apps Script library you intended.
	- This name is also how we access the library's function in the document's scripts.
- Click Add.

The imported library is now listed under Libraries.

As an example, if your library is named `Test`, as shown in the Identifier field when the library was added to the document, and the library contains a function named `test`, then we can call that library found from the document's Apps Script with
```js
Test.test();
```


# Deploy Library

A deployment is a fixed version of the library.
Except for the head deployment, which is changed with the code changes.

To deploy the library click the Deploy button in the top-right corner of the [[App Script Editor]].
Click Manage Deployments.
Click Create Deployment.
From the left side for Select Type select Library.
Give it a description.
Click Deploy.
This will give you a Deployment ID and a Library URL.

# References

- [_Create and manage deployments_ by Google](https://developers.google.com/apps-script/concepts/deployments)
- 