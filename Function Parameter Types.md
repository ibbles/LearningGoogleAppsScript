The Apps Script IDE understands [JSDoc](https://jsdoc.app/) comments.
In the following we can do auto-complete on `name` and get a list of `string` functions.
```js
/**
 * @param {string} name - The name to process
 */
function process(name) {
	name.// Hit CTRL+Spacebar to get a list of string functions.>
}
```
