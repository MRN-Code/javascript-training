# Basics

[JavaScript's operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators) are C-based, and very similar to PHP:

* `+`: Add numbers, concat strings
* `-`: Subtract numbers
* `*`: Multiple numbers
* `/`: Divisor: divide numbers
* `!`, `!!`: To boolean
* `=`: Assignment
* `==`: Equality
* `===`: Strict equality
* `<`: Less than
* `<=` Less than or equal to
* `>`: Greater than
* `>=`: Greater than or equal to

JavaScript has two data types: primitives and non-primitives. Everything can be treated like an object, mostly.

* Primitives: string, number, boolean, symbol, null, undefined
* Non-primitives: Object, Function, Array, Date, typed arrays, Map, WeakMap, Set, WeakSet (ES6 stuff)

Determine a argument's type using `typeof`. (This can backfire when you're testing against `null`.) If you're testing for truthiness it isn't necessary to test for type. Determine if an object has a reference in its prototype chain by using `instanceof`.

Some ES6 features that you can use today (depending on version of Node.js):

* String templates
* Destructuring, default params, spread (check LTS compatibility: http://kangax.github.io/compat-table/es6/)
* `class` and `extends` sugar (easy prototypal extension)
* Enhanced object literals
* `const`, `let` and block scoping
* Arrow functions
* Symbols
* Array methods: iterator, find, findIndex, fill, from
* Iterator protocol, generators, for…of loop
* Proxy and Reflection (?)

## Examples:

* Lambdas: functions as values, passing functions around
* Immutable data structures
* Scoping & closures

## Further reading:

* https://developer.mozilla.org/en-US/docs/Web/JavaScript/Data_structures
* https://www.reddit.com/r/LearnJavascript
* https://developer.mozilla.org/en-US/docs/Learn/JavaScript
* https://github.com/lukehoban/es6features
