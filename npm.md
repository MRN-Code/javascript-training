# NPM

[npm](https://www.npmjs.com) is the primary package manager for JavaScript code. Its CLI tool comes bundled with all recent builds of Node.js.

JavaScript adheres to the UNIX philosophy: published modules are generally small and focus on doing a single task well. We use these pieces to compose our application. Finding packages is easy: search on https://npmjs.com/ or on http://npms.io/. Measuring packages' quality is more difficult. npms.io has some decent metrics, but it's always good to look at download statistics, number of dependencies, quality of documentation, existence/quality of tests, project contributors, open issues/PRs, etc. (Do an example search?)

## Discuss:

* **dependencies:**

  npm has the concept of 'development' dependencies, referred to as 'dev dependencies', and 'production' dependencies, referred to as just 'dependencies'. These are separated in your _package.json_ under different properties:

  ```json
  {
    "name": "my-module",
    "dependencies": {
      "bluebird": "3.4.6",
      "lodash": "^4.16.4"
    },
    "devDependencies": {
      "tape": "^4.6.2"
    }
  }
  ```

  When `my-module` is installed in _another_ module as a dependency only packages listed in `dependencies` are installed. If `my-module` is the root module (it's cloned and under development) modules in both `dependencies` and `devDependencies` will be installed.

  One potential issue occurs when the `NODE_ENV` environment variable is set to `production`. In this case, _only_ `dependencies` are installed.
  
* **global packages:**
  
  Make a npm package available on your system by installing it globally. There are a few packages that must be used this way, like [Grunt](http://gruntjs.com):

  ```shell
  # Install Grunt globally with the '-g' flag:
  npm install -g grunt-cli

  # 'grunt' CLI now available:
  grunt --help
  ```

  Add the [`preferGlobal` property](https://docs.npmjs.com/files/package.json#preferglobal) to your _package.json_ file if you want npm to warn users when they **don't** install your package globally:

  ```json
  {
    "preferGlobal": true
  }
  ```

* **versioning:** npm expects dependencies’ versions to adhere to [semver](http://semver.org). Version numbers may be modified to specify ranges using [special characters](https://docs.npmjs.com/getting-started/semantic-versioning), like `^`, `~`, and `*`.
* **changing source:**

  Use GitHub instead of npm as a source:

  ```shell
  npm install user/repo#branch
  ```

  You can also use just about anything that’s a tarball and contains a _package.json_ file. See [npm install documentation](https://docs.npmjs.com/cli/install) for more information.

* **publishing:** Run `npm publish` to push your module to the registry.
* **npm scripts:**

  npm allows the inclusion of runable scripts in the `scripts` property inside a _package.json_ file. An example:

  ```json
  {
    "scripts": {
      "build": "node scripts/build.js",
      "start": "node lib/index.js",
      "test": "node test/index.js"
    }
  }
  ```

  The `start` and `test` scripts maybe run via `npm start` and `npm test`, respectively. These are special cases; custom scripts, such as `build`, must be run as `npm run build`.

  Scripts may also have pre- and post-scripts via prefixes:

  ```json
  {
    "scripts": {
      "prebuild": "mkdir .tmp",
      "build": "node scripts/build.js",
      "postbuild": "rm -rf .tmp"
    }
  }
  ```

  Running `npm run build` results in the `prebuild` script running, followed by the `build` script and the `postbuild` script.

  You can also easily compose scripts, like so:

  ```json
  {
    "devDependencies": {
      "autoprefixer": "^6.5.1",
      "postcss-cli": "^2.6.0",
      "webpack": "^1.13.2"
    },
    "scripts": {
      "build:css": "postcss -c .postcssrc -u autoprefixer",
      "build:js": "NODE_ENV=production; webpack",
      "build": "npm run build:css && npm run build:js"
    }
  }
  ```

  The `build` script runs `build:css`, then `build:js`. You can also use [parallelshell](https://www.npmjs.com/package/parallelshell) to easily run scripts in parallel in a cross-environment manner:

  ```json
  {
    "devDependencies": {
      "autoprefixer": "^6.5.1",
      "parallelshell": "^2.0.0",
      "postcss-cli": "^2.6.0",
      "webpack": "^1.13.2"
    },
    "scripts": {
      "build:css": "postcss -c .postcssrc -u autoprefixer",
      "build:js": "NODE_ENV=production; webpack",
      "build": "parallelshell 'npm run build:css' 'npm run build:js'"
    }
  }
  ```

  More examples:

  * [coinstac-server-core](https://github.com/MRN-Code/coinstac/blob/fc89742e6fb6ca4c09fb43a8b07779921c84c43b/packages/coinstac-server-core/package.json#L7-L13)
  * [thealphanerd’s start-here](https://github.com/TheAlphaNerd/start-here/blob/867f9cee0c6910bfd03c69f4cddf12a7c53820a5/package.json#L17-L31)
  * [coins-pr-site](https://github.com/MRN-Code/coins-pr-site/blob/11b0480a35ac2b6f6f71328e127b7d45d7671cae/package.json#L61-L92)

  See the [npm scripts documentation](https://docs.npmjs.com/misc/scripts) and [`run-script` documentation](https://docs.npmjs.com/cli/run-script) for more information.

## Commands:

* `npm init`: initialize your project with a _package.json_. Pass a `-y` flag to skip the prompts and use the default _package.json_.
* `npm install`: install dependencies. Use `--save-dev` (`-D`) to save in `devDependencies`, or `--save` (`-S`) to save in `dependencies
* `npm prune`: remove dependencies no longer referenced in your _package.json_
* `npm update`: Upgrades top-level packages. Use `--save` (`-S`) to persist updates to your package.json. Use `--dev- to upgrade dev dependencies, too.
* `npm link`:

  Link separate modules together, making development and debugging easier.

  ```shell
  # Go to development module:
  cd module-a
  # links 'module-a' by creating a symlink in npm's global modules
  npm link

  # Go to parent module, which depends on 'module-a'
  cd ../module-b
  # links 'module-a' inside 'module-b' by creating a symlink that points to
  # 'module-a's global symlink
  npm link module-a
  ```

  See [npm’s link documentation](https://docs.npmjs.com/cli/link) for more information.

* `npm rebuild`: Rebuilds native modules. Use this if you change versions of Node.js.
* `npm publish`: publish the module!

You can always type `npm help [command]` to get help. The docs are excellent.

## Further readings:

* https://blog.risingstack.com/nodejs-at-scale-npm-best-practices/
* https://docs.npmjs.com
* https://www.keithcirkel.co.uk/how-to-use-npm-as-a-build-tool/

