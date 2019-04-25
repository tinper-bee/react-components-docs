> 在[官网Icon组件示例](http://bee.tinper.org/bee-icon#bee-icon)中列举了tinper-bee的所有字体图标，那么当我们在开发过程中，有新增的字体要添加进去的时候该如何下手呢，或许这篇blog会对你有所帮助

### 前面的
- 关于字体图标，tinper-bee组件库默认加载cdn的地址，如果你的项目是私有化部署，不能访问外网资源的话，可以查阅[这篇文章](https://github.com/iuap-design/blog/issues/318)
- 关于字体文件，总的包括demo的html和css文件、iconfont的css、js以及各种字体文件，demo是使用说明，iconfont文件是使用这个图标库所必须的文件，可根据使用的具体方式引用相应文件

![image](https://user-images.githubusercontent.com/33412781/51782221-c1e30080-215f-11e9-9e4a-6377a0b5d6c4.png)

- tinper-bee-core是组件库的核心样式及公用方法库，新增的字体文件也需要在这里备一份

## iconfont更新步骤
### 1. 更新tinper-bee-core的图标文件
- 用新的字体文件替换以下tinper-bee-core/scss目录下的文件，包括：
    - iconfont.eot  
    - iconfont.js
    - iconfont.woff 
    - iconfont.ttf  
    - iconfont.svg  

- 在新字体文件的iconfont.css中找到待增加的图标，复制添加到tinper-bee-core/util-iconfont.css对应的地方，如下：     
![image](https://user-images.githubusercontent.com/33412781/51783818-9d485200-217a-11e9-9852-fea18937330c.png)

- npm publish发布新版本

### 2. 更新CDN资源  

== 图标字体要确认验证后再更新，不然影响面会较大。线上图标字体cdn资源更新得在晚上的时候进行，并且需要对之前的版本进行备份，以防出现异常可以快速回滚。==

> OSS的资源路径：iuap-design-cdn/static/iconfont  

### 3. 修改bee-icon组件
- npm i tinper-bee-core安装最新版本的bee-core
- 更新src/Icon.scss    
![image](https://user-images.githubusercontent.com/33412781/51783876-adacfc80-217b-11e9-8b47-33961dcec4bd.png)  

- 更新demolist/Demo1.js    
![image](https://user-images.githubusercontent.com/33412781/51783885-d1704280-217b-11e9-81a2-870eb78dde45.png)

- 验证并发布新版本
```
npm publish
```
> 注：先发tinper-bee-core，再发bee-icon，否则图标会显示不出来


### 总结解决步骤
1. 更新tinper-bee-core并发版
2. 更新CDN资源
3. 更新bee-icon并发版

之后就可以愉快地使用bee-icon字体图标了
