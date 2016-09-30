# react组件开发规范
## 语言要求
- 使用es6开发
- 使用jsx语法
- 组件命名使用大驼峰， ComponentDemo
- 带命名空间的组件，如果一个组件包含只有自身使用的子组件，以该组件为命名空间编写组件，例如Table，Table.Head
- 不使用displayName命名
- 每一个文件只包含一个组件，每一个基本组件只包含单一功能
- 使用js为扩展名
- 组件样式调用，使用classnames模块，进行样式处理，使用className调用
- 自定义属性使用data-
- 使用propTypes进行props类型校验
- 使用defaultProps定义默认参数
- 使用getInitialState初始化状态对象
- 尽量少或者不使用ref获取和操作dom节点，使用state和prop进行控制dom
- 事件调用使用在元素上onClick调用
- 注意，react和html的表单元素的差异
- 使用es6后，不支持mixin，使用decorator进行扩展，（babel？需要增加解析器）和高阶组件方式扩展。
- 代码规范使用   [airbnb规范](https://github.com/airbnb/javascript/tree/master/react)

## 基本代码结构

```javascript
//引入依赖
let React = require('react');
let ReactDOM = require('react-dom');
let classnames = require('classnames');

//定义prop检验
const propTypes = {

}

//定义默认参数
const defaultProps = {

}

//定义组件
class Button extends React.Component {
	constructor (props) {
		super(props);
		//定义state
		this.state = {

		}
	}
    //自定义内容

	render () {
		return (

		)
	}
}

Button.propTypes = propTypes;
Button.defaultProps = defaultProps;

module.exports = Button;
```
