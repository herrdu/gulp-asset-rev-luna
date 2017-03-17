
## gulp-asset-rev-luna

a plugin for gulp.js to replace file's name by adding content hash

## Installation

```bash
npm install gulp-asset-rev-luna
```

## Usage

```js
var gulp = require('gulp');
var assetRev = require('gulp-asset-rev-luna');

gulp.task('rev',function() {
    gulp.src("./test/test.html")
        .pipe(assetRev())
        .pipe(gulp.dest('./'));
});
```

## Options

### hashLen: length of hash version string
Type: `Number` default: 7

### verConnecter: version connect char
Type: `String` default: '-'

### rootPath: it should be assigned when the asset's path is an absolute path
Type: `String` default: ""

### verStr: use custom version string 
Type: `String` 

## Example

```js
var gulp = require('gulp');
var assetRev = require('./index.js');

gulp.task('rev',function() {
    gulp.src("./test/test.html")
        .pipe(assetRev())
        .pipe(gulp.dest('./test/test.html'));
});

OR

gulp.task('rev', function() {
    var app_path = 'webapp';
    gulp.src([app_path + '/**/*.jsp'])
        .pipe(assetRev({
            reg: /<%=request.getContextPath\(\)\s?%>/,
            prePath:'<%=request.getContextPath() %>',
            rootPath: app_path,
            verConnecter: '?v=',
        }))
        .pipe(gulp.dest(app_path + '/'));
});

gulp.task('default',['rev']);
```

### before: test.html
```html
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <title></title>
    <link rel="stylesheet" href="./styles/test.css" type="text/css" />
</head>
<body>
    <div>
        <img src="./images/test.png" />
    </div>
    <script src="./scripts/test.js" type="text/javascript"></script>
</body>
</html>
```
### after: test.html

```html
<html lang="en">
<head>
    <meta charset="utf-8"/>
    <title></title>
    <link rel="stylesheet" href="./styles/test.css?v=0ede2cf" type="text/css" />
</head>
<body>
    <div>
        <img src="./images/test.png?v=25cf2b4" />
    </div>
    <script src="./scripts/test.js?v=8ced4e6" type="text/javascript"></script>
</body>
</html>
```



