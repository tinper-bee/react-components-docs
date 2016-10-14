#React组件测试流程和规范

### 测试依赖
- mocha
- chai
- jsdom
- enzyme

### 试用Enzyme测试
- shallow Rendering 测试虚拟dom
- DOM Rendering 测试真实dom

#### shallow
浅渲染，将组件渲染成虚拟dom对象，但是只渲染第一层，不渲染所有子组件
```javascript
import React from 'react';
import {shallow, mount, render} from 'enzyme';
import {expect} from 'chai';
import Button from '../src/index';

describe('Enzyme Shallow', function () {
  it('Button should be exist', function () {
    let button = shallow(<Button/>);
    expect(button.hasClass('u-button')).to.equal(true);
  });
});
```
find只支持简单选择器
- .find('.classname')
- .find('#id')
- .find('tagname')
- .find('tag.class')
- .find('displayname')
- .find(constructor)

#### render
render将组件渲染成静态HTML字符串（通过cheerio解析库解析），可以分析HTML代码结构。
```javascript
import {render} from 'enzyme';

describe('Enzyme Render', function () {
  it('Todo item should not have todo-done class', function () {
    let app = render(<App/>);
    expect(app.find('.todo-done').length).to.equal(0);
  });
});
```
#### mount
mount用于将组件加载为真实DOM
```javascript
import {mount} from 'enzyme';

describe('Enzyme Mount', function () {
  it('Delete Todo', function () {
    let app = mount(<App/>);
    let todoLength = app.find('li').length;
    app.find('button.delete').at(0).simulate('click');
    expect(app.find('li').length).to.equal(todoLength - 1);
  });
});
```
`at`返回指定位置的子组件，`simulate`在组件上触发某种行为，第一个参数为事件，第二个参数为传入的参数

#### Enzyme API
- .get(index)：返回指定位置的子组件的DOM节点
- .at(index)：返回指定位置的子组件
- .first()：返回第一个子组件
- .last()：返回最后一个子组件
- .type()：返回当前组件的类型
- .text()：返回当前组件的文本内容
- .html()：返回当前组件的HTML代码形式
- .props()：返回根组件的所有属性
- .prop(key)：返回根组件的指定属性
- .state([key])：返回根组件的状态
- .setState(nextState)：设置根组件的状态
- .setProps(nextProps)：设置根组件的属性
