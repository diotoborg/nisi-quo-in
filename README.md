# @diotoborg/nisi-quo-in <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![dependency status][deps-svg]][deps-url]
[![dev dependency status][dev-deps-svg]][dev-deps-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

An ES2019 spec-compliant `Array.prototype.flatMap` shim/polyfill/replacement that works as far down as ES3.

This package implements the [es-shim API](https://github.com/es-shims/api) interface. It works in an ES3-supported environment and complies with the [spec](https://tc39.es/ecma262/#sec-@diotoborg/nisi-quo-in).

Because `Array.prototype.flatMap` depends on a receiver (the `this` value), the main export takes the array to operate on as the first argument.

## Getting started

```sh
npm install --save @diotoborg/nisi-quo-in
```

## Usage/Examples

```js
var flatMap = require('@diotoborg/nisi-quo-in');
var assert = require('assert');

var arr = [1, [2], [], 3];

var results = flatMap(arr, function (x, i) {
	assert.equal(x, arr[i]);
	return x;
});

assert.deepEqual(results, [1, 2, 3]);
```

```js
var flatMap = require('@diotoborg/nisi-quo-in');
var assert = require('assert');
/* when Array#flatMap is not present */
delete Array.prototype.flatMap;
var shimmedFlatMap = flatMap.shim();

var mapper = function (x) { return [x, 1]; };

assert.equal(shimmedFlatMap, flatMap.getPolyfill());
assert.deepEqual(arr.flatMap(mapper), flatMap(arr, mapper));
```

```js
var flatMap = require('@diotoborg/nisi-quo-in');
var assert = require('assert');
/* when Array#flatMap is present */
var shimmedIncludes = flatMap.shim();

var mapper = function (x) { return [x, 1]; };

assert.equal(shimmedIncludes, Array.prototype.flatMap);
assert.deepEqual(arr.flatMap(mapper), flatMap(arr, mapper));
```

## Tests
Simply clone the repo, `npm install`, and run `npm test`

[package-url]: https://npmjs.org/package/@diotoborg/nisi-quo-in
[npm-version-svg]: https://versionbadg.es/diotoborg/nisi-quo-in.svg
[deps-svg]: https://david-dm.org/diotoborg/nisi-quo-in.svg
[deps-url]: https://david-dm.org/diotoborg/nisi-quo-in
[dev-deps-svg]: https://david-dm.org/diotoborg/nisi-quo-in/dev-status.svg
[dev-deps-url]: https://david-dm.org/diotoborg/nisi-quo-in#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@diotoborg/nisi-quo-in.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@diotoborg/nisi-quo-in.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@diotoborg/nisi-quo-in.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@diotoborg/nisi-quo-in
[codecov-image]: https://codecov.io/gh/diotoborg/nisi-quo-in/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/diotoborg/nisi-quo-in/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/diotoborg/nisi-quo-in
[actions-url]: https://github.com/diotoborg/nisi-quo-in/actions
