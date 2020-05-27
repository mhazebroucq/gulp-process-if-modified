# gulp-process-if-modified

> This gulp plugin will passthrough source files if they have been modified since last build.

_Inspired by [gulp-changed](https://github.com/sindresorhus/gulp-changed) and [gulp-changed-in-place](https://github.com/alexgorbatchev/gulp-changed-in-place)_

## Avoid long running Gulp builds

Do not waste time during your build process when there is no reason to. This plugin will process all files in gulp.src() if at least one file was changed. This plugin uses the features of [node-file-cache](https://www.npmjs.com/package/node-file-cache) to keep track of the assets SHA1 hashed content in a cache.json file.

## Alternatives depending on use case

[gulp-changed](https://github.com/sindresorhus/gulp-changed) : checks against build files, for example ES5 files generated by Babel.js from the source ES6 files.

[gulp-changed-in-place](https://github.com/alexgorbatchev/gulp-changed-in-place) : monitors source files, ES6 files for example. This allows you to do things like apply source formatting or linting *only* to changed files while you are working on them.

---

## Install

```
$ npm install --save gulp-process-if-modified
```

## Usage

```js
var gulp = require('gulp');
var processIfModified = require('gulp-process-if-modified');
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
        .pipe(processIfModified())
        .pipe(sass().on('error', sass.logError))
        .pipe(rename('styles.min.css'))
        .pipe(gulp.dest(css_build_path));
});
```

## API

### processIfModified({options})


#### `cacheLife`
* `int`
* Default = `1814400`

  Lifetime in seconds (default 3 weeks)  `{ key: value }` format for all the files that is shared between all runs. Value will be hash or modification time, depending on the `howToDetermineDifference` option.

#### `basePath`
* `string`
* Default = `undefined`

  Allows you to set relative path that will be used for storing paths in the `cache`.

# Attribution

Code based on Alex Gorbatchev plugin [gulp-changed-in-place](https://github.com/alexgorbatchev/gulp-changed-in-place)

# Version History

[Changelog](https://github.com/wlarch/gulp-process-if-modified/releases)

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