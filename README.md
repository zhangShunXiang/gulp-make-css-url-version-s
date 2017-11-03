## gulp-make-css-url-version-tdw



a plugin for gulp.js to replace version for images in css files,the version should be file's md5 or time stamp;

## Installation

```bash
npm install gulp-make-css-url-version-tdw
```

## Usage

```js
var makeUrlVer = require('gulp-make-css-url-version-tdw');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(makeUrlVer())
        .pipe(gulp.dest('dist'))
});
```

## Options

useDate :make version with time stamp

```js
var makeUrlVer = require('gulp-make-css-url-version-tdw');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(makeUrlVer({useDate:true}))  //修改后格式：03395445409(时间拼接精确到毫秒)  原格式：yy-mm-dd
        .pipe(gulp.dest('dist'))
});
```

assetsDir: specify the public directory for correct MD5 calculation in some specific cases

```js
var makeUrlVer = require('gulp-make-css-url-version-tdw');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(makeUrlVer({
            assetsDir: __dirname + '/public'
        }))
        .pipe(gulp.dest('dist'))
});
```

## Example

### before: index.css

```css
/* loading */
.i-loading{width:32px;height:32px;background:url(../images/loading.gif) no-repeat;}    
```

### after: index.css

```css
/* loading */
原来 ：
.i-loading{width:32px;height:32px;background:url(../images/loading.gif?v=Je0sUcMH0mhJPW
dZdpHzXg%3D%3D) no-repeat}
```
###为了节省CSS文件大小只截取生成MD5的前8位
```
修改后 ：
.i-loading{width:32px;height:32px;background:url(../images/loading.gif?v=Je0sUcMH)  
```


#备注:这个包由 gulp-make-css-url-version 修改如有权限问题请联系我 17482174@qq.com
