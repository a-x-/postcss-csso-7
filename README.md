[![NPM version](https://img.shields.io/npm/v/postcss-csso.svg)](https://www.npmjs.com/package/postcss-csso)
[![Build Status](https://travis-ci.org/lahmatiy/postcss-csso.svg?branch=master)](https://travis-ci.org/lahmatiy/postcss-csso)

# postcss-csso-7

[PostCSS](https://github.com/postcss/postcss) plugin to minify CSS using [CSSO](https://github.com/css/csso) (a CSS minifier with structural optimizations).

Under the hood, the plugin converts `PostCSS` AST into `CSSO`'s AST, optimises it and converts back. The plugin uses input `PostCSS`'s AST nodes (or their clones) on back convertation, so the shape of original `PostCSS`'s nodes persists the same after compression in most cases (e.g. properties added by other plugins isn't lost). This approach makes it possible to achieve a great performance and generate source maps correctly.

The performance of `postcss-csso` is approximately the same as `CSSO` has itself (see `CSSO` numbers in [minifiers comparison table](https://goalsmashers.github.io/css-minification-benchmark/)).

> If you have any difficulties with the output of this plugin, please use the [CSSO tracker](https://github.com/css/csso/issues).

## Install

```
npm install postcss-csso-7
```

## Usage

```js
var postcss = require('postcss');
var csso = require('postcss-csso-7');

postcss([
    csso
])
    .process('.a { color: #FF0000; } .b { color: rgba(255, 0, 0, 1) }')
    .then(function(result) {
        console.log(result.css);
        // .a,.b{color:red}
    });
```

Plugin takes the same [options](https://github.com/css/csso#compressast-options) as `compress()` method of CSSO with no exception.

```js
postcss([
    csso({ restructure: false })
])
    .process('.a { color: #FF0000; } .b { color: rgba(255, 0, 0, 1) }')
    .then(function(result) {
        console.log(result.css);
        // .a{color:red}.b{color:red}
    });
```

## License

MIT
