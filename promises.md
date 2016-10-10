# Promises

Promises are sugar for callbacks that make asynchronous code easier to write and read. They underlie most new language features (`async`/`await`) and HTML APIs (Service Workers, etc.).

We use [Bluebird.js](http://bluebirdjs.com/docs/getting-started.html) in several projects. It was especially helpful when native Promise support was low, especially in browsers. Nowadays, Promises are global in Node.js and [all modern browsers have ‘em](http://caniuse.com/#feat=promises). Some nice things Bluebird.js adds:

* promisifying: wrap functions expecting a callback and make them return a new Promise
* finally: adds a `finally` method to Promise instances. It’s called regardless of the Promise's state
* Collection methods: props, map, reduce, etc. These make dealing with several Promises easier.

However, I find that Bluebird.js oftentimes is unnecessary (show an implementation of map, an implementation of filter, etc.). It emits annoying warnings (disable with BLUEBIRD_WARNINGS=0), and adds some difficulty to debugging and tracing rejections. Prefer native when possible.

## Further readings:

* https://developers.google.com/web/fundamentals/getting-started/primers/promises
* https://davidwalsh.name/promises
* https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html
