---
title: Hexo博客使用gulp压缩静态资源进行优化
author: 少年
tags:
  - Hexo
  - gulp
categories: 博客篇
abbrlink: gulp
date: 2021-01-06 12:00:00
---

Gulp.js 是一个自动化构建工具，开发者可以使用它在项目开发过程中自动执行常见任务。Gulp.js 是基于 Node.js 构建的，利用 Node.js 流的威力，你可以快速构建项目并减少频繁的 IO 操作。Gulp.js 源文件和你用来定义任务的 Gulp 文件都是通过 JavaScript（或者 CoffeeScript ）源码来实现的。

### Hexo博客使用gulp压缩静态资源

#### 全局安装gulp

```bash
npm install gulp -g
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/gulp1.png)

```bash
# 查看版本
gulp -v
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/gulp2.png)

#### 安装gulp插件

**在站点根目录下安装**

以下步骤同上：

```bash
npm install gulp --save
npm install gulp-minify-css --save
npm install gulp-uglify --save
npm install gulp-htmlmin --save
npm install gulp-htmlclean --save
npm install gulp-imagemin --save
# 解决【Gulp打包问题】 GulpUglifyError: unable to minify JavaScript
# 解决 gulp-uglify 压缩JavaScript 不兼容 es5 语法的问题
npm install babel-core@6.26.3 --save
npm install gulp-babel@7.0.1 --save
npm install babel-preset-es2015@6.24.1 --save
# gulp-babel 取消严格模式方法("use strict")
npm install babel-plugin-transform-remove-strict-mode --save
```

问题：如果安装`gulp-imagemin`错误请执行以下语句
`sudo npm i gulp-imagemin --unsafe-perms`

#### 创建`gulpfile.js`文件

在 Hexo 站点下新建`gulpfile.js`文件，文件内容如下：

```javascript
var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
var babel = require('gulp-babel');

// 压缩css文件
gulp.task('minify-css', function (done) {
    return gulp.src('./public/**/*.css')
        .pipe(minifycss())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩html文件
gulp.task('minify-html', function (done) {
    return gulp.src('./public/**/*.html')
        .pipe(htmlclean())
        .pipe(htmlmin({
            removeComments: true,
            minifyJS: true,
            minifyCSS: true,
            minifyURLs: true,
        }))
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩js文件
gulp.task('minify-js', function (done) {
    return gulp.src(['./public/**/*.js', '!./public/**/*.min.js'])
        .pipe(babel({
            //将ES6代码转译为可执行的JS代码
            presets: ['es2015'] // es5检查机制
        }))
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
    done();
});

// 压缩 public/images 目录内图片(Version<3)
// gulp.task('minify-images', function () {
//     gulp.src('./public/images/**/*.*')
//         .pipe(imagemin({
//             optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
//             progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
//             interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
//             multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
//         }))
//         .pipe(gulp.dest('./public/images'));
// });

// 压缩 public/images 目录内图片(Version>3)
gulp.task('minify-images', function (done) {
    gulp.src('./public/images/**/*.*')
        .pipe(imagemin([
            imagemin.gifsicle({interlaced: true}),
            imagemin.jpegtran({progressive: true}),
            imagemin.optipng({optimizationLevel: 5}),
            imagemin.svgo({
                plugins: [
                    {removeViewBox: true},
                    {cleanupIDs: false}
                ]
            })
        ]))
        .pipe(gulp.dest('./public/images'));
    done();
});

//4.0以前的写法 
//gulp.task('default', [
//  'minify-html', 'minify-css', 'minify-js', 'minify-images'
//]);
//4.0以后的写法
// 执行 gulp 命令时执行的任务
gulp.task('default', gulp.series(gulp.parallel('minify-html', 'minify-css', 'minify-js', 'minify-images')), function () {
    console.log("----------gulp Finished----------");
    // Do something after a, b, and c are finished.
});
```

#### 创建`.babelrc`文件

在 Hexo 站点下新建`.babelrc`文件，文件内容如下：

```javascript
{
    'presets': ['es2015'],
    "plugins": ["transform-remove-strict-mode"]
}
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/hg.png)

#### 静态资源压缩

生成博文时执行 `hexo g && gulp` 就会根据 `gulpfile.js` 中的配置，对 `public` 目录中的静态资源文件进行压缩。

```shell
hexo g && gulp
```

本篇参照码云思伟 / zhousiwei