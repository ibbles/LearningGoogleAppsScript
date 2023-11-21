A custom formula function is one that can be called from a cell formula.
There is nothing special about such functions, most functions can be called from cell formulas.

Example function named `customFunction`:
```js
function customFunction() {
	return "Hello, World!";
}
```

Cell formula:
```
=customFunction()
```

Cell contents:
```
Hello, World!
```

We can mark a function as being intended for use in formulas.
This makes it show up in the auto-complete list.
The mark is done with a documentation comment.
```js
/**
 * Get a greeting.
 * @customfunction
 */
function customFunction() {
	return "Hello, World!";
}
```

# Passing An Argument, Taking A Parameter

We can pass a parameter to the function.

```js
function multiplyByFive(operand) {
	return operand * 5;
}
```

Cell formula:
```
=multiplyByFive(2)
```
Will evaluate to 10.

We can give a cell ID in the parameter list, to pass the value of that cell to the function.
```
=multiplyByFive(A1)
```
Will read the value of the A1 cell in the same sheet and pass that to the `operand` parameter.

The parameter can be documented.
```js
/**
 * @param operand The value to multiply.
 * @customfunction
 */
function multiplyByFive(operand) {
	return operand * 5;
}
```

If we pass a range of cells to the function then we will get an error: `Result was not a number`.
```
=multiplyByFive(A1:A5)
```
I assume there is some way to process array inputs.


# Passing Multiple Arguments, Taking Multiple Parameters

To take multiple parameters list them as a comma-separated list.
```js
function twoParameter(lhs, rhs) {
	return lhs * rhs;
}
```

# Returning An Array

If we return an array then the values of that array will populate a column of cells,
starting with the cell containing the formula calling the function and extending down.


# Parameters Update Bug

Google Sheets is (as of 2023) quite buggy regarding updating the cell display after changing the argument list of a function call.
If a change doesn't take then:
- copy the formula
- delete everything in the cell
- press Return and then F2 to exit and re-enter edit mode for the cell
- paste the formula back into the cell
- press Return again.

This will force a re-evaluation of the expression.

# References

- [_Google Sheets - Create Custom Functions (UDF) using Apps Script with AutoComplete Tutorial - Part 5_ by Learn Google Sheets & Excel Spreadsheets 2017](https://www.youtube.com/watch?v=SUs74nwFMFY)
