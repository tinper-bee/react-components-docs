# 编写tinper-bee标准组件

#### 环境依赖
- 需要安装node 4.0版本及以上, npm版本最好3.0以上
- (sass环境依赖)[]

### 一、生成组件脚手架
#### 1、下载
```
npm install -g yo generator-tinper-bee
```

#### 2、生成组件脚手架
下面以创建button组件为例
```
mkdir button
cd button
yo tinper-bee --port=8000 --author=yonyou
```
API介绍
| 参数        | 说明          | 默认值  |
| ------------- |:-------------:| -----:|
| port      | 开发时服务监听端口 | 8000 |
| author      | 作者名字      |   空字符串 |
| beeVersion | 版本号     |    0.0.1 |
| pkgName | 包名      |    bee-组件名 |
| repoUrl | 仓库地址      |    https://github.com/tinper-bee/ + 包名|

默认发布的包名为bee-组件名

#### 3、开发指南
##### 目录结构

```
-demo
 -ButtonDemo.js
 -ButtonDemo.scss
 -index.js
-src
 -Button.js
 -Button.scss
 -index.js
-test
 -setup.js
 -index.test.js
-.eslintignore
-.eslintrc
-.npmignore
-gulpfile.js
-HISTORY.md
-index.html
-package.json
-README.md
-webpack.dev.js
```
##### 目录说明

- 在 src 目录中写源程序代码。
- 在 demo 目录下写使用用例。
- 在 test 目录下写 测试用例。
- build目录产出打包组件。
- 代码规范参考 [代码规范]()。
- 根目录 中的 html 不可修改，通过 js 中的 jsx 渲染页面，通过 require css 引入 css。
- 开发中用到其他公共库，通过 `npm install --save` 以及 `npm install --save-dev` 来安装


##### 开发调试

- 在项目根目录执行 `npm install` 安装必要模块
- 在项目根目录执行 `npm run dev` 查看demo
- 在项目根目录执行 `gulp` 产出build目录代码
- 在项目根目录执行 `gulp publish` 进行组件发布,master分支为正式发布版，release分支为开发分支

##### 浏览器支持版本

- ie8, ie8+, chrome, firefox 最新版
- 可适当渐进降级，如 css 动画可以不支持 ie8
