# Testing

Testing ensures your program works as expected. Writing tests provides an easy, repeatable, fast way to make sure modules don't break on changes or dependency updates. It promotes writing code in a style that's modular and avoids side effects.

Integration testing versions functional (end-to-end) test versus unit testing. Don't test vendor code!

## Tools:

* [tape](https://www.npmjs.com/package/tape): Basic assertions and test running, TAP-style. Used in coinstac.
* [sinon](http://sinonjs.org/docs/): Useful spying, stubbing and mocking library. Manipulate your libraries!
* [mockery](https://www.npmjs.com/package/mockery): Hijack Node.js’s module system to stub modules.
* [nock](https://www.npmjs.com/package/nock): Mock HTTP for Node.js.
* [Mocha](https://mochajs.org): Full-featured testing framework. Used in coins-browser-test and steelpenny.
* [Should.js](https://shouldjs.github.io): Behavior-driven assertion library. Used in coins-browser-test and steelpenny.
* [nyc](https://www.npmjs.com/package/nyc): Istanbul wrapper for testing with code coverage.
* [testem](https://github.com/testem/testem): Run tests in browsers.

## Further readings:

* https://www.sitepoint.com/javascript-testing-unit-functional-integration/
* http://stackoverflow.com/a/680713
