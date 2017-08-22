# 编写tinper-bee标准组件

#### 环境依赖
- 需要安装node 4.0版本及以上, npm版本最好3.0以上
- [sass环境依赖](https://github.com/tinper-bee/react-components-docs/blob/master/sass%E7%8E%AF%E5%A2%83%E4%BE%9D%E8%B5%96%E8%A7%A3%E5%86%B3.md)

### 一、下载tinper-bee开发工具
#### 1、全局安装开发工具

如果是用友内部员工，请使用用友内部npm镜像和下载工具ynpm-tool。

```
npm install -g ynpm-tool
ynpm install
```

也可以使用npm。

```
npm install -g bee-tools
```
使用版本号，来验证是否下载成功。
```
bee-tools --version
```
因为npm下载较慢，所以请使用cnpm或者切换为淘宝源来下载

- 使用cnpm

```
npm install -g cnpm
cnpm install -g bee-tools
```
- 切换淘宝源

```
npm --registry https://registry.npm.taobao.org install -g bee-tools
```



#### 2、生成组件脚手架
下面以创建button组件为例

```
bee-tools create bee-button --author yonyou --port 8000 --tbVersion 0.1.0 --repoUrl https://github.com/tinper-bee/bee-button
```

API介绍

| 参数        | 说明         | 默认值  |
|:------------ |:-------------:| -----:|
| port      | 开发时服务监听端口 | 8000 |
| author      | 作者名字      |   空字符串 |
| tbVersion | 版本号     |    0.0.1 |
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
 -Button.test.js
-.gitignore
-.npmignore
-HISTORY.md
-index.html
-package.json
-README.md
```
##### 目录说明

- 在 src 目录中写源程序代码。
- 在 demo 目录下写使用用例。
- 在 test 目录下写 测试用例。
- build目录产出打包组件。
- 代码规范参考 [代码规范](https://github.com/tinper-bee/react-components-docs/blob/master/react%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83.md)。
- 根目录 中的 html 不可修改，通过 js 中的 jsx 渲染页面，通过 require css 引入 css。
- 开发中用到其他公共库，通过 `npm install --save` 以及 `npm install --save-dev` 来安装

##### 代码书写规范
[react编码规范](https://github.com/tinper-bee/react-components-docs/blob/master/react%E7%BC%96%E7%A0%81%E8%A7%84%E8%8C%83.md)
[react组件测试流程和规范](https://github.com/tinper-bee/react-components-docs/blob/master/react%E7%BB%84%E4%BB%B6%E6%B5%8B%E8%AF%95%E6%B5%81%E7%A8%8B%E5%92%8C%E8%A7%84%E8%8C%83.md)

##### 开发调试

- 在项目根目录执行 `npm install` 安装必要模块
- 在项目根目录执行 `npm run dev` 查看demo，进行调试
- 在项目根目录执行 `npm run build` 产出build目录代码
- 在项目根目录执行 `npm run lint` 执行lint检查
- 在项目根目录执行 `npm run test` 执行测试用例
- 在项目根目录执行 `npm run coveralls` 执行测试覆盖率
- 在项目根目录执行 `npm run chrome` 在chrome执行测试用例
- 在项目根目录执行 `npm run browsers` 在本机多浏览器执行测试用例
- 在项目根目录执行 `npm run pub` 进行组件发布,master分支为正式发布版，release分支为开发分支

##### 浏览器支持版本

- ie9, ie9+, chrome, firefox 最新版
