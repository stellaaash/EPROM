---
tags:
  - book
Status: IN PROGRESS
Website: https://exploringjs.com/js/book/index.html
Author: Axel Rauschmayer
---
Learning JavaScript for programmers!
# Progress
16 - non-values
# Notes
## 8 - Using Javascript: the big picture
This book teaches the JavaScript language, and just the language. It's not particularly eager about teaching web dev or such things as [[Node.js]].
There are two distinct JavaScript platforms: web browsers, and Node.js.
They are both structured in two layers:
- The foundational layer consists of the JavaScript engine and platform-specific core functionality.
- There's two APIs on top of this foundation:
	- The JavaScript standard library that is part of the language and runs on top of the engine.
	- The platform API that is also inside of JavaScript, and provides platform specific functionality.
	  This can mean the browser' UI, reacting to mouse clicks, playing audio, etc...
	  And in Node, this can mean reading and writing files, downloading data via HTTP, etc...
### JS references
There's a few valuable references to keep in mind:
- [MDN Web Docs](https://developer.mozilla.org/en-US/) for all web technologies, [[HTML]], [[CSS]], JavaScript and more.
- [Node.js Docs](https://nodejs.org/docs/latest/api/) for the Node.js API.
- [ExploringJS.com](https://exploringjs.com/): Other books from the author talking about aspects of web development.
## [9 - Syntax](https://exploringjs.com/js/book/ch_syntax.html)
A good cheatsheet of JavaScript's basic syntax.
### Naming conventions
In JavaScript, use camel case, except for constants.
Lowercase:
- Functions, variables: `myFunction`
- Methods: `obj.myMethod`
- CSS:
    - CSS names: `my-utility-class` (dash case)
    - Corresponding JavaScript names: `myUtilityClass`
- Module file names are usually dash-cased:
    ```js
    import * as theSpecialLibrary from './the-special-library.mjs';
    ```
Uppercase:
- Classes: `MyClass`
All-caps:
- Constants (as shared between modules etc.): `MY_CONSTANT` (underscore case)
___
If the name of a parameter stars with an underscore, it means it is not used:
```js
arr.map((_x, i) => i)
```
If the name of a property of an object starts with an underscore that property is considered private:
```js
class ValueWrapper {
	constructor(value) {
		this._value = value;
	}
}
```
## 10 - JavaScript consoles
In order to easily run JavaScript code, you have multiple options:
- The console in your browser, accessible through its devtools.
- The [[REPL]]: after instaling [[Node.js]], you can use it through the CLI utility `node`.
- Other options, such as web apps, other native apps and IDE plugins.
Careful though, most consoles run in non-strict mode.
### 10.2 - The `console.*` API
`console.*` methods allow you to interact with both the browser console and the Node.js one.
Most functionality is supported by both.
You can use `console.log()` to output to stdout and `console.error()` to output to stderr.
Both always output a newline after their arguments, which can be numerous and consist of different types.
You can also give it a single string containing `%` directives for substitutions, like for `printf` in C.
## 11 - Assertions
JavaScript has a **built-in** module for assertions, giving the `assert` keyword
that throws an exception when something isn't true.
There are multiple methods attached to that module.
```js
import assert from 'node:assert/strict';
assert.equal(3 + 5, 8);
```
There are multiple versions of assert, but you'd better use the strict version as shown in the above example.
### 11.3 - Normal vs deep comparison
JavaScript has two comparison operators, `==` and `===`.
The strict `assert.equal()` uses `===` to compare values. Therefore, an object is only equal to itself (think of it as pointers to the objects, if two objects exist, they can't have the same address, and are thus different).
`assert.deepEqual()` is a better choice for comparing objects.
```js
assert.deepEqual({foo: 1}, {foo: 1});
```
That works for comparing arrays, too.
### 11.4 - Quick reference for `assert`
#### Normal equality
- `assert.equal(actual, expected, message?)`: `actual === expected` must be `true`. If not, an `AssertionError` is thrown.
- `assert.notEqual(actual, expected, message?)`: `actual !== expected` must be `true`. If not, an `AssertionError` is thrown.
You can give message as the optional third argument to be added to the `AssertionError` and also to explain what is being checked.
#### Deep equality
- `assert.deepEqual(actual, expected, message?)`: `actual` must be deeply equal to `expected`. If not, an `AssertionError` is thrown.
- `assert.notDeepEqual(actual, expected, message?)` `actual` must not be deeply equal to `expected`. If it is, an `AssertionError` is thrown.
#### Expecting exceptions
With `assert.throws(callback, message?)`, you can check if a function `callback` throws an exception.
You can give it additional parameters to specify what error you're expecting:
- `assert.throws(callback, message?): void`: no argument just checks for any exception.
- `assert.throws(callback, errorClass, message?): void`: Pass in the exception type to check for that specific one.
- `assert.throws(callback, errorRegExp, message?): void`: Pass in a [[Regular Expression]] to search for in the exception message.
- `assert.throws(callback, errorObject, message?): void`: Pass in a full object to check against the exception.
#### Always fail
With `assert.fail(messageOrError?)`, you can always through an `AssertionError` when it is called.
Sometimes useful for unit testing.
`messageOrError` can be:
- A string to override the error message.
- An instance of `Error` or a subclass of `Error` to throw a different value than `AssertionError.
## 12 - Getting started with exercises
To get all the exercises, you'll have to buy the book.
Tests are run using the Mocha framework. They're basically just asserts though, you can probably create your own.
The structure is the main code in a js module, and the tests for that module into a separate file.
## 13 - Variables and assignment
You have two main ways of declaring variables:
- `let` gives you a mutable variable.
- `const` gives you a constant, or immutable variable.
Technically, `var` also exists, but it's a bit weird. **Don't use `var`.**
### 13.2 - Const
In JavaScript, the `const` keyword only means that the **binding** is immutable.
That means only the link between the name of the variable and its value is immutable.
**It does not mean the value itself is immutable.**
For example, declaring a new object as `const` still allows you to mutate internal values of that object.
### 13.3 - When to use let or const
In general, as with other languages, **use const when you don't have to change the binding of a variable**.
### 13.5 - Scope
Scope and shadowing variables works essentially the same as C and other languages, mostly what you'd expect in theory.
### 13.8 - Scope vs activation
In javascript, scope is one thing, and activation is another thing.
Scope is a static trait (determined by the code structure), and tells where you can see an entity.
Activation, on the other hand, is a dynamic trait (determined at runtime). It tells when you can **access** an entity.
Some entities can be access as soon as we enter their scopes, but others you have to wait for execution to reach their declarations before you can access them.
## 14 - Values
JavaScript has two general types of values: **primitive values and objects**. Most if not all objects are instances of the type `Object`.
### 14.3 - Types of the spec
- `undefined` with the only element `undefined`
- `null` with the only element `null`
- `boolean` with the elements `false` and `true`
- `number`, the type of all numbers (e.g., `-123`, `3.141`)
- `bigint`, the type of all big integers (e.g., `-123n`)
- `string`, the type of all strings (e.g., `'abc'`)
- `symbol`, the type of all symbols (e.g., `Symbol('My Symbol')`)
- `object`, the type of all objects (different from `Object`, the type of all instances of class `Object` and its subclasses)
### 14.4 - Primitives vs objects
Primitive values are the elements of the types `undefined`, `null`, `boolean`, `number`, `bigint`, `string`, `symbol`.
All other values are objects.
Primitives are **passed by value and compared by value**, which means their exact contents are compared.
Objects, on the other hand, are **passed by identity and compared by identity** instead. Identities are a bit like pointers.
Both primitives and objects have key-value entries as **properties**, like the `length` for strings.
### 14.5 - Primitive values
You can't touch primitives' properties. Either change, add or remove them will all result in a `TypeError`.
Primitives are all passed by value.
Primitives are all compared by value, comparing their contents.
### 14.6 - Objects
You can create objects with both object literals and array literals.
**Object literal**
```js
const range = {
	min: 0,
	max: 10,
};
```
**Array literal**
```js
const vegetables = ['salad', 'avocado'];
```
___
Objects are **mutable by default**, meaning we can **freely change, add or remove properties of an object**.
They are **passed by identity**. Variables store these identities, which are transparent references (like pointers) to the object's actual data on the **heap**.
When you pass an object to a function or assign it to a variable, you copy its identity, not its contents.
JavaScript is a **garbage collected language**, managing heap-allocated memory like objects automatically.
Objects are also **compared by identity**.
This is why comparing two distinct objects without deep equality always results in a false statement, because their identities (or pointers) can't be the same, even if their contents are.
```js
const obj = {};
assert.equal(obj === obj, true) // same identity
assert.equal({} === {}, false); // same contents, but different identities
```
### 14.7 - typeof and instanceof
You can use `typeof <variable>` to get the type of a **primitive** value, and `<variable> instanceof <type>` to get a boolean telling you if an **object** is of a given type.
#### 14.7.1 - `typeof`
There are two quirks about typeof:
- `typeof null` returns `object`: That's a bug, and it can't be fixed. They tried, and it broke too much code on the web.
- `typeof <function>` should be `object`, but it is `function` instead. Which is confusing, because **functions are objects**.
#### 14.7.2 - `instanceof`
The `x instanceof C` operator answers the question "has a value `x` been created by a class `C`?"
### 14.8 - Classes and constructors
Objects are created using **constructors functions**, functions that return instances of themselves when invoked with the `new` operator.
This makes constructor functions **essentially classes**, which were introduced in ES6. They're the preferred syntax to use for using classes.
Classes are **really just constructor functions**. These function define the class' properties and how they are structured.
The return value of a constructor function is the actual class instance.
#### 14.8.1 - Constructors and primitives
Each primitive type has its own associated constructor function (also named class as seen above).
For example, booleans have `Boolean`, and strings have `String`.
You can also use these functions to convert values to other types, like a string to a number:
```js
assert.equal(Number('123'), 123);
```
Using `Type.prototype`  on a constructor function gives you access to its properties and methods, like the `toString()` method:
```js
assert.equal((123).toString, Number.prototype.toString);
```
Each class is also a namespace or container object for util functions related to that class.
For example, the `Number` class contains a `isInteger()` method.
And of course, you can easily use primitive classes to create objects of that class.
However, these aren't real number (since they're objects), and thus should be avoided.
### 14.9 - Converting between types
In JavaScript, there are two ways to convert values to other types:
- Explicit conversion with constructors/classes, like `String()`.
- Coercion, which happens whenever you do implicit conversions like giving a number to a function that expects a string.
## 15 - Operators
### 15.1 - Making sense of operators
In today's episode of "JavaScript is weird", we have operators.
Most operators only work with primitive values.
Two rules are important to remember to be less weirded out by the language:
- Operators **coerce their operands to appropriate types**.
- Most operators **only work with primitives**.
#### 15.1.1 - Operator coercion
JavaScript often fails silently when an operator gets operands that don't match the proper types.
Indeed, it chooses to **coerce the values** to automatically convert them instead of throwing an exception.
```node
> '7' * '3'
21
```
Same thing for the square brackets operator to access properties of an object: it only accepts strings and symbols.
Everything else is **coerced to a string**.
#### 15.1.2 - Operators and primitives
Most operators only work with primitives.
That means that, to function with objects, they'll start by **coercing them into primitives** first.
```node
> [1,2,3] + [4,5,6]
'1,2,34,5,6'
```
This happens because both arrays are first converted to strings, and THEN concatenated.
### 15.3 - The plus operator
The addition operator works like this in JavaScript:
- First, it converts both operands to primitives. By default, it prefers converting to numbers. Then, there's two options:
	- If one of the two primitives is a string, it also makes the other a string and concatenates them for the result.
	- Otherwise, both operands are made numbers and mathematically added to each other, and returned.
String mode allows us to easily concatenate strings with the `+` operator.
```node
> 'There are ' + 3 + ' items'
'There are 3 items'
```
Number mode means that if neither of the operands are strings (or can be coerced to strings), then everything is coerced to numbers instead.
Booleans for example get coerced to 0 or 1.
### 15.5 - Equality
In JavaScript, there are two equality operators:
- `==` loose quality
- `===` strict equality
In general, **you should always use strict equality**. There's hardly ever cases where you'd want to "loosely compare" values.
**Two values are only strictly equal if they have the same type.**
Strict equality never coerces, loose quality does.
It's sometimes (rarely) useful to use loose equality, for example when you'd want to compare a string to a number without explicitly converting values.
Rejoice, ordering operators like `<=` and `>=` are based on strict equality.
## 16 - `undefined` and `null`
The difference between `undefined` and `null` (both represent non-values) lies in their actual meaning:
- `undefined` means "not initialized" (for variables) or "not existing" (for properties of objects)
- `null` means "the **intentional** absence of any object value"
Both `undefined` and `null` are falsy values, so you can easily check for them in `if` statements.
The `<value> ?? <default>` operator allows you to check if `value` is `undefined` or `null`, and if so, returns the `default` value you set instead as the expression.
Of course, the right side is only evaluated if it's going to be used, like conditional stuff.

