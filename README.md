# JavaScript

## Table of Contents

  1. [Whitespace](#whitespace)
  1. [Objects](#objects)
  1. [Arrays](#arrays)
  1. [Strings](#strings)
  1. [Functions](#functions)
  1. [Variables](#variables)
  1. [Naming Conventions](#naming-conventions)
  1. [Modules](#modules)
  1. [Classes](#classes)
  1. [Comments](#comments)
  1. [Commas](#commas)
  1. [Semicolons](#semicolons)
  1. [Conditional Expressions & Equality](#conditional-expressions--equality)
  1. [File Structure](#file-structure)

## Whitespace

  - Use two-space indents.

    ```javascript
    // bad
    if (err) {
    ∙∙∙∙throw err;
    }

    // good
    if (err) {
    ∙∙throw err;
    }
    ```

  - Insert one space after the `function` keyword.

    ```javascript
    // bad
    var process = function(job){};

    // good
    var process = function (job) {};
    el.addEventListener(function (event) {});
    ```

  - Insert one space before the leading brace.

    ```javascript
    // bad
    if(active){
      console.log("hello world");
    }

    // good
    if (active) {
      console.log("hello world");
    }

    // bad
    for(var i = 0; i < items.length; i++){
      console.log(items[i]);
    }

    // good
    for (var i = 0; i < items.length; i++) {
      console.log(items[i]);
    }
    ```

  - Pad operators with one space.

    ```javascript
    // bad
    var result=x+5;

    // good
    var result = x + 5;

    // bad
    if (active===true) {
      console.log("active");
    }

    // good
    if (active === true) {
      console.log("active");
    }
    ```

    - Pad blocks with one newline.

    ```javascript
    // bad
    function getResult(id) {
      var result = null;
      if (typeof id === "number") {
        result = fetch(id);
      }


      return result;
    }

    // good
    function getResult(id) {
      var result = null;

      if (typeof id === "number") {
        result = fetch(id);
      }

      return result;
    }
    ```

## Objects

  - Use the literal syntax when creating objects.

    ```javascript
    // bad
    var obj = new Object();

    // good
    var obj = {};
    ```

  - Access properties using dot notation when possible.

    ```javascript
    // bad
    var name = person["name"];

    // good
    var name = person.name;
    var state = attrs["data-state"];
    ```

## Arrays

  - Use the literal syntax when creating arrays.

    ```javascript
    // bad
    var list = new Array();

    // good
    var list = [];
    ```

  - To convert an array-like object into an array, use `Array#slice`.

    ```javascript
    var args = Array.prototype.slice.call(arguments);
    ```

  - To copy an array, use `Array#slice`.

    ```javascript
    var itemsCopy = items.slice();
    ```

## Strings

  - Use double-quotes when creating strings.

    ```javascript
    // bad
    var name = 'Jane Doe';

    // good
    var name = "Jane Doe";
    ```

  - Strings longer than 80 characters should be written over multiple lines using concatenation.

    ```javascript
    // bad
    var message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut ac vehicula erat. Aenean consectetur ligula vel mi dapibus interdum. Quisque id purus tempus, posuere mi a, scelerisque.";

    // bad
    var message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut \
                  ac vehicula erat. Aenean consectetur ligula vel mi dapibus \
                  interdum. Quisque id purus tempus, posuere mi a, scelerisque.";

    // good
    var message = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Ut " +
      "ac vehicula erat. Aenean consectetur ligula vel mi dapibus interdum. " +
      "Quisque id purus tempus, posuere mi a, scelerisque.";
    ```

  - When constructing a string dynamically, use `Array#join`.

## Functions

  - Function expressions:

    ```javascript
    // anonymous function expression
    var logger = function (msg) {
      console.log(msg);
    };

    // named function expression
    var logger = function logger(msg) {
      console.log(msg);
    };

    // immediately invoked function expression
    (function (msg) {
      console.log(msg);
    })("Hello World");
    ```

  - Functions requiring more than four parameters should use an options hash instead.

    ```javascript
    // bad
    function setupRoute(name, action, method, handler, callback) {
      console.log("too complex");
    }

    // good
    function setupRoute(options, callback) {
      console.log("much better");
    }
    ```

  - Functions must not contain blocks nested three levels deep. Functional programming techniques and libraries such as [Lo-Dash](http://lodash.com/) can be very helpful.

    ```javascript
    // bad
    function findAltText(urls) {
      var anchors, html, window;
      var texts = [];

      for (var i = 0; i < urls.length; i++) {
        if (isValidUrl(urls[i])) {
          html = getPage(urls[i]);

          if (html) {
            window = makeWindow(html);
            anchors = getAnchors(window);

            for (var j = 0; j < anchors.length; j++) {
              texts.push(anchors[j].alt);
            }
          }
        }
      }

      return texts;
    }

    // good
    function findAltText(urls) {
      var validUrls = urls.filter(isValidUrl);
      var htmls = _.filter(validUrls.map(getPage), _.isString);
      var windows = htmls.map(makeWindow);
      var anchors = [].concat(windows.map(getAnchors));

      return anchors.map(_.property("alt"));
    }
    ```

## Variables

  - Declare all undefined variables on a single line, and defined variables on their own lines. Variables should be declared alphabetically, when possible.

    ```javascript
    // bad
    var state,
        attrs,
        iterations = 0,
        items = [];

    // good
    var attr, states;
    var items = [];
    var iterations = 0;
    ```

  - Declare all variables at the outermost function scope that they're used in, even if they are undefined.

    ```javascript
    // bad
    function parseResults(results) {
      if (results.length) {
        var parsed = [];
      }
    }

    // good
    function parseResults(results) {
      var parsed;

      if (results.length) {
        parsed = [];
      }
    }
    ```

## Naming Conventions

  - References must be named using descriptive names and sparing abbreviations.

    ```javascript
    // bad
    var t = new Task();
    var drv = Selenium.Driver.create();

    // good
    var task = new Task();
    var driver = Selenium.Driver.create();
    ```

  - Functions should usually be named as verb or verbNoun.

    ```javascript
    // bad
    function file(path) {
      return fs.readFileSync(path);
    }

    // good
    function getFile(path) {
      return fs.readFileSync(path);
    }
    ```

  - Constants must be defined in UPPER_SNAKE_CASE.

    ```javascript
    // bad
    var active = "active";
    var defaultInterval = 2000;

    // good
    var ACTIVE = "active";
    var DEFAULT_INTERVAL = 2000;
    ```

## Classes

  - A basic class should take the following form:

    ```javascript
    // constructor
    function Model(attrs) {
      this.attrs = attrs;
    }

    // public method
    Model.prototype.findById = function (id, callback) {
      var self = this;

      db.find(id, function (err, data) {
        if (err) {
          callback(err);
        } else {
          return self._parseResult(data);
        }
      });
    };

    // private method
    Model.prototype._parseResult = function (result) {
      delete result.id;

      return result;
    };
    ```

  - To inherit another class in browser-based environments:

    ```javascript
    function Model(attrs) {
      this.attrs = attrs;
    }

    Model.prototype = new EventEmitter();
    Model.prototype.constructor = Model;
    ```

  - In Node.js-based environments, use the `util.inherits` function:

    ```javascript
    var EventEmitter = require("events").EventEmitter;
    var util = require("util");

    module.exports = Model;

    function Model(attrs) {
      this.attrs = attrs;
    }

    util.inherits(Model, EventEmitter);
    ```

## Modules

  - Node.js modules typically fall into one of two categories: classes and utilities

  - Classes should take the form of:

    ```javascript
    module.exports = Job;

    var defaults = { type: "job" };

    function Job(options) {
      this.settings = _.defaults(defaults, options);
    }

    Job.prototype.run = function (callback) {
      callback(null);
    };
    ```

  - Utilities should take the form of:

    ```javascript
    exports.flatten = function (list) {
      return true;
    };

    exports.stripUrl = function (str) {
      return true;
    };

    exports.typeOf = function (obj) {
      return true;
    };
    ```

    - Module requirement groups should be separated with a newline by core, third-party, and first-party, sorted alphabetically:

    ```javascript
    var path = require("path");
    var util = require("util");

    var Hapi = require("hapi");
    var program = require("commander");

    var pkg = require("./package.json");
    ```

## Comments

  - Single-line comments must be placed above the subject of their contents and should contain a space after the initial `//`.

    ```javascript
    // bad
    var timeout = 2000; // time until request times out

    // bad
    //time until request times out
    var timeout = 2000;

    // good
    // time until request times out
    var timeout = 2000;
    ```

  - Multi-line comments should use align `*` at the beginning of each line.

    ```javascript
    // bad
    /* Parses results created at time. Please see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date */
    function getTimestamp(item) {
    }

    // bad
    /*
       Parses results created at time. Please see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date 
     */
    function getTimestamp(item) {
    }

    // good
    /*
     * Parses results created at time.
     * Please see: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date
     */
    function getTimestamp(item) {
    }
    ```

## Commas

  - Commas must be placed at the end of a line.

    ```javascript
    // bad
    var settings = {
      interval: 50
    , state: "active"
    , list: []
    };

    // good
    var settings = {
      interval: 50,
      state: "active",
      list: []
    };
    ```

## Semicolons

  - Use them.

    ```javascript
    // bad
    var attr, states
    var items = []
    var parseEach = function (item) {
      return true
    }

    // bad
    var attr, states;
    var items = [];
    var parseEach = function (item) {
      return true;
    };
    ```

## Conditional Expressions & Equality

  - Use `===` and `!==` over `==` and `!=`.
  - Use shortcuts when possible.

    ```javascript
    // bad
    if (str !== "") {
      // ...
    }

    // good
    if (str) {
      // ...
    }

    // bad
    if (items.length > 0) {
      // ...
    }

    // good
    if (items.length) {
      // ...
    }
    ```

## File Structure

  - Use lower_snake_case when naming files.

    ```shell
    # bad
    requestHandler.js
    TestSuite.js

    # good
    request_handler.js
    test_suite.js
    ```

  - Use train-case when naming directories.

    ```shell
    # bad
    image_assets/apple.png
    imageAssets/apple.png

    # good
    image-assets/apple.png
    ```
