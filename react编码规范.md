# react组件开发规范

要求编码规范，接口定义规范，组件结构自由给予用户充分定制能力。

## 文件命名
- 每一个文件只包含一个组件，每一个基本组件只包含单一功能
- src目录下，如果文件返回是一个类，文件名首字母大写
- 文件js模块统一使用js后缀名
- React组件文件使用大驼峰命名方式，其他文件一律使用小写命名，如果需要使用中划线分割。

## js规范
- 使用es6开发，尽量使用常用的ES6语法，[ES6语法参考](http://es6.ruanyifeng.com/)
- 使用jsx语法

### 格式

- 标签自闭合

```
//bad

<Button></Button>

//good
<Button />
```

- 自闭合换行
```
//bad

 <Button color="primary" />

//good

<Button
    color="primary"
/>
```

-

### 组件命名

- 组件文件命名使用大驼峰， ComponentDemo
- 带命名空间的组件，如果一个组件包含只有自身使用的子组件，以该组件为命名空间编写组件，例如Table，Table.Head

### 组件声明

- 使用es6的class来声明组件，而不是使用`createClass`,在React V16版本，`createClass`已经废弃

```
// bad
const Button = React.createClass({
  // ...
  render() {
    return <button>{this.state.hello}</button>;
  }
});

// good
class Button extends React.Component {
  // ...
  render() {
    return <button>{this.state.hello}</button>;
  }

```

- 对于不包含`state`和`refs`的组件，建议写成纯函数组件，而且建议使用function关键字声明

```
//bad

class Button extends React.Component{
    render() {
        return (
            <Button>{ this.props.text }</Button>
        )
    }
}

//bad

const Button = ({ text }) => (
    <button>{ text }</button>
 )

//good

function Button ({ text }) {
    return (
        <button>{ text }</button>
    )
}
```

- 对于只有简单数据类型的`props`和`state`的组件，建议使用`PureComponent`来声明组件

```

//bad

class Button extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            disabled: false
        }
    }
    render() {
        return (
            <Button
                disabled={this.state.disabled}>
            { this.props.text }
            </Button>
        )
    }
}

//good

class Button extends React.PureComponent{
    constructor(props){
        super(props);
        this.state = {
            disabled: false
        }
    }
    render() {
        return (
            <Button
                disabled={this.state.disabled}>
            { this.props.text }
            </Button>
        )
    }
}

```

### 组件内部声明

- 使用propTypes进行props类型校验

```
import PropTypes from 'prop-types';

const propTypes = {
    disabled: PropTypes.bool
}

class Button extends React.Component{}

Button.propTypes = propTypes;

```
- 使用defaultProps定义默认参数

```
import PropTypes from 'prop-types';

const defaultProps = {
    disabled: false
}

class Button extends React.Component{}

Button.defaultProps = defaultProps;

```

- 不使用displayName命名

displayName属性用于组件调试时输出显示，JSX自动设置该值，可以理解为调试时显示的组件名。

```
// bad
export default React.createClass({
  displayName: 'Button',
  // stuff goes here
});

// good
export default class Button extends React.Component {
}
```


### 属性定义

- 定义props避开react关键字及保留字，常用的props及state定义可参考下表

- `props`和`state`使用驼峰命名。

- 不直接修改`state`

```
//bad

class Button extends React.Component{
    constructor(props){
       super(props);
       this.state = {
            disabled: false
       }
    }
    handleClick = () => {
        this.state.disabled = true;
        this.setState({
           disabled:  this.state.disabled
        })

    }

    render() {
        return (
            <Button
                disabled={this.state.disabled}>
            { this.props.text }
            </Button>
        )
    }
}

//good

class Button extends React.Component{
    constructor(props){
       super(props);
       this.state = {
            disabled: false
       }
    }
    handleClick = () => {
        let disabled = ture;
        this.setState({
           disabled
        })

    }

    render() {
        return (
            <Button
                disabled={this.state.disabled}>
            { this.props.text }
            </Button>
        )
    }
}

```

- 自定义HTML属性使用data-

```
class Button extends React.Component{

    render() {
        return (
            <Button
                data-name="submit-button">
            { this.props.text }
            </Button>
        )
    }
}


```

- 可以使用es6的这种`...props`语法获取剩下所有属性,但是如果没有必要，尽量不要使用

```
class Button extends React.Component{

    render() {
    let {onClick, disabled, ...props} = this.props;
        return (
            <Button
                { ...props }>
            { this.props.text }
            </Button>
        )
    }
}

```

### ref

- 通过`ref`可以取到组件原生dom对象。使用传入函数function方式来定义`ref`，不使用字符串定义`ref`

```
//bad


class Button extends React.Component{
    constructor(props){
            super(props);
    }
    componentDidMount() {
        this.refs.buttonRef.focus();
    }

    render() {
        return (
            <Button
                ref="buttonRef">
            { this.props.text }
            </Button>
        )
    }
}

//good

class Button extends React.Component{
    constructor(props){
        super(props);
        this.buttonRef = {};
    }
    componentDidMount() {
        this.buttonRef.focus();
    }

    render() {
        return (
            <Button
                ref={(el) => this.buttonRef = el;}>
            { this.props.text }
            </Button>
        )
    }
}

```

- 尽量少或者不使用ref获取和操作dom节点，使用state和prop进行控制dom

### 组件声明周期函数

- 组件方法定义顺序
    - constructor
    - getChildContext
    - componentWillMount
    - componentDidMount
    - componentWillReceiveProps
    - shouldComponentUpdate
    - componentWillUpdate
    - componentDidUpdate
    - componentWillUnmount

- 在`componentDidMount`生命周期内获取初始数据

```
class Button extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            data: ''
        }
    }
    componentDidMount() {
        axios.get('http://baidu.com/button-name')
            .then((res) => {
                this.setState({
                    data：res.data
                })
            })
    }

    render() {
        return (
            <Button>
            { this.state.data }
            </Button>
        )
    }
}

```

- 在组件`componentWillUnmount`卸载生命周期中，进行清除定时器、卸载组件绑定的自定义事件等。

```
class Button extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            data: ''
        }
        this.timer = null;
    }
    componentDidMount() {
        this.timer = setInterval(this.getData, 1000);
    }

    getData = () => {
            axios.get('http://baidu.com/button-name')
                .then((res) => {
                    this.setState({
                        data：res.data
                    })
                })
    }

    componentWillUnmount() {
        window.clearInterval(this.timer);
    }

    render() {
        return (
            <Button>
            { this.state.data }
            </Button>
        )
    }
}
```

- 使用箭头函数定义自定义的组件内方法

```
//bad
class Button extends React.Component{
    handleClick(e) {

    }
    render() {
        return (
            <Button onClick={this.handleClick.bind(this)}>
            { this.state.data }
            </Button>
        )
    }
}


//good

class Button extends React.Component{
    handleClick = (e) => {

    }
    render() {
        return (
            <Button onClick={this.handleClick}>
            { this.state.data }
            </Button>
        )
    }
}
```

### Mixin

- 使用es6后，不支持mixin，使用decorator进行扩展和高阶组件方式扩展。





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
