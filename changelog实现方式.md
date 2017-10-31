#changelog实现方式

##1、Commitizen

> Commitizen是一个格式化commit message的工具。

    npm install -g commitizen
    
    commitizen init cz-conventional-changelog --save --save-exact

>此操作会修改package.json文件。
>![](media/15093486333182/15094378630612.jpg)

git cz替换git commit命令

![](media/15093486333182/15094380852015.jpg)


##2、conventional-changelog-cli
>就是生成 Change log 的工具。

    npm install -g conventional-changelog-cli
    cd my-project
    conventional-changelog -p angular -i CHANGELOG.md -s
    
>现在是配置在package.json中   
![](media/15093486333182/15094388347044.jpg)



##3、validate-commit-msg
>用于检查 Node 项目的 Commit message 是否符合格式。

1. 拷贝下面这个JS文件，[JS](https://github.com/conventional-changelog-archived-repos/validate-commit-msg/blob/master/index.js)放入你的代码库。文件名可以取为validate-commit-msg.js。

2. 把这个脚本加入 Git 的 hook。下面是在package.json里面使用 ghooks，把这个脚本加为commit-msg时运行。     
    ![](media/15093486333182/15094386539876.jpg)

3. 每次git commit的时候，这个脚本就会自动检查 Commit message 是否合格。如果不合格，就会报错。
eg:
![](media/15093486333182/15094385275825.jpg)

##4、命令截图
![](media/15093486333182/15094390880861.jpg)

##5、效果截图
![](media/15093486333182/15094393010120.jpg)


##辅助工具

> conventional-github-releaser：通过提交记录生成 github release 中的变更描述

### 把md文件转html,且提交到github上
一下两工具分别解决，是把README.md编译成html，并带有左侧目录功能，然后推送到git pages上

https://github.com/tschaub/gh-pages


1. 依赖i5ting_ztree_toc插件，生成目录。
2. git pages是免费的http静态服务器。
3. rub 环境。

https://github.com/rowoot/gulp-gh-pages【为gulp 的插件】

生成以后的效果如下
http://i5ting.github.io/docto-example/#101




## commit message 格式

commit message 主要包括三个部分：Header、Body、Footer。

除 Header 外，Body、Footer均为非必填项。

### Header

Header 要求单行，其中包括 <type>、<scope>、<subject>三个部分。

### type

用来标识 commit 的类型，总共有以下 11 个标识：

	feat: 添加了一个新功能
	fix: 修复了一个 bug
	docs: 文档发生修改
	style: 不影响代码运行的更改（空格，格式，缺少分号等）
	refactor: 重构代码且不引进新的功能或修复 bug
	perf: 代码优化
	test: 添加或修改测试用例
	build: 构建工具或外部依赖的更改（npm，webpack，gulp等）
	ci: 更改项目级的配置文件或脚本
	chore: 除上述之外的修改
	revert: 撤销改动先前的提交

### scope

用来标识改动所影响的范围，视项目而定。

### subject

改动的简短描述，不超过 50 字符长度。

### Body

本次 commit 的详细描述。

### Footer

主要用于两种情况：

1. 重大的不兼容改动: 用于给出改动说明及解决方案。
2. 关联 issues: 用于关闭相应 issues。


> 特别注意：使用 revert 标识撤销 commit 时，subject 应为所撤销的 commit 的 message， Body 应包含 所撤销的 commit 的 hash。
格式如下：


