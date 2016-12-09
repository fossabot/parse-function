# parse-function [![NPM version](https://img.shields.io/npm/v/parse-function.svg?style=flat)](https://www.npmjs.com/package/parse-function) [![NPM downloads](https://img.shields.io/npm/dm/parse-function.svg?style=flat)](https://npmjs.org/package/parse-function) [![npm total downloads][downloads-img]][downloads-url]

> Parse a function to an object that has its name, body, args and few more useful properties. Support regular functions, async/await, arrow and generator functions.

[![code climate][codeclimate-img]][codeclimate-url] 
[![standard code style][standard-img]][standard-url] 
[![linux build status][travis-img]][travis-url] 
[![windows build status][appveyor-img]][appveyor-url] 
[![coverage status][coveralls-img]][coveralls-url] 
[![dependency status][david-img]][david-url]

## Table of Contents
- [Install](#install)
- [Usage](#usage)
- [API](#api)
  * [parseFunction](#parsefunction)
- [Related](#related)
- [Contributing](#contributing)
- [Building docs](#building-docs)
- [Running tests](#running-tests)
- [Author](#author)
- [License](#license)

_(TOC generated by [verb](https://github.com/verbose/verb) using [markdown-toc](https://github.com/jonschlinkert/markdown-toc))_

## Install
Install with [npm](https://www.npmjs.com/)

```
$ npm install parse-function --save
```

or install using [yarn](https://yarnpkg.com)

```
$ yarn add parse-function
```

## Usage
> For more use-cases see the [tests](test.js)

```js
const parseFunction = require('parse-function')
```

## API

### [parseFunction](index.js#L64)
> Parse a function or string that contains a function, using [babylon][] or [acorn][] parsers. By default it uses `babylon`, but you can pass custom one through `options.parser` option - for example pass `.parse: acorn.parse` to force use the `acorn` parser instead.

**Params**

* `code` **{Function|String}**: function to be parsed, it can be string too    
* `options` **{Object}**: optional, passed directly to [babylon][] or [acorn][]; you can also pass custom `options.parser` parser    
* `returns` **{Object}**: always returns an object, check `result.valid`  

**Example**

```js
const acorn = require('acorn')
const acornLoose = require('acorn/dist/acorn_loose')
const parseFunction = require('parse-function')

const myFn = function abc (e, f, ...rest) { return 1 + e + 2 + f }
const parsed = parseFunction(myFn)

console.log(parsed.name) // => 'abc'
console.log(parsed.body) // => ' return 1 + e + 2 + f '
console.log(parsed.args) // => [ 'e', 'f', 'rest' ]
console.log(parsed.params) // => 'e, f, rest'

// some useful `is*` properties
console.log(parsed.isNamed) // => true
console.log(parsed.isArrow) // => false
console.log(parsed.isAnonymous) // => false
console.log(parsed.isGenerator) // => false

// use `acorn` parser
const someArrow = (foo, bar) => 1 * foo + bar
const result = parseFunction(someArrow, {
  parser: acorn.parse,
  ecmaVersion: 2017
})

console.log(result.name) // => 'anonymous'
console.log(result.body) // => '1 * foo + bar'
console.log(result.args) // => [ 'foo', 'bar' ]

console.log(result.isArrow) // => true
console.log(result.isNamed) // => false
console.log(result.isAnonymous) // => true
```

## Related
- [always-done](https://www.npmjs.com/package/always-done): Handle completion and errors with elegance! Support for streams, callbacks, promises, child processes, async/await and sync functions. A drop-in replacement… [more](https://github.com/hybridables/always-done#readme) | [homepage](https://github.com/hybridables/always-done#readme "Handle completion and errors with elegance! Support for streams, callbacks, promises, child processes, async/await and sync functions. A drop-in replacement for [async-done][] - pass 100% of its tests plus more")
- [minibase](https://www.npmjs.com/package/minibase): Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing… [more](https://github.com/node-minibase/minibase#readme) | [homepage](https://github.com/node-minibase/minibase#readme "Minimalist alternative for Base. Build complex APIs with small units called plugins. Works well with most of the already existing [base][] plugins.")
- [try-catch-core](https://www.npmjs.com/package/try-catch-core): Low-level package to handle completion and errors of sync or asynchronous functions, using [once][] and [dezalgo][] libs. Useful for and… [more](https://github.com/hybridables/try-catch-core#readme) | [homepage](https://github.com/hybridables/try-catch-core#readme "Low-level package to handle completion and errors of sync or asynchronous functions, using [once][] and [dezalgo][] libs. Useful for and used in higher-level libs such as [always-done][] to handle completion of anything.")

## Contributing
Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/tunnckoCore/parse-function/issues/new).  
Please read the [contributing guidelines](CONTRIBUTING.md) for advice on opening issues, pull requests, and coding standards.  
If you need some help and can spent some cash, feel free to [contact me at CodeMentor.io](https://www.codementor.io/tunnckocore?utm_source=github&utm_medium=button&utm_term=tunnckocore&utm_campaign=github) too.

**In short:** If you want to contribute to that project, please follow these things

1. Please DO NOT edit [README.md](README.md), [CHANGELOG.md](CHANGELOG.md) and [.verb.md](.verb.md) files. See ["Building docs"](#building-docs) section.
2. Ensure anything is okey by installing the dependencies and run the tests. See ["Running tests"](#running-tests) section.
3. Always use `npm run commit` to commit changes instead of `git commit`, because it is interactive and user-friendly. It uses [commitizen][] behind the scenes, which follows Conventional Changelog idealogy.
4. Do NOT bump the version in package.json. For that we use `npm run release`, which is [standard-version][] and follows Conventional Changelog idealogy.

Thanks a lot! :)

## Building docs
Documentation and that readme is generated using [verb-generate-readme][], which is a [verb][] generator, so you need to install both of them and then run `verb` command like that

```
$ npm install verbose/verb#dev verb-generate-readme --global && verb
```

_Please don't edit the README directly. Any changes to the readme must be made in [.verb.md](.verb.md)._

## Running tests
Clone repository and run the following in that cloned directory

```
$ npm install && npm test
```

## Author
**Charlike Mike Reagent**

+ [github/tunnckoCore](https://github.com/tunnckoCore)
+ [twitter/tunnckoCore](http://twitter.com/tunnckoCore)
+ [codementor/tunnckoCore](https://codementor.io/tunnckoCore)

## License
Copyright © 2016, [Charlike Mike Reagent](http://i.am.charlike.online). Released under the [MIT license](LICENSE).

***

_This file was generated by [verb-generate-readme](https://github.com/verbose/verb-generate-readme), v0.2.0, on December 09, 2016._

[always-done]: https://github.com/hybridables/always-done
[async-done]: https://github.com/gulpjs/async-done
[base]: https://github.com/node-base/base
[commitizen]: https://github.com/commitizen/cz-cli
[dezalgo]: https://github.com/npm/dezalgo
[once]: https://github.com/isaacs/once
[standard-version]: https://github.com/conventional-changelog/standard-version
[verb-generate-readme]: https://github.com/verbose/verb-generate-readme
[verb]: https://github.com/verbose/verb

[downloads-url]: https://www.npmjs.com/package/parse-function
[downloads-img]: https://img.shields.io/npm/dt/parse-function.svg

[codeclimate-url]: https://codeclimate.com/github/tunnckoCore/parse-function
[codeclimate-img]: https://img.shields.io/codeclimate/github/tunnckoCore/parse-function.svg

[travis-url]: https://travis-ci.org/tunnckoCore/parse-function
[travis-img]: https://img.shields.io/travis/tunnckoCore/parse-function/master.svg?label=linux

[appveyor-url]: https://ci.appveyor.com/project/tunnckoCore/parse-function
[appveyor-img]: https://img.shields.io/appveyor/ci/tunnckoCore/parse-function/master.svg?label=windows

[coveralls-url]: https://coveralls.io/r/tunnckoCore/parse-function
[coveralls-img]: https://img.shields.io/coveralls/tunnckoCore/parse-function.svg

[david-url]: https://david-dm.org/tunnckoCore/parse-function
[david-img]: https://img.shields.io/david/tunnckoCore/parse-function.svg

[standard-url]: https://github.com/feross/standard
[standard-img]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg

[acorn]: https://github.com/ternjs/acorn
[babylon]: https://babeljs.io/