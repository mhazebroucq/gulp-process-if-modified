# gulp-process-only-modified-files

[![Build Status](https://travis-ci.org/wlarch/gulp-process-if-modified.svg?branch=master)](https://travis-ci.org/wlarch/gulp-process-if-modified) ![NPM](https://img.shields.io/npm/l/gulp-process-if-modified)

> This gulp plugin will passthrough only modified source files since last build.

_Inspired by [gulp-process-if-modified](https://github.com/wlarch/gulp-process-if-modified)_

## Install

```
$ npm install --save gulp-process-if-modified
```

## Usage

```js
var gulp = require('gulp');
var processIfModified = require('gulp-process-only-modified-files');
var sass = require('gulp-sass');
var rename = require("gulp-rename");

// Styles example task
gulp.task(config.path + '-styles', () =>{

    var files = [
        'public/css/styles.scss',
        'public/css/custom.scss',
        'public/css/header.scss'
        'public/css/footer.scss'
    ];

    var css_build_path = 'public/build/css/';

    return gulp.src(files)
        .pipe(processIfModified({ cacheFilename: "styles" }))
        .pipe(sass().on('error', sass.logError))
        .pipe(rename('styles.min.css'))
        .pipe(gulp.dest(css_build_path));
});
```

## API

### processIfModified({options})

#### `cacheFilename`
* `string`
* Default = `./cache/.cache-default.json`

  Cache filename for specific task. The name provided here will be prefixed with `.cache-`. Example : `special_task` as cacheFilename will create the following file in cache folder : `./cache/.cache-special_task.json`

#### `cacheLife`
* `int`
* Default = `1814400`

  Cache keys lifetime in seconds (default 3 weeks).

#### `basePath`
* `string`
* Default = `undefined`

  Allows you to set relative path that will be used for storing paths (keys) in the `cache`.

# Issues

* Be careful not to have multiple processes accessing the same cache file. In fact, it is sugested that each gulp task has it's own cache file by using the `cacheFilename` option above.

# Attribution

Code based on Alex Gorbatchev plugin [gulp-changed-in-place](https://github.com/alexgorbatchev/gulp-changed-in-place)

# License

The MIT License (MIT)

Copyright (c) 2015 Alex Gorbatchev

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
