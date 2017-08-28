### Demo文档生成机制

### 目录接口

* 目录位置：demo／demolist／Demo*.js(\*为数字)

### 格式：

```js

/**
 *
 * @title 选择日期
 * @description 以「日期」为基本单位，基础的日期选择控件
 */

import React, { Component } from 'react';
import {Con, Row, Col } from 'bee-layout';
import DatePicker from '../../src';

import zhCN from 'rc-calendar/lib/locale/zh_CN';
import enUS from 'rc-calendar/lib/locale/en_US';



const format = 'YYYY-MM-DD';

const dateInputPlaceholder = '选择日期';


function onSelect(d) {
    console.log(d)
}


function onChange(d) {
    console.log(d)
}


class Demo1 extends Component {
    render() {

        return (
            <div>
                <Row>
                    <Col md={12}>
                        <DatePicker

                            format={format}

                            onSelect={onSelect}

                            onChange={onChange}

                            locale={zhCN}

                            placeholder = {dateInputPlaceholder}

                        />
                    </Col>
                </Row>
            </div>
        )
    }
}

export default  Demo1;


```

### 加入标题和描述信息

*  @title （文字标题） @description （组件的描述文件）

### 组件的引入

```js
import DatePicker from '../../src';

```

* '../../src'在文档中会被替换成'tinper-bee'的引入方式：

```js
import DatePicker from 'tinper-bee';

```

### 组件的运行

* demo组件的定义 

```js

class Demo(*) extends Component 

```

* demo组件的运行，需要定义export

```js

export default  Demo();

```
