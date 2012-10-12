# Node.js Style Guide

This is a guide for writing JavaScript code in any environment.
It is inspired by pragmatic thought leaders in the community
and decisions from working with JavaScript in Node and in the browser day-in-day-out.

This guide was forked from [Felix Geisendörfer](http://felixge.de/)'s guide and is
licensed under the [CC BY-SA 3.0](http://creativecommons.org/licenses/by-sa/3.0/)
license. The original guide is located [here](https://github.com/felixge/node-style-guide).
You are encouraged to fork this repository and make adjustments according to your preferences.

There is a jshint options json file in this repo to help you conform to
some of the guidelines outlined here.

![Creative Commons License](http://i.creativecommons.org/l/by-sa/3.0/88x31.png)

## 2 Spaces for indention

Use 2 spaces for indenting your code and swear an oath to never mix tabs and
spaces in your code - a special kind of hell is awaiting you otherwise.

## Spacing

Follow Crockford’s rules about spaces and **be consistent**:

- No space between and named function and its brackets: `function foo() {}`
- Exactly one space between an annonymous function and its brackets: `function () {}`
- Exactly one space after a comma: `console.log(a, b, c)`
- Exactly one space each side of infix operators: `5 + 5 / 3`, `10 * Math.min(a, b)`
- No space between a prefix/postfix operator and its operand: `-8 / 2`, `i++`
- No space after a property name and exactly one space after it in an object literal: `foo: bar`

## No trailing whitespace

Just like you brush your teeth after every meal, you clean up any trailing
whitespace in your JS files before committing. Otherwise the rotten smell of
careless neglect will eventually drive away contributors and/or co-workers.

## No Semicolons

Semicolons should be omitted for brevity and reduced visual noise.

Semicolons are unnecessary and all JavaScript implementations follow the same
automatic semicolon injection rules to-the-T (yes, including IE6). Removing
them makes the code easier to write and easier to read.

There are exceptional circumstances when lines should start with a semicolon.
However, these circumstances are not common, and you should ratify your decision
to use one before beginning a line with a semicolon.

Here is Isaacs' run down on those circumstances (verbatim, from
[here](https://npmjs.org/doc/coding-style.html)):

- `for (;;)` loops. They're actually required.
- null loops like: `while (something) ;` (But you'd better have a good reason for doing that.)
- `case "foo": doSomething(); break`
- In front of a leading `(` or `[` at the start of the line. This prevents the expression from being interpreted as a function call or property access, respectively.

Some examples of good semicolon usage:

```
;(x || y).doSomething()
;[a, b, c].forEach(doSomething)
for (var i = 0; i < 10; i++) {
  switch (state) {
    case "begin": start(); continue
    case "end": finish(); break
    default: throw new Error("unknown state")
  }
  end()
}
```

Note that starting lines with - and + also should be prefixed with a semicolon, but this is much less common.

**__To Recap:__ If a line begins with `[`, `(`, `+` or `-`, you should start it with a semicolon.**

## 80 characters per line

Limit your lines to 80 characters and *be strict about it*. Yes, screens have
gotten much bigger over the last few years, but your brain has not. Use the
additional room for split screen, your editor supports that, right?

## Use single quotes

Use single quotes, unless you are writing JSON.

*Right:*

```js
var foo = 'bar'
```

*Wrong:*

```js
var foo = "bar"
```

## Opening braces go on the same line

Your opening braces go on the same line as the statement.

*Right:*

```js
if (true) {
  console.log('winning')
}
```

*Wrong:*

```js
if (true)
{
  console.log('losing')
}
```

Also, notice the use of whitespace before and after the condition statement.

## One liners

Blocks containing a single statement may appear on one line, if desired. Curly
braces should be omitted. Blocks containing more than one statement (and an `if`
that has any `else if`s or an `else`) should always appear on multiple lines with
braces. This is because the most important tokens should
always appear on the left.

*Right*:

```
if (true) console.log('winning')

if (true) {
  console.log('winning')
} else {
  console.log('losing')
}
```

*Wrong*:

```
if (true) { console.log('winning') }
if (true) console.log('winning') else console.log('losing')
```

## Declare many variables per var statement

Declare many variables per var statement as it is less to type, and less
visual noise.

*Right:*

```js
var keys = [ 'foo', 'bar' ]
  , values = [ 23, 42 ]
  , object = {}
  , key

while (items.length) {
  key = keys.pop()
  object[key] = values.pop()
}
```

*Wrong:*

```js
var keys   = [ 'foo', 'bar' ]
var values = [ 23, 42 ]

var object = {};
while (items.length) {
  var key = keys.pop()
  object[key] = values.pop()
}
```

## Use lowerCamelCase for variables, properties and function names

Variables, properties and function names should use `lowerCamelCase`.  It is
most preferrable to use a single word for a variable name. Make an effort to
choose a good balance between meaningfull-ness and brevity. Single character
variables should generally be avoided, but are occasionally acceptable.

*Right:*

```js
var admins = db.query('SELECT * FROM users ...');
```

*Wrong:*

```js
var admin_user = db.query('SELECT * FROM users ...')
```

```js
var adminUsersFromDb = db.query('SELECT * FROM users ...')
```

## Use UpperCamelCase for constructors

Constructors should be capitalized using `UpperCamelCase` (also known as
Pascal Case).

*Right:*

```js
function BankAccount() {
}
```

*Wrong:*

```js
function bank_Account() {
}
```

## Use UPPERCASE for Constants

Constants should be declared as regular variables or static class properties,
using all uppercase letters.

Node.js / V8 actually supports mozilla's [const][const] extension, but
unfortunately that cannot be applied to class members, nor is it part of any
ECMA standard.

*Right:*

```js
var SECOND = 1 * 1000

function File() {
}
File.FULL_PERMISSIONS = 0777
```

*Wrong:*

```js
const SECOND = 1 * 1000

function File() {
}
File.fullPermissions = 0777
```

[const]: https://developer.mozilla.org/en/JavaScript/Reference/Statements/const

## Object / Array creation

Use comma first style and put *short* declarations on a single line. Only quote
keys when your interpreter complains:

*Right:*

```js
var a = [ 'hello', 'world' ]
var b =
  { good: 'code'
  , 'is generally': 'pretty'
  }
```

*Wrong:*

```js
var a = [
  'hello', 'world'
]
var b = {
  "good": 'code',
  is generally: 'pretty'
};
```

*Right:*

```
var required =
  [ 'main-nav'
  , 'local-news-selector'
  , 'notifications'
  , 'datepicker'
  ]
```

*Wrong:*

```
var required = [
  'main-nav',
  'local-news-selector',
  'notifications',
  'datepicker',
]
```
For an explanation on why to use comma-first, look no further than
[this gist by Isaacs][9]. Deviate slightly from the npm style here about the
level of indentation. The npm style is to line up with where the opening symbol
naturally occurs:

*Wrong:*

```
var myObj = { propA: 10
            , proB: 20
            }
```

It is better to have consistent levels of indenation, which means you don’t have
to maintain all those indents if you rename the variable. Break a line and
indent before the start symbol:

*Right:*

```
  var myObj =
    { propA: 10
    , proB: 20
    }
```

## Use the === operator

Programming is not about remembering [stupid rules][comparisonoperators]. Use
the triple equality operator as it will work just as expected.

*Right:*

```js
var a = 0
if (a === '') {
  console.log('winning')
}

```

*Wrong:*

```js
var a = 0
if (a == '') {
  console.log('losing')
}
```

[comparisonoperators]: https://developer.mozilla.org/en/JavaScript/Reference/Operators/Comparison_Operators

## Use the ternary operator

The ternary operator should be used on a single line if it will fit within the 80
char limit. Split it up into multiple lines if it doesn't.

*Right:*

```js
var foo = (a === b) ? 1 : 2
```

*Wrong:*

```js
var foo = (aReallyLongVariableName.someProperty === bReallyLongVariableName.someProperty) ? 1 : 2
```

## Do not extend built-in prototypes

Do not extend the prototype of native JavaScript objects. Unless you are writing
or using a 'polyfill' to simulate standard behaviour in old environments.

*Right:*

```js
var a = []
if (!a.length) {
  console.log('winning')
}
```

*Wrong:*

```js
Array.prototype.empty = function () {
  return !this.length
}

var a = []
if (a.empty()) {
  console.log('losing')
}
```

## Use descriptive conditions

Any non-trivial conditions should be assigned to a descriptive variable:

*Right:*

```js
var isAuthorized = (user.isAdmin() || user.isModerator())
if (isAuthorized) {
  console.log('winning')
}
```

*Wrong:*

```js
if (user.isAdmin() || user.isModerator()) {
  console.log('losing')
}
```

## Write small functions

Keep your functions short. A good function fits on a slide that the people in
the last row of a big room can comfortably read. So don't count on them having
perfect vision and limit yourself to ~15 lines of code per function.

## Limit your parameters

Functions should aim to have less than 5 parameters. 5 is the most that
any should have. If you find yourself wanting more paramaters, you should
generally use an options hash instead.

*Good:*

```
function animate(el, options, cb) {
  ...
}
```

*Bad:*

```
function animate(el, duration, ease, delay, properties, cb) {
  ...
}
```

## Keep your files small
There are times when a 1,000+ line file is needed but as a general rule of thumb
try and keep your file < 300 lines. More than 500 lines and it's starting to be
a code smell.

## Return early from functions

To avoid deep nesting of if-statements, always return a functions value as early
as possible.

*Right:*

```js
function isPercentage(val) {
  if (val < 0) {
    return false
  }

  if (val > 100) {
    return false
  }

  return true
}
```

*Wrong:*

```js
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true
    } else {
      return false
    }
  } else {
    return false
  }
}
```

Or for this particular example it may also be fine to shorten things even
further:

```js
function isPercentage(val) {
  var isInRange = (val >= 0 && val <= 100)
  return isInRange
}
```

## Name your closures

Feel free to give your closures a name. It shows that you care about them, and
will produce better stack traces, heap and cpu profiles.

*Right:*

```js
req.on('end', function onEnd() {
  console.log('winning')
});
```

*Wrong:*

```js
req.on('end', function () {
  console.log('losing')
});
```

## Limit nested closures

Use closures, but don't nest them too much. Otherwise your code will become a mess.
Your 80 char line limit should help prevent you nesting too far.

*Right:*

```js
setTimeout(function () {
  client.connect(afterConnect)
}, 1000)

function afterConnect() {
  console.log('winning')
}
```

*Wrong:*

```js
setTimeout(function () {
  client.connect(function () {
    console.log('losing')
  });
}, 1000)
```

## Comments

Inline comments should be line comments: `//`, regardless of how many lines
they span, eg:

      // Only run on browsers that support media queries.
      // If a browser doesn't support media queries, .mq()
      // will always return false.
      if (!window.Modernizr.mq('(min-width:0px)')) return
      breakPoints.push(new BreakPoint(name, media).check())

  Comments describing the functionality of a method or function should be
  multi-line comments: `/* */`, eg:

      /*
       * Sanitizes a file-type extension
       */
      function getFormat(f) {
        switch (f) {
          case '.jpg': return 'jpeg'
          case '.gif': return 'gif'
          default: return 'png'
        }
      }

Try to write comments that explain higher level mechanisms or clarify difficult
segments of your code. Don't use comments to restate trivial things. Be terse,
to the point and don't waffle.

*Right:*

```js
// 'ID_SOMETHING=VALUE' -> [ 'ID_SOMETHING=VALUE'', 'SOMETHING', 'VALUE' ]
var matches = item.match(/ID_([^\n]+)=([^\n]+)/))

// This function has a nasty side effect where a failure to increment a
// redis counter used for statistics will cause an exception. This needs
// to be fixed in a later iteration.
function loadUser(id, cb) {
  // ...
}

var isSessionValid = (session.expires < Date.now())
if (isSessionValid) {
  // ...
}
```

*Wrong:*

```js
// Execute a regex
var matches = item.match(/ID_([^\n]+)=([^\n]+)/))

// Usage: loadUser(5, function () { ... })
function loadUser(id, cb) {
  // ...
}

// Check if the session is valid
var isSessionValid = (session.expires < Date.now())
// If the session is valid
if (isSessionValid) {
  // ...
}
```

## Errors

Use actual Error objects for errors, not strings or any other type of object.
Justification [here](http://www.devthought.com/2011/12/22/a-string-is-not-an-error/).

Don't `throw` in asynchronous code.

*Right*

```
if (unicorns.length < 10) {
  callback(new Error('not enough unicorns'))
}
```

*Wrong:*

```
if (unicorns.length < 10) {
  callback('not enough unicorns')
}
```

```
if (unicorns.length < 10) {
  callback('not enough unicorns')
}
```

```
if (unicorns.length < 10) {
  throw 'not enough unicorns'
} else {
  callback(null, unicorns)
}
```

## Asynchronous function signature

Writing asynchronous functions with a callback, the callback's signature should
always be `function (err, data) { ... }`.

## Prefer function declaration over assigning a function expression

To define a function in the current scope, use a function declaration. Don't assign
the result of a function expression to a variable.

*Right:*

```
function greet() {
  console.log('hello')
}
```

*Wrong:*

```
var greet = function () {
  console.log('hello')
}
```

## module.exports

When writing in a node style environment, export only one thing from your module.
In general, if you are assigning multiple exports, you have designed a poor API
or you have written several modules that should be separated out.

*Right*:

```
module.exports = jim
```

*Wrong*:

```
module.exports.jim = jim
module.exports.bob = bob
module.exports.barry = barry
```

## Object.freeze, Object.preventExtensions, Object.seal, with, eval

Crazy shit that you will probably never need. Stay away from it.

## Getters and setters

Do not use setters, they cause more problems for people who try to use your
software than they can solve.

Feel free to use getters that are free from [side effects][sideeffect], like
providing a length property for a collection class.

[sideeffect]: http://en.wikipedia.org/wiki/Side_effect_(computer_science)