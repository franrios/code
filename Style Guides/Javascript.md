# JavaScript

A minimalist's guide to modern JavaScript.



## Table of Contents

- [Golden rule](#golden-rule)
- [Structure](#structure)
  - [Spaces or tabs](#spaces-or-tabs)
  - [Line length](#line-length)
  - [Whitespace](#whitespace)
  - [Alignment](#alignment)
- [Semicolons](#semicolons)
- [Comments](#comments)
  - [Inline](#inline)
  - [Block](#block)
- [Naming conventions](#naming conventions)
- [Variables](#variables)
- [Functions](#functions)
- [Objects](#objects)
- [Arrays](#arrays)
- [Modules](#modules)
- [Conditionals](#conditionals)
- [Loops](#loops)
- [Annotations](#annotations)



## Golden rule

The codebase should read as one voice - regardless of how many authored it.



## Structure

#### Spaces or tabs

Use **spaces** and indent **2 spaces** per indentation level.


#### Line length

Keep code lines < 80 characters per line. If you're going over, that means it's time to refactor.


#### Whitespace

Maintain at least 2 line breaks between your top-level functions and at least 1 line break between bodies of functions where it helps readability:

###### Bad

```javascript
function someEpicMethod() {
  var values = getSomeAmazingThings()
  // Manipulate the values
  values = values.map(doSomeOtherAmazingThing)
  values = values.map(doOneMoreOtherAmazingThing)
  return values
}
function getSomeAmazingThings() {
  // ...
}

/**
  This does some amazing things
 */
function doSomeOtherAmazingThing() {
  // ...
}
```

###### Good

```javascript
function someEpicMethod() {

  var values = getSomeAmazingThings()

  // Manipulate the values
  values = values.map(doSomeOtherAmazingThing)
  values = values.map(doOneMoreOtherAmazingThing)

  return values

}


function getSomeAmazingThings() {
  // ...
}


/**
 * This does some amazing things
 */
function doSomeOtherAmazingThing() {
  // ...
}
```

#### Alignment

Align groups of variable assignments:

###### Bad

```javascript
var debug = require('debug')('javascript')
var lodash = require('lodash')
var oriento = require('oriento')

var one = 1
var fifteen = 15
var onePlusFifteen = one + fifteen
```

###### Good

```javascript
var debug   = require('debug')('javascript')
var lodash  = require('lodash')
var oriento = require('oriento')

var one            = 1
var fifteen        = 15
var onePlusFifteen = one + fifteen
```


## Semicolons

Don't use them. JavaScript has reliable ASI (automatic-semicolon-insertion) which allows for cleaner looking code.

In the few rare scenarios where a semicolon is required, JSHint will catch it. The issue should then be resolved by a small refactor or by adding a semicolon to the **front** of the line that requires it.

Example by inserting semicolon:

```javascript
function myFunc() {
  var collection = []
  ;[].map.call(arguments, function() {
    // ...
  })
}
```

Or better yet, a small refactor:

```javascript
function myFunc() {
  var collection = []
  mapArgs(arguments, function() {
    // ...
  })
}
function mapArgs(args, fn) {
  return [].map.call(args, fn)
}
```


## Comments

Comments are necessary to describe to humans what code a snippet of code is doing - however, they must be as concise as possible to make them easier to maintain as the snippet evolves.

#### Inline

Inline comments should always appear *before* the line they are describing:

###### Bad

```javascript
x = x + 1 // Compensate for border
```

###### Good

```javascript
// Compensate for border
x = x + 1
```


#### Block

Use [DocBlockr](https://github.com/Warin/Sublime/tree/master/DocBlockr).

Here is a complete mock comment to exemplify all of the possible inclusions:

```javascript
/**
 * @deprecated because yolo
 * This is my description
 *
 * TODO: make all your comments this awesome
 * FIXME: just kidding, my code is gold
 *
 * @example
 *   callThisFunctionWithArgs("myString", 123, {
 *     prop1: '1',
 *     prop2: '2'
 *   })
 *   // 12345
 * @example
 *   callThisFunctionWithArgs("oneLiner", 1) // 12345
 * @example
 *   callThisFunctionWithArgs("tooLongForOneLine", 12345, {
 *     too:   'many',
 *     props: 2,
 *     count: true
 *   }
 *   =>
 *   {
 *     it:       "won't",
 *     actually: 'return',
 *     "this":   'because',
 *     i:        'said',
 *     so:       '.'
 *   }
 *
 * @param {String} arg1 the first argument
 * @param {Number} arg2 the second argument
 * @param {Object} obj  the object @optional
 *
 * @return {Number} always returns 12345 because yolo
 *
 * @private
 * @admin
 */
```


## Naming conventions

Be descriptive with your naming choice. Avoid unnecessary abbreviations because they might not be as obvious to someone else:

```javascript
// Bad
var btn  = document.getElementById('button')
var stmt = ''
var age  = user.age()

// Good
var button    = document.getElementById('button')
var statement = ''
var age       = user.getAge()
```

If a method returns something, it should be prefixed with `get`, `is`, etc. If a method sets something, it should be prefixed with `set`, `update`, `insert`, etc.

###### Letter casings

These are the casings we use for naming things:

```
UPPER_SNAKE_CASE : used for constants
PascalCase       : used for classes
camelCase        : used for everything else
```

For example:

```javascript
var MY_CONSTANT   = 500
var myVariable    = true
var myConstructor = new MyConstructor()
var myClass       = new MyClass()
var myObject      = Object.create(MyObject)
var myFunction    = function(myArg) {}
```

###### Private members

Typically, you can achieve private members through function or module scoping. However, if your class or module exposes these private members, prefix them with an underscore (`_`).

For example:

```javascript
var MyObj = function(name) {
  this._name = name

  this.setName = function(name) {
    this._name = name
  }
  this.getName = function() {
    return this._name
  }

  return this
}
```


## Variables

Use multiple `var` declarations instead of comma separating them:

```javascript
// Bad
var someVar      = true,
    someOtherVar = false

// Good
var someVar      = true
var someOtherVar = false
```


## Functions

Know the basic terminology:

```javascript
// Anonymous function expression
var anonymous = function() {}

// Named function expression
var named = function named() {}

// Function declaration
function declaration() {}
```

Only use function declarations for the sake of consistency and added benefits they come with.

```javascript
// Bad
module.exports = {
  myMethod: function() {}
}

// Good
module.exports = {
  myMethod: myMethod
}
function myMethod() {}
```

###### Private methods

All private methods should be defined *after* the `return` statement so that the main function body is easier to digest:

```javascript
// Bad
function calculate(options) {

  var start = options.starting.map(calcStart)
  var end = options.ending.map(calcEnd)

  function calcStart(starting) {
    /* do some magic */
  }

  function calcEnd(ending) {
    /* do some magic */
  }

  return start.join('') + end.join('')
}

// Good
function calculate(options) {

  var start = options.starting.map(calcStart)
  var end = options.ending.map(calcEnd)

  return start.join('') + end.join('')

  function calcStart(starting) {
    /* do some magic */
  }

  function calcEnd(ending) {
    /* do some magic */
  }
}
```


###### Whitespace

Whitespace around a function should look like this:

```javascript
function getSomeValue(object, propertyName) {
  // ..
}
var value = getSomeValue(someObject, 'property')
```

Whitespace around a generator should look like this:

```javascript
// Anonymous
app.use(function* () {})

// Named
function* myGenerator() {}
```


## Objects

Use the literals:

```javascript
// Bad
var myObject = new Object()

// Good
var myObject = {}
```

###### Trailing commas

Trailing commas are fine:

```javascript
var object = {
  prop1: true,
  prop2: false,
}
```

###### Whitespace

Whitespace around an object should look like this:

```javascript
var object = {
  prop: true,
  method: function() {}
}
```


## Arrays

Use the literals:

```javascript
// Bad
var myArray = new Array()

// Good
var myArray = []
```

Don't mess directly with the array's indices **unless** if you're mutating it with a targeted index. Use `[].push` instead.

###### Trailing commas

Trailing commas are fine:

```javascript
var array = [
  'value1',
  'value2',
]
```

###### Whitespace

Whitespace around an array should look like this:

```javascript
var shortArray = ['some', 'value', 'here']
var longArray = [
  'some',
  'values',
  'seem',
  'to',
  'go',
  'on',
  'for-',
  'wait',
  'for',
  'it',
  '-ever'
]
```


## Modules

A module's imports and exports should appear at the very top of the file:

```javascript
import 'globals'
import {sync as glob} from 'glob'

export {getFiles, setContent}
export const DEFAULT_TIMEOUT = 500

// ...rest of the file
```


## Conditionals

Be explicit with your conditional checks by always using `===`, unless:

```javascript
// Checking if a value is either `null` or `undefined`
if (value == null) {}
```

Be concise with your logical checks:

```javascript
// Bad
if (something === true) {}
if (array.length === 0) {}

// Good
if (something) {}
if (!array.length) {}
```

Or better yet, cache the condition:

```javascript
// Best
var isSomething = !!something
var isEmptyArray = !array.length
if (isSomething) {}
if (isEmptyArray) {}
```

For complicated conditions, **definitely** cache the condition or even break it down into sub-conditions.

###### Whitespace

Whitespace around a conditional should look like this:

```javascript
if (isCondition) {
  // ...
}
else if (something === true) {
  // ...
}
else {
  // ...
}
```

If the function is returning between each conditional branch, remove the `else`s:

```javascript
if (isCondition) {
  return // ...
}
if (something === true) {
  return // ...
}
return // ...
```


## Loops

Avoid loops whenever possible. They aren't as flexible as native array methods, such as `forEach`, `map`, `filter`, etc.

When using these array methods, extract the looped function:

```javascript
// Bad
array.map(function() {})

// Good
array.map(manipulateItem)
function manipulateItem() {}
```

If you must use loops, **never** create functions within them. It's bad for performance.

###### Whitespace

Whitespace around a loop should look like this:

```javascript
for (let i = 0; i < 10; i++) {
  // ...
}
while (value === true) {
  // ...
}
do {
  // ...
} while (value === true)
```



## Annotations

Use annotations whenever necessary to describe any action needed for a snippet of code. Use any of the following as suited:

- `TODO`     : for missing functionality that should be added at a later date
- `FIXME`    : for broken code that must be fixed
- `OPTIMIZE` : for code that is inefficient and may become a bottleneck
- `HACK`     : for the use of a questionable (or ingenious) coding practice
- `REVIEW`   : for code that should be reviewed to confirm implementation











<br><br><br><br><br><br>