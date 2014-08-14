# Relaxed JSON

[![Build Status](https://secure.travis-ci.org/phadej/relaxed-json.svg?branch=master)](http://travis-ci.org/phadej/relaxed-json)
[![NPM version](https://badge.fury.io/js/relaxed-json.svg)](http://badge.fury.io/js/relaxed-json)
[![Dependency Status](https://gemnasium.com/phadej/relaxed-json.svg)](https://gemnasium.com/phadej/relaxed-json)
[![Code Climate](https://img.shields.io/codeclimate/github/phadej/relaxed-json.svg))](https://codeclimate.com/github/phadej/relaxed-json)

Are you frustrated that you cannot add comments into your configuration JSON
Relaxed JSON is a simple solution.
Small JavaScript library with only one exposed function `RJSON.transform(text : string) : string`
(and few convenient helpers).

[Relaxed JSON](http://oleg.fi/relaxed-json) (modified BSD license) is a strict superset of JSON,
relaxing strictness of valilla JSON.
Valid, vanilla JSON will not be changed by `RJSON.transform`. But there are few additional
features helping writing JSON by hand.

* Comments are stripped : `// foo` and `/* bar */`  → `     `.
  Comments are converted into whitespace, so your formatting is preserved.
* Trailing comma is allowed : `[1, 2, 3, ]` → `[1, 2, 3]`. Works also in objects `{ "foo": "bar", }` → `{ "foo": "bar" }`.
* Identifiers are transformed into strings : `{ foo: bar }` → `{ "foo": "bar" }`.
* Single quoted strings are allowed : `'say "Hello"'` → `"say \"Hello\""`.
* More different characters is supported in identifiers: `foo-bar` → `"foo-bar"`.

## API

- `RJSON.transform(text : string) : string`.
  Transforms Relaxed JSON text into JSON text. Doesn't verify (parse) the JSON, i.e result JSON might be invalid as well
- `RJSON.parse(text : string, reviver : function | opts : obj) : obj`.
  Parse the RJSON text, virtually `JSON.parse(JSON.transform(text), reviver)`.
  You could pass a reviver function or an options object as the second argument. Supported options:
  - `reviver`: you could still pass a reviver
  - `relaxed`: use relaxed version of JSON (default: true)
  - `warnings`: use relaxed JSON own parser, supports better error messages (default: false).
  - `duplicate`: fail if there are duplicate keys in objects

## Executable

There is `rjson` executable<sup>&dagger;</sup>

```sh
$ sudo npm install -g relaxed-json

$ rjson relaxed-json.js
Error on line 27: Unexpected character: (
(function () {

% rjson package.json   
{
  "name": "relaxed-json",
  "description": "Relaxed JSON is strict superset JSON, relaxing strictness of valilla JSON",

<sup>&dagger;</sup>`rjson` is similar to `python -mjson.tool`.

## Changelog

- 0.2.6 Dependencies update
- 0.2.5 Use `make`
- 0.2.4 Maintenance release
- 0.2.3 Bugfixes
  - `$` is valid identifier character
  - single line comments may end with `CR` and `CRLF` also
- 0.2.2 Bugfix
- 0.2.1 Code reogranization
  - More though into toleration, handles valid json without colons and commas
  - trailing comma stripping is more strict
- 0.2.0 Shiny new features
  - overloaded `rjson.parse`
  - tolerating parser support
  - duplicate key warning
  - test suite (!)
- 0.1.1 RJSON.parse
- 0.1.0 Initial release
