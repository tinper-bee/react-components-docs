# react组件开发规范

## 文件命名
- 每一个文件只包含一个组件，每一个基本组件只包含单一功能
- src目录下，如果文件返回是一个类，文件名首字母大写
- 文件js模块统一使用js后缀名
- 测试用例文件名使用.spec.js后缀
- 每一个组件使用一个单独的测试用例文件

## js规范
- 使用es6开发，尽量使用常用的ES6语法，(ES6语法参考)[http://es6.ruanyifeng.com/]
- 使用jsx语法
- 组件命名使用大驼峰， ComponentDemo
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


- 代码规范使用   [airbnb规范](https://github.com/airbnb/javascript/tree/master/react)

## 样式规范
- 组件样式使用sass编写，公用样式使用tinper-bee-core包，请阅读[tinper-bee-core文档](https://github.com/tinper-bee/tinper-bee-core)
- 组件样式调用，使用classnames模块，进行样式处理，使用className调用
- 组件内部使用clsPrefix为样式前缀
```javascript
const clsPrefix = 'u-select';
const class1 = {
    [`${clsPrefix}-item`]: true,
    [`${clsPrefix}-item-last`]: stepLast,
    [`${clsPrefix}-status-${status}`]: true,
    [`${clsPrefix}-custom`]: icon,
    [className]: !!className,
  };
const class2 = [`${clsPrefix}-submit`, `${clsPrefix}-item`];

const classString = classNames('hide', class1, class2);

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

//定义组件
class Button extends React.Component {
	constructor (props) {
		super(props);
		//定义state
		this.state = {
    //每一个state要写注释
		}
	}
    //自定义函数方法，及注释
    //组件生命周期方法

	render () {
		return (

		)
	}
}

Button.propTypes = propTypes;
Button.defaultProps = defaultProps;

export default Button;
```


参考链接
https://github.com/react-component/react-component.github.io/blob/master/docs/zh-cn/code-style/js.md
