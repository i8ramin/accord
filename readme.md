accord
======

A unified interface for compiled languages and templates in javascript.

[![npm](https://badge.fury.io/js/accord.png)](http://badge.fury.io/js/accord)
[![tests](https://travis-ci.org/jenius/accord.png?branch=master)](https://travis-ci.org/jenius/accord)
[![dependencies](https://david-dm.org/jenius/accord.png)](https://david-dm.org/jenius/accord)

### Why should you care?

There are two other libraries out there that already do this same thing, [consolidate.js](https://github.com/visionmedia/consolidate.js) and [transformers](https://github.com/ForbesLindesay/transformers). After looking over and using both of them, I decided to make this one anyway mainly because of **maintenance**. When creating an interface to many different languages, all of which are constantly changing, you need to be on top of maintenance, testing, and releases. Transformers is not well maintained or tested, which rules it out. Conslidate.js is a little better, but the maintenance at this point is mostly accepting pull requests from people who have changes, rather than actively keeping on top of it. TJ has a lot to do, I understand.

Compiling many different languages is a central component of [roots](http://roots.cx), and it needs a clean, well-managed, and tightly maintained and tested library that adapts to each supported language's interface. We (the maintainers of roots) are not comfortable forking and/or making pull requests into a library that we cannot feel 100% confident in, and so far we have not been able to find one that we are yet. So this is accord, a javascript templating interface you can feel confident in.

### Installation

`npm install accord`

### Usage

Although we are planning a CLI interface which will be awesome, right now accord exposes only a javascript API. Since some templating engines are async and others are not, accord keeps things consistent by returning a promise for any compilation task (using when.js). Here's an example in coffeescript:

```
fs = require 'fs'
accord = require 'accord'
stylus = accord.load('jade')

# render a string
jade.render('body\n  .test')
  .done (res) ->
    console.log res
  , (err) ->
    console.error(err)

# or a file
jade.renderFile('./example.jade')
  .done (res) ->
    console.log res
  , (err) ->
    console.error(err)

# or precompile the template (limited support)
# you can also just use jade.precompile('string')
jade.precompileFile('./example.jade')
  .done (fn) ->
    console.log fn.toString()
  , (err) ->
    console.error(err)

```

The `accord.load` method is really the core of the library. It accepts two params, the second optional. The first should be a string, the name of the compiler you want to use. If that language is supported by accord and you have it loaded locally, it will automatically require and adapt it for use. If either of the two conditions above are not met, it will throw you an appropriate error.

If you have a modded version of a compiler or are trying to require it from somewhere else, you can require it yourself and pass that in as the second argument. But be warned that if you have modified the compiler to be breaking from the current stable version, it almost might break the accord adapter.

### Supported Languages

##### HTML
- jade
- ejs
- mustache (hogan)
- handlebars
- haml
- haml-coffee
- dust
- underscore
- swig
- toffee
- markdown

##### CSS
- stylus
- scss
- less

##### Javascript
- coffeescript
- coffeescript-redux
- dogescript
- coco
- typescript

##### Minifiers
- uglify-js
- uglify-css
- uglify-html
- csso

### Languages Supporting Precompile

Accord can also precompile templates into javascript functions for some languages, which is really useful for client-side rendering. Languages with precompile support are listed below. If you try to precompile a language without support for it, you will get an error.

- jade
- ejs
- underscore

We are always looking to add precompile support for more languages, but it can be difficult. Any contributions that help to expand this list are greatly appreciated!

### Adding Languages

Want to add more languages? We have put extra effort into making the adapter pattern structrue understandable and easy to add to and test. Rather than requesting that a language be added, please add a pull request and add it yourself! We are quite responsive and will quickly accept if the implementation is well-tested.

Details on running tests and contributing [can be found here](contributing.md)

### License

Licensed under [MIT](license.md)