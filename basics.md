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

JavaScript has two data types: primitives and non-primitives. **Primitives are passed by value** (immutable), and **non-primitives are passed by reference** (mutable). Everything can be treated like an object, mostly.

* Primitives: string, number, boolean, symbol, null, undefined
* Non-primitives: Object, Function, Array, Date, typed arrays, Map, WeakMap, Set, WeakSet (ES6 stuff)

Determine a argument's type using `typeof`. (This can backfire when you're testing against `null`.) If you're testing for truthiness it isn't necessary to test for type. Determine if an object has a reference in its prototype chain by using `instanceof`.

Some ES6 features that you can use today (depending on version of Node.js):

* String templates
* Destructuring, default params, spread:

  ```js
  // Object
  const { a, b } = { a: 1, b: 2 };
  console.log(a, b); // 1, 2

  // Array
  const [c, d, ...e] = [1, 2, 3, 4, 5];
  console.log(c, d); // 1, 2
  console.log(e); // [4, 5, 6]
  ```

  See [MDN’s _Destructuring assignment_ article](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) for more examples, and check the [ES6 compatibility table](http://kangax.github.io/compat-table/es6/) to ensure the target version of Node.js supports destructuring.
* Easy constructor functions with `class` and prototypal inheritance with `extends`:

  These constructs are sugar for constructor functions:

  ```js
  // Constructor:
  function MyClass(params) {
    this.params = params;
  }

  MyClass.prototype.logParams() {
    console.log(this.params);
  };

  // ES6 class:
  class MyClass {
    constructor(params) {
      this.params = params;
    }
    logParams() {
      console.log(this.params);
    }
  }
  ```

  The two `MyClass` constructors are the same. `extends` provides an easy way to “inherit” via prototype modification:

  ```js
  // Constructor
  function MyGreatClass(params, greatParams) {
    MyClass.call(this, params);
    this.greatParams = greatParams;
  }
  MyGreatClass.prototype = Object.create(MyClass.prototype);
  MyGreatClass.prototype.constructor = MyGreatClass;
  MyGreatClass.prototype.logGreatParams() {
    console.log(this.greatParams);
  };

  // ES6 class:
  class MyGreatClass extends MyClass {
    constructor(params, greatParams) {
      super(params);
      this.greatParams = greatParams;
    }
    logGreatParams() {
      console.log(this.greatParams);
    }
  }
  ```

  The sugar makes prototypal inheritance quite a bit easier. Read [MDN’s _Classes_ document](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes).

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
