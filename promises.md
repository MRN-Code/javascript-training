# Promises

Promises are sugar for callbacks that make asynchronous code easier to write and read. They underlie most new language features (`async`/`await`) and HTML APIs (fetch, ServiceWorker, etc.).

We use [Bluebird.js](http://bluebirdjs.com/docs/getting-started.html) in several projects. It was especially helpful when native Promise support was low, especially in browsers. Nowadays, Promises are global in Node.js and [all modern browsers have ‘em](http://caniuse.com/#feat=promises). Some nice things Bluebird.js adds:

* **promisifying:**

  Wrap functions expecting a callback and make them return a new `Promise`:

  ```js
  const bluebird = require('bluebird');
  const fs = require('fs');

  bluebird.promisify(fs.readFile)('./path/to/file.txt')
    .then(d => d.toString())
    .catch(console.error);
  ```

  `bluebird.promisify(fs.readFile)` returns a wrapped [`fs.readFile`](https://nodejs.org/api/fs.html#fs_fs_readfile_file_options_callback) that operates without a callback parameter, instead returning a `Promise`. You can use `.then`, `.catch`, and any other Bluebird-y instance methods. See [Bluebird’s `promisify` documentation](http://bluebirdjs.com/docs/api/promise.promisify.html) for more details.
* **finally:** Bluebird adds a `.finally` method to Promise instances. It’s called regardless of whether an instance resolves or rejects. See [Bluebird’s `.finally` documentation](http://bluebirdjs.com/docs/api/finally.html) for more details.
* **Collection methods:** `.props`, `.map`, `.reduce`, etc. These make dealing with several Promises easier.

However, I find that Bluebird.js oftentimes is unnecessary. It emits annoying warnings (disable with `BLUEBIRD_WARNINGS=0`), and adds some difficulty to debugging and tracing rejections. Prefer native when possible.

When handing side-effects or synchronous code in a Promise chain, ensure that you return a value!

This doesn’t work:

```js
doSomethingAsync()
  .then(() => {
    doSomethingElseAsync();
  })
  .then(itShouldBeDone);
```

`doSomethingElseAsync` is called, but its return value is lost!

### Bluebird.js’s Promise Reflection

Bluebird [offers a way](http://bluebirdjs.com/docs/api/reflect.html) to perform several asynchronous actions without erroring:

```js
// Assumes methods return Bluebird promises
Promise.all(
  [getUsers(), getStudies(), getConsortia()].map(p => p.reflect())
).each(inspection => {
  if (inspection.isFullfilled()) {
    console.log(inspection.value());
  } else {
    console.error(inspection.reason());
  }
});
```

### Mapping:

```js
// `ids` is an array, like `[100, 101, 102, 103]`
function getUsersByIds(ids) {
  return Promise.all(ids.map(id => {
    return fetch(`http://localhost:1337/api/users/${id}`);
  }));
}
```

### Filtering:

```js
function getEvenUsersByIds(ids) {
  return Promise.all(
    ids
      .filter(id => !(id % 2))
      .map(id => fetch(`http://localhost:1337/api/users/${id}`))
  );
}

function betterGetEvenUsersByIds(ids) {
  return Promise.all(ids.reduce((memo, id) => {
    return id % 2 ?
      memo :
      memo.concat(fetch(`http://localhost:1337/api/users/${id}`));
  }, []));
}
```

### Handling `.all`s with destructuring

```js
getUser()
  .then(user => {
    return Promise.all([
      user,
      getUserAttributes(user),
      getUserPermissions(user),
    ])
  })
  .then(([user, attributes, permissions ]) => {
    console.log(user, attributes, permissions);
  })
  .catch(console.error.bind(error));
```

## Further readings:

* https://developers.google.com/web/fundamentals/getting-started/primers/promises
* https://davidwalsh.name/promises
* https://pouchdb.com/2015/05/18/we-have-a-problem-with-promises.html



