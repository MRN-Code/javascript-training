# NPM

[npm](https://www.npmjs.com) is the primary package manager for JavaScript code. Its CLI tool comes bundled with all recent builds of Node.js.

JavaScript adheres to the UNIX philosophy: published modules are generally small and focus on doing a single task well. We use these pieces to compose our application. Finding packages is easy: search on https://npmjs.com/ or on http://npms.io/. Measuring packages' quality is more difficult. npms.io has some decent metrics, but it's always good to look at download statistics, number of dependencies, quality of documentation, existence/quality of tests, project contributors, open issues/PRs, etc. (Do an example search?)

## Discuss:

* npm scripts, `test` and `start`
* dev dependencies versus dependencies, running with NODE_ENV=production
* global packages
* versioning: semver, the caret, locking to versions
* Using GitHub instead of npm for source
* Publishing: use preset scripts

## Commands:

* npm init: initialize your project with a package.json
* npm install: install dependencies. Use --save-dev (-D) to save in `devDependencies`, or --save (-S) to save in `dependencies
* npm prune: remove dependencies no longer referenced in your package.json
* npm update: Upgrades top-level packages. Use --save (-S) to persist updates to your package.json. Use --dev to upgrade dev dependencies, too.
* npm link: link modules together for development
* npm rebuild: Rebuilds native modules. Use this if you change versions of Node.js.
* npm publish: publish the module!

You can always type `npm help [command]` to get help. The docs are excellent.

## Further readings:

* https://blog.risingstack.com/nodejs-at-scale-npm-best-practices/
* https://docs.npmjs.com
* https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/

