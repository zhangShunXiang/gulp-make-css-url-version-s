## gulp-make-css-url-version-s


<p>修改了 gulp-make-css-url-version 增加版本号的方式：</p>
<p>原来的日期模式是"yy-mm-dd" 修改成以毫秒为序列号</p>
<p>原来的MD5模式引用字段过长引起CSS文件过大，现在截取前8位为版本号</p>
<p>解决图片url以域名 （"http://", "https://", "//"）为前缀导致找不到文件路径而无法修改版本号问题；</p>
<p>可过滤不需要修改版本号的路径</p>

## 安装

```bash
npm install gulp-make-css-url-version-s
```

## 使用
默认MD5模式
```js
var makeUrlVer = require('gulp-make-css-url-version-s');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(makeUrlVer())
        .pipe(gulp.dest('dist'))
});
```

## 配置

<p>使用日期模式：</p>

```js
var makeUrlVer = require('gulp-make-css-url-version-s');

gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
    //原格式：yy-mm-dd 修改后格式：201711061728(时间拼接精确到毫秒)  
        .pipe(makeUrlVer({useDate:true}))  
        .pipe(gulp.dest('dist'))
});
```
##### 域名路径配置
```js
var makeUrlVer = require('gulp-make-css-url-version-s');
gulp.task('stylesheets', function() {
    gulp.src('css/*.css')
        .pipe(cssver({
            /*域名替换，路径必须以'/'结束 ;
            / 例如" http://abc.com/images/logo.png" 用'../'替换后你可以处理的路径是'../images/logo.png' */
            domainName:'../',  
            //过滤不需要加版本号的域名 
            exincludeDomain:["//abc.cn/","http://abc.com/"]}))
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
.logo{background:url(//js.abc.com/loading.png) ;}    
   
```

### after: index.css

```css
/* loading */
.i-loading{background:url(../images/loading.gif?v=Je0sUcMH)}
.logo{background:url(//js.abc.com/logo.png?v=Je0sUcMH) ;}    
```
 

 