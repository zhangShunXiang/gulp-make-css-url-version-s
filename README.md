## gulp-make-css-url-version-s


优化了 gulp-make-css-url-version 增加版本号的方式：
原来的日期模式是"yy-mm-dd" 修改成以毫秒为序列号
原来的MD5模式引用字段过长引起CSS文件过大，现在截取前8位为版本号

## Installation

```bash
npm install gulp-make-css-url-version-s
```

## Usage

```js
var makeUrlVer = require('gulp-make-css-url-version-s');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(makeUrlVer())
        .pipe(gulp.dest('dist'))
});
```

## Options

useDate :make version with time stamp

```js
var makeUrlVer = require('gulp-make-css-url-version-s');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
    //原格式：yy-mm-dd 修改后格式：03395445409(时间拼接精确到毫秒)  
        .pipe(makeUrlVer({useDate:true}))  
        .pipe(gulp.dest('dist'))
});
```

assetsDir: specify the public directory for correct MD5 calculation in some specific cases

```js
var makeUrlVer = require('gulp-make-css-url-version-s');

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
.i-loading{background:url(../images/loading.gif) ;}    
```

### after: index.css

```css
/* loading */
原来 ：
.i-loading{background:url(../images/loading.gif?v=Je0sUcMH0mhJPWdZdpHzXg%3D%3D)}
```
###为了节省CSS文件大小只截取生成MD5的前8位
```css
修改后 ：
.i-loading{background:url(../images/loading.gif?v=Je0sUcMH)  }
```


备注:这个包由 gulp-make-css-url-version 修改如有权限问题请联系我 17482174@qq.com
