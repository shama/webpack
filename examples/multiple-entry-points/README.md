# pageA.js

``` javascript
var common = require("./common");
require(["./shared"], function(shared) {
	shared("This is page A");
});
```

# pageB.js

``` javascript
var common = require("./common");
require.ensure(["./shared"], function(require) {
	var shared = require("./shared");
	shared("This is page B");
});
```

# webpack.config.js

``` javascript
var path = require("path");
var CommonsChunkPlugin = require("../../lib/optimize/CommonsChunkPlugin");
module.exports = {
	entry: {
		pageA: "./pageA",
		pageB: "./pageB"
	},
	output: {
		path: path.join(__dirname, "js"),
		filename: "[name].bundle.js",
		chunkFilename: "[id].chunk.js"
	},
	plugins: [
		new CommonsChunkPlugin("commons.js")
	]
}
```

# pageA.html

``` html
<html>
	<head></head>
	<body>
		<script src="js/commons.js" charset="utf-8"></script>
		<script src="js/pageA.bundle.js" charset="utf-8"></script>
	</body>
</html>
```

# js/commons.js

``` javascript
/******/ (function(modules) { // webpackBootstrap
/******/ 	
/******/ 	// The module cache
/******/ 	var installedModules = {};
/******/ 	
/******/ 	// object to store loaded and loading chunks
/******/ 	// "0" means "already loaded"
/******/ 	// Array means "loading", array contains callbacks
/******/ 	var installedChunks = {
/******/ 		1:0
/******/ 	};
/******/ 	
/******/ 	// The require function
/******/ 	function __webpack_require__(moduleId) {
/******/ 		// Check if module is in cache
/******/ 		if(installedModules[moduleId])
/******/ 			return installedModules[moduleId].exports;
/******/ 		
/******/ 		// Create a new module (and put it into the cache)
/******/ 		var module = installedModules[moduleId] = {
/******/ 			exports: {},
/******/ 			id: moduleId,
/******/ 			loaded: false
/******/ 		};
/******/ 		
/******/ 		// Execute the module function
/******/ 		modules[moduleId].call(module.exports, module, module.exports, __webpack_require__);
/******/ 		
/******/ 		// Flag the module as loaded
/******/ 		module.loaded = true;
/******/ 		
/******/ 		// Return the exports of the module
/******/ 		return module.exports;
/******/ 	}
/******/ 	
/******/ 	// This file contains only the entry chunk.
/******/ 	// The chunk loading function for additional chunks
/******/ 	__webpack_require__.e = function requireEnsure(chunkId, callback) {
/******/ 		// "0" is the signal for "already loaded"
/******/ 		if(installedChunks[chunkId] === 0)
/******/ 			return callback.call(null, __webpack_require__);
/******/ 		
/******/ 		// an array means "currently loading".
/******/ 		if(installedChunks[chunkId] !== undefined) {
/******/ 			installedChunks[chunkId].push(callback);
/******/ 		} else {
/******/ 			// start chunk loading
/******/ 			installedChunks[chunkId] = [callback];
/******/ 			var head = document.getElementsByTagName('head')[0];
/******/ 			var script = document.createElement('script');
/******/ 			script.type = 'text/javascript';
/******/ 			script.charset = 'utf-8';
/******/ 			script.src = __webpack_require__.p + "" + chunkId + ".chunk.js";
/******/ 			head.appendChild(script);
/******/ 		}
/******/ 	};
/******/ 	
/******/ 	// expose the modules object (__webpack_modules__)
/******/ 	__webpack_require__.m = modules;
/******/ 	
/******/ 	// expose the module cache
/******/ 	__webpack_require__.c = installedModules;
/******/ 	
/******/ 	// __webpack_public_path__
/******/ 	__webpack_require__.p = "js/";
/******/ 	
/******/ 	// install a JSONP callback for chunk loading
/******/ 	var parentJsonpFunction = window["webpackJsonp"];
/******/ 	window["webpackJsonp"] = function webpackJsonpCallback(chunkIds, moreModules) {
/******/ 		// add "moreModules" to the modules object,
/******/ 		// then flag all "chunkIds" as loaded and fire callback
/******/ 		var moduleId, chunkId, i = 0, callbacks = [];
/******/ 		for(;i < chunkIds.length; i++) {
/******/ 			chunkId = chunkIds[i];
/******/ 			if(installedChunks[chunkId])
/******/ 				callbacks.push.apply(callbacks, installedChunks[chunkId]);
/******/ 			installedChunks[chunkId] = 0;
/******/ 		}
/******/ 		for(moduleId in moreModules) {
/******/ 			modules[moduleId] = moreModules[moduleId];
/******/ 		}
/******/ 		if(parentJsonpFunction) parentJsonpFunction(chunkIds, moreModules);
/******/ 		while(callbacks.length)
/******/ 			callbacks.shift().call(null, __webpack_require__);
/******/ 		if(moreModules[0]) {
/******/ 			installedModules[0] = 0;
/******/ 			__webpack_require__(0);
/******/ 		}
/******/ 	};
/******/ })
/************************************************************************/
/******/ ([
/* 0 */,
/* 1 */
/*!*******************!*\
  !*** ./common.js ***!
  \*******************/
/***/ function(module, exports, __webpack_require__) {

	module.exports = "Common";

/***/ }
/******/ ])
```

# js/pageA.bundle.js

``` javascript
webpackJsonp([3],[
/* 0 */
/*!******************!*\
  !*** ./pageA.js ***!
  \******************/
/***/ function(module, exports, __webpack_require__) {

	var common = __webpack_require__(/*! ./common */ 1);
	__webpack_require__.e/* require */(0/* duplicate */, function(__webpack_require__) { var __WEBPACK_AMD_REQUIRE_ARRAY__ = [__webpack_require__(/*! ./shared */ 2)]; (function(shared) {
		shared("This is page A");
	}.apply(null, __WEBPACK_AMD_REQUIRE_ARRAY__));});

/***/ }
])
```

# js/pageB.bundle.js

``` javascript
webpackJsonp([2],[
/* 0 */
/*!******************!*\
  !*** ./pageB.js ***!
  \******************/
/***/ function(module, exports, __webpack_require__) {

	var common = __webpack_require__(/*! ./common */ 1);
	__webpack_require__.e/*nsure*/(0, function(require) {
		var shared = __webpack_require__(/*! ./shared */ 2);
		shared("This is page B");
	});

/***/ }
])
```

# js/0.chunk.js

``` javascript
webpackJsonp([0],{

/***/ 2:
/*!*******************!*\
  !*** ./shared.js ***!
  \*******************/
/***/ function(module, exports, __webpack_require__) {

	var common = __webpack_require__(/*! ./common */ 1);
	module.exports = function(msg) {
		console.log(msg);
	};

/***/ }

})
```

# Info

## Uncompressed

```
Hash: 790c5174bb64d68297d6
Version: webpack 1.1.0
Time: 64ms
          Asset  Size  Chunks             Chunk Names
     0.chunk.js   286       0  [emitted]             
     commons.js  3801       1  [emitted]  commons.js 
pageB.bundle.js   366       2  [emitted]  pageB      
pageA.bundle.js   485       3  [emitted]  pageA      
chunk    {0} 0.chunk.js 91 {2} {3} [rendered]
    > [0] ./pageB.js 2:0-5:2
    > duplicate [0] ./pageA.js 2:0-4:2
    [2] ./shared.js 91 {0} [built]
        amd require ./shared [0] ./pageA.js 2:0-4:2
        require.ensure item ./shared [0] ./pageB.js 2:0-5:2
        cjs require ./shared [0] ./pageB.js 3:14-33
chunk    {1} commons.js (commons.js) 26 [rendered]
    [1] ./common.js 26 {1} [built]
        cjs require ./common [0] ./pageA.js 1:13-32
        cjs require ./common [0] ./pageB.js 1:13-32
        cjs require ./common [2] ./shared.js 1:13-32
chunk    {2} pageB.bundle.js (pageB) 152 {1} [rendered]
    > pageB [0] ./pageB.js 
    [0] ./pageB.js 152 {2} [built]
chunk    {3} pageA.bundle.js (pageA) 108 {1} [rendered]
    > pageA [0] ./pageA.js 
    [0] ./pageA.js 108 {3} [built]
```

## Minimized (uglify-js, no zip)

```
Hash: af178c6be99868cf9cda
Version: webpack 1.1.0
Time: 189ms
          Asset  Size  Chunks             Chunk Names
     0.chunk.js    82       0  [emitted]             
     commons.js   727       1  [emitted]  commons.js 
pageB.bundle.js    92       2  [emitted]  pageB      
pageA.bundle.js   124       3  [emitted]  pageA      
chunk    {0} 0.chunk.js 91 {2} {3} [rendered]
    > [0] ./pageB.js 2:0-5:2
    > duplicate [0] ./pageA.js 2:0-4:2
    [2] ./shared.js 91 {0} [built]
        amd require ./shared [0] ./pageA.js 2:0-4:2
        require.ensure item ./shared [0] ./pageB.js 2:0-5:2
        cjs require ./shared [0] ./pageB.js 3:14-33
chunk    {1} commons.js (commons.js) 26 [rendered]
    [1] ./common.js 26 {1} [built]
        cjs require ./common [0] ./pageA.js 1:13-32
        cjs require ./common [0] ./pageB.js 1:13-32
        cjs require ./common [2] ./shared.js 1:13-32
chunk    {2} pageB.bundle.js (pageB) 152 {1} [rendered]
    > pageB [0] ./pageB.js 
    [0] ./pageB.js 152 {2} [built]
chunk    {3} pageA.bundle.js (pageA) 108 {1} [rendered]
    > pageA [0] ./pageA.js 
    [0] ./pageA.js 108 {3} [built]

WARNING in 0.chunk.js from UglifyJs
Side effects in initialization of unused variable common [./shared.js:1,0]

WARNING in pageB.bundle.js from UglifyJs
Dropping unused function argument require [./pageB.js:2,0]
Side effects in initialization of unused variable common [./pageB.js:1,0]

WARNING in pageA.bundle.js from UglifyJs
Side effects in initialization of unused variable common [./pageA.js:1,0]
```
