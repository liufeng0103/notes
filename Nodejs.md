##Jade
###安装
npm install -g jade

###模板生成html
jade index.jade
参数:
1. -P 生成格式化的html,默认一行不方便阅读
2. -w 开启监视模式，每次更改模版,html文件都会自动编译

##Gulp
###安装
cnpm install gulp-jshint gulp-concat gulp-rename gulp-uglify gulp-jade gulp-minify --save-dev