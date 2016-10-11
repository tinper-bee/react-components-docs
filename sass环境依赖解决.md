# sass环境依赖

## 安装Ruby
sass依赖Ruby环境，所以需要先安装Ruby
- 下载地址[http://rubyinstaller.org/downloads](http://rubyinstaller.org/downloads)
- 注意事项：安装时，最好勾选Add Ruby executables to your PATH这个选项，添加环境变量。
- 查看ruby是否正确安装，在命令窗口使用ruby -v查看版本号来确认是否正确安装


## 安装gulp-sass
generator-tinper-bee是我们编写组件的脚手架产出工具，它产出的脚手架使用gulp-sass编译sass，
gulp-sass依赖于node-sass，node-sass由于某些网络原因，我们可能无法下载
所以请使用cnpm下载node-sass
```
npm install -g cnpm

cnpm install --save-dev node-sass

```
接着下载gulp-sass
```
cnpm install --save-dev gulp-sass
```



## sass用法
请移步参考：
[http://www.w3cplus.com/sassguide/](http://www.w3cplus.com/sassguide/)
[http://sass-lang.com/documentation/file.SASS_REFERENCE.html](http://sass-lang.com/documentation/file.SASS_REFERENCE.html)
