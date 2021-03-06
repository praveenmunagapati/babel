# Contributing

## Adding a new plugin to support (when approved in the next ECMAScript version)

### Update [`plugin-features.js`](https://github.com/babel/babel-preset-env/blob/master/data/plugin-features.js)

*Example:*

If you were going to add `**` which is in ES2016:

Find the relevant entries on [compat-table](https://kangax.github.io/compat-table/es2016plus/#test-exponentiation_(**)_operator):

`exponentiation (**) operator`

Find the corresponding babel plugin:

`transform-exponentiation-operator`

And add them in this structure:

```js
// es2016
"@babel/transform-exponentiation-operator": {
  features: [
    "exponentiation (**) operator",
  ],
},
```

### Update [`built-in-features.js`](https://github.com/babel/babel-preset-env/blob/master/data/built-in-features.js)

*Example:*

In case you want to add `Object.values` which is in ES2017:

Find the relevant feature and subfeature on [compat-table](https://kangax.github.io/compat-table/es2016plus/#test-Object_static_methods_Object.values)
and split it with `/`:

`Object static methods / Object.values`

Find the corresponding module on [core-js](https://github.com/zloirock/core-js/tree/master/modules):

`es7.object.values.js`

Find required ES version in [`built-in-features.js`](https://github.com/babel/babel-preset-env/blob/master/data/built-in-features.js) and add the new feature:

```js
const es2017 = {
  //...
  "es7.object.values": "Object static methods / Object.values"
}
```

### Update [`plugins.json`](https://github.com/babel/babel-preset-env/blob/master/data/plugins.json)

Until `compat-table` is a standalone npm module for data we are using the git url

`"compat-table": "kangax/compat-table#[latest-commit-hash]"`,

So we update and then run `npm run build-data`. If there are no changes, then `plugins.json` will be the same.

## Tests

### Running tests locally

```bash
npm test
```

### Checking code coverage locally

```bash
npm run coverage
```

### Writing tests

#### General

All the tests for `babel-preset-env` exist in the `test/fixtures` folder. The
test setup and conventions are exactly the same as testing a Babel plugin, so
please read our [documentation on writing tests](https://github.com/babel/babel/blob/master/CONTRIBUTING.md#babel-plugin-x).

#### Testing the `debug` option

Testing debug output to `stdout` is similar. Under the `test/debug-fixtures`,
create a folder with a descriptive name of your test, and add the following:

* Add a `options.json` file (just as the other tests, this is essentially a
`.babelrc`) with the desired test configuration (required)
* Add a `stdout.txt` file with the expected debug output. For added
convenience, if there is no `stdout.txt` present, the test runner will
generate one for you.
