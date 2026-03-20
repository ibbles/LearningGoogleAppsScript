Clasp is a tool for working on Google Apps Script project locally ([1](https://developers.google.com/apps-script/guides/clasp)).
With Clasp you can download the Apps Script source file, edit them in your favorite editor, and then push the new version back up.
Combining this with Git and you also get merge conflict handling and revision tracking.


# Installation

```shell
npm install @google/clasp -g
```


Enable Google Apps SCript API: https://script.google.com/home/usersettings
Required to modify the Apps Script files, but not to clone / pull them.


# Commands

```shell
clasp --version
clasp login
clasp clone PROJECT_ID
clasp push
clasp pull
```


# References

- 1: [_feedbackUse the command-line interface with clasp_ @ developers.google.com](https://developers.google.com/apps-script/guides/clasp)

