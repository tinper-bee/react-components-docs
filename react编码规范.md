# react组件开发规范

要求编码规范，接口定义规范，组件结构自由给予用户充分定制能力。

## 文件命名
- 每一个文件只包含一个组件，每一个基本组件只包含单一功能
- src目录下，如果文件返回是一个类，文件名首字母大写
- 文件js模块统一使用js后缀名
- 测试用例文件名使用.spec.js后缀
- 每一个组件使用一个单独的测试用例文件

## js规范
- 使用es6开发，尽量使用常用的ES6语法，(ES6语法参考)[http://es6.ruanyifeng.com/]
- 使用jsx语法
- 组件仓库命名为小写和“-”连接，如button、button-group
- 组件文件命名使用大驼峰， ComponentDemo
- 带命名空间的组件，如果一个组件包含只有自身使用的子组件，以该组件为命名空间编写组件，例如Table，Table.Head
- 不使用displayName命名
- 自定义属性使用data-
- 使用propTypes进行props类型校验
- 使用defaultProps定义默认参数
- 定义props避开react关键字及保留字，常用的props及state定义可参考下表
- 尽量少或者不使用ref获取和操作dom节点，使用state和prop进行控制dom
- 事件调用使用在元素上onClick调用
- 注意，react和html的表单元素的差异
- 使用es6后，不支持mixin，使用decorator进行扩展，（babel？需要增加解析器）和高阶组件方式扩展。
- 尽量不使用比较大的第三方js库
- 组件方法定义顺序 constructor --> 声明周期方法(componentWillMount,componentDidMount,
componentWillUpdate,componentDidUpdate,componentWillUnmount)
- 尽量多而有用的代码注释，方法用块级注释，结构如下例。
- 有必要需要些组件的销毁方法，比如 定时器，需要用销毁方法销毁定时器
- ...others 没有必要 勿用
- 自身定义的props属性应避免与react的关键字相同




- 代码规范使用   [airbnb规范](https://github.com/airbnb/javascript/tree/master/react)

## 样式规范
- 组件样式使用sass编写，公用样式使用tinper-bee-core包，请阅读[tinper-bee-core文档](https://github.com/tinper-bee/tinper-bee-core)
- 组件样式调用，使用classnames模块，进行样式处理，使用className调用
- 所有组件默认类名命名以`u-``开头
- 组件使用clsPrefix为样式前缀,用户也可在组件上设置自定义的`clsPrefix="yourPre"`
```javascript
const clsPrefix = 'u-select';
const class1 = {
    [`${clsPrefix}-item`]: true,
    [`${clsPrefix}-item-last`]: stepLast,
    [`${clsPrefix}-status-${status}`]: true,
    [`${clsPrefix}-custom`]: icon
  };
const class2 = [`${clsPrefix}-submit`, `${clsPrefix}-item`];

const classString = classNames('hide', class1, class2);

```
- 可提供多种颜色的组件，在写scss文件时，颜色设置需提出公用的minxin方法例如Alert组件中设置多种颜色： @alert-styles-variant

## 通用组件接口规范

|参数|说明|类型|默认值|
|---|----|---|------|
|size|尺寸|string|medium|
|color|颜色|string|''|
|shape|形状|string|''|
|disabled|是否禁用(`disabled` 或 `true` `false`)|bool|false|
|className|增加额外的类名|string|''|
|htmlType|html dom 的 type 属性|string|''|
|style|内联样式|object|''|
|clsPrefix|自定义样式前缀|string|''|

对于方法的传递，外部使用onClick传入事件，内部使用handleClick进行接收使用

## 国际化


当你的组件包含一些文字时，在src目录下，创建`i18n.js`文件，写下对应的hash值。内容如下：
```
module.exports = {
    'zh-cn': {
        'ok': '确定',
        'cancel': '取消',
        'isee': '知道了'
    },
    'en-us': {
        'ok': 'ok',
        'cancel': 'cancel',
        'isee': 'ok'
    }
}
```
组件内这么使用:
```
import i18n from './i18n';
import React from 'react';

Example.defaultProps = {
    locale: 'zh-cn'
};

class Example extends React.Component {
    constructor(props) {
        super(props);
    }


    render() {
        const {locale} = this.props;
        const locale = i18n[locale];

        const buttons= [
            <Button>
                {locale['ok']}
            </Button>,
            <Button>
                {locale['cancel']}
            </Button>
        ];
        return (
            <div>
            { buttons }
            </div>
            )
    }
}


```



## 基本代码结构

```javascript
//引入依赖
import React from 'react';
import ReactDOM from'react-dom';
import classnames from 'classnames';

//定义prop检验
const propTypes = {
//每一个props都要写注释
}

//定义默认参数
const defaultProps = {

}

/**
 * 定义组件
 */
class Button extends React.Component {
	constructor (props) {
		super(props);
		//定义state
		this.state = {
    //每一个state要写注释
		}
		// 事先声明方法绑定
		this.MyEvent = this.MyEvent.bind(this);
	}

    //自定义函数方法，及注释
      MyEvent () {

      }
    //组件生命周期方法


	render () {
		return (
			// <div onClick={this.MyEvent}></div>
		)
	}
}

Button.propTypes = propTypes;
Button.defaultProps = defaultProps;

export default Button;
```

### 常用npm包

##### [keyCode](https://github.com/timoxley/keycode)


##### [warning](https://github.com/BerkeleyTrue/warning)

```
var warning = require('warning');

var ShouldBeTrue = false;

warning(
  ShouldBeTrue,
  'This thing should be true but you set to false. No soup for you!'
);
```

##### [bee-animate](https://github.com/tinper-bee/bee-animate)

##### [bee-overlay](https://github.com/tinper-bee/bee-overlay)

##### [dom-helpers (3.0.0)](https://github.com/react-bootstrap/dom-helpers)


参考链接
https://github.com/react-component/react-component.github.io/blob/master/docs/zh-cn/code-style/js.md
