# tinper-bee-core 整体文档
tinper-bee组件库的核心样式及公用方法库

## 核心样式
放在scss文件夹下，由index.scss统一导出
包括
- 重置浏览器样式
- 全局样式设置
- 图标样式
- 波纹效果、阴影样式、文本及字体样式
- 主辅色及常用颜色设置

## 工具方法库

### set-global
- 设置body字体及颜色
- 设置图表间距
- 设置显隐u-visible u-not-visible
- 设置边框u-border-top...



### set-normalize
- 重置css样式

### set-resets
- 选择时删除文本阴影，及设置默认选中颜色
- html5标签的跨浏览器样式适配

### util-iconfont
- 图标设定

### util-ripple
- 波动动画设定

### util-shadow
- 阴影样式设定

### util-utilities
- 垂直对齐样式
- display样式
- 文本换行，浅色
- 文本位置
- 文本大小写
- 字体粗度
- 字体大小
- 清除浮动及左右浮动
- 显示隐藏
- 宽高常用预设样式
- 常用margin，padding预设样式
- visible，hidden的适配预设

### minxin-colors
- 调色板
- [文档链接](http://tinper.org/dist/neoui/global/color.html)

### minxin-mixins
- 该文件定义了很多可复用的功能模块，比如说border-radius和box-shadow等组合样式。

### minxin-palette
- 设置根据minxin-colors的颜色生成背景颜色和字体颜色
- 在组件的Demo 示例中可直接添加该文件中的定义className。

### minxin-themeColors
- 设置主色和辅色等tinper-bee 中最常用的通用变量，即主题定制时可供用户配置的样式变量

### minxin-variables
- 默认变量
    - 默认字体
    - 默认颜色
    - 字体大小和粗细
    - 波纹效果
    - 贝塞尔曲线动画
    - 阴影
    - 常用z-index值设定
    - UI组件的预设



### js方法

#### keyCode对象

引入方法：

```
import keyCode from 'tinper-bee-core/lib/keyCode';

//或者

import { keyCode } from 'tinper-bee-core';

```

方法：

- isTextModifyingKeyEvent 验证是否是特殊按键或组合按键

```
handleKeyDown = (e) => {
if(keyCode.isTextModifyingKeyEvent(e)){
 //一些操作
}
}
...

<Input onKeyDown={this.handleKeyDown} />
```

- isCharacterKey 验证是否是文本键
```
handleKeyDown = (e) => {
if(keyCode.isCharacterKey(e)){
 //一些操作
}
}
...

<Input onKeyDown={this.handleKeyDown} />
```

#### toArray 将数组安全的转换为react element 数组

#### splitComponentProps 通过父组件的propTypes拆分分别传给父子组件的props


```
const propTypes = {
    color: PropTypes.string,
    size: PropTypes.string
}
class ParentClass extends React.Component{
    render() {
        let props = this.props;
        let [parentProps, childProps] = splitComponentProps(props);

        return (
            <div>
                <ChildrenClass {...childProps} />
            </div>
        )
    }
}

ParentClass.propTypes = propTypes;

```

#### createChainedFunction 创建链式调用方法


#### contains 检验是否包含

