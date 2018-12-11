# quant-template
---
> 用来适配量投前端框架，快速生成常用模板，简化开发工作得到snippets

我们会持续的更新这个插件，集成多种的模板来方便开发。

Supported languages (file extensions)

> * JavaScript (.js)
> * JavaScript React (.jsx)

## Basic Methods
| Prefix  | Method                                              |
| ------: | --------------------------------------------------- |
| `quant default react→`  | `基本页面模板`                      |
| `quant default models→`  | `基本models模板`                                   |
| `quant services models→`  | `含有增删改查服务的models模板`                                   |
| `quant services api→`  | `生成services下的基础api对象`                                   |

## React Components

### quant default react

```javascript
import React, { Component } from 'react'
import { connect } from 'dva';
import { Card, Form } from 'quant-ui';
import PageHeaderLayout from '@/layouts/PageHeaderLayout'
class FileName extends Component {
    render() {
        return (
            <PageHeaderLayout  >
                <Card className='hover-shadow'>
                    demo
                </Card>
            </PageHeaderLayout>)
    }
}
export default connect(({ snippets, loading }) => {
    const { } = snippets
    return {

    }
})(
    Form.create()(FileName)
)
```
## Models

### quant default models
```
import { POST } from '@/utils/request';
import api from '@/services/api.js';
import { message } from "quant-ui"
export default {
    namespace: 'FileName',
    state: {

    },
    effects: {

        
    },
    reducers: {
        save(state, { payload }) {
            return {
                ...state, ...payload
            };
        },
    },
    subscriptions: {

    },
};
```
### quant 弹出框
```
import React, { Component } from 'react'
import { connect } from 'dva';
import { Form, MoveModal, Card, Input, Row, Col } from "quant-ui";
import { gutter, formLayout, colLayout } from '@/utils/utils';
const FormItem = Form.Item;
class Index extends Component {
    componentWillReceiveProps = (nextProps) => {
        if (this.props.addVisible !== nextProps.addVisible) {
            this.props.form.resetFields();
        }
    }
    //modal取消事件
    onCancel = () => {
        const { dispatch } = this.props;
        dispatch({
            type: "template/save",
            payload: {
                addVisible: false
            }
        })
    }
    //modal确定事件
    onOk = () => {
        const { dispatch, isUpdate, currentData, form: { validateFields } } = this.props;
        validateFields((error, values) => {
            if (!!error) return;
            if (isUpdate) { //修改
                dispatch({
                    type: "template/update",
                    payload: { ...currentData, ...values }
                })
            } else {          //新增
                dispatch({
                    type: "template/add",
                    payload: values
                })
            }
        })
    }
    render() {
        const { loading, addVisible, form: { getFieldDecorator }, currentData, isUpdate } = this.props;
        return (
            <MoveModal
                visible={addVisible}
                title={isUpdate ? "标题修改" : "标题新增"}
                onCancel={this.onCancel}
                onOk={this.onOk}
                maskClosable={false}
                confirmLoading={loading}
                width="50%"
            >
                <Card className="hover-shadow" style={{ width: '100%' }}>
                    <Form >
                        <Row gutter={gutter}>
                            <Col {...colLayout}>
                                <FormItem label={"字段1"}
                                    {...formLayout}
                                >
                                    {getFieldDecorator('id', {
                                        initialValue: currentData.id,
                                        rules: [{ required: true, message: '请选择' }],
                                    })(
                                        <Input />
                                    )}
                                </FormItem>
                            </Col>
                            <Col {...colLayout}>
                                <FormItem label={"字段2"}
                                    {...formLayout}
                                >
                                    {getFieldDecorator('k2', {
                                        initialValue: currentData.k2,
                                        rules: [{ required: true, message: '请选择' }],
                                    })(
                                        <Input />
                                    )}
                                </FormItem>
                            </Col>
                        </Row>
                    </Form>
                </Card>
            </MoveModal>
        )
    }
}
export default connect(({ template, loading }) => {
    const { addVisible, isUpdate, currentData = {} } = template
    return {
        addVisible: true,
        isUpdate,
        currentData,
        loading: !!loading.effects['template/update'] || !!loading.effects['template/add']
    }
})(
    Form.create()(Index)
)
```
### quant services models
```
import { POST } from "@/utils/request";
import api from "@/services/api.js";
import { message } from "quant-ui";
export default {
    namespace: "FileName",
    state: {

    },
    effects: {
        //查询所有
        *findAll({ payload }, { call, put }) {
            const { errorCode, data } = yield call(POST, api.FileName.findAll);
            if (errorCode == 0) {

            }
        },
        //条件查询
        *findByQuery({ payload }, { call, put }) {
            const { errorCode, data } = yield call(POST, api.FileName.findByQuery, [payload]);
            if (errorCode == 0) {

            }
        },
        //更新、修改
        *update({ payload }, { call, put }) {
            const { errorCode, data } = yield call(POST, api.FileName.update, [payload]);
            if (errorCode == 0) {
                message.success("修改成功！");
            }
        },
        //删除
        *delete({ payload }, { call, put }) {
            const { errorCode, data } = yield call(POST, api.FileName.delete, [payload]);
            if (errorCode == 0) {
                message.success("删除成功！");
            }
        },
        //添加
        *add({ payload }, { call, put }) {
            const { errorCode, data } = yield call(POST, api.FileName.add, [payload]);
            if (errorCode == 0) {
                message.success("添加成功！");
            }
        },
    },
    reducers: {
        save(state, { payload }) {
            return {
                ...state, ...payload
            };
        },
    },
    subscriptions: {

    },
};
```

## API
### quant services api
```
"namespace":{
   findAll: basUrl + "/service",       //查询所有接口
   findByQuery: basUrl + "/service",   //条件查询接口
   update: basUrl + "/service",        //更新、修改接口
   delete: basUrl + "/service",        //删除接口
   add: basUrl + "/service",           //添加接口
},
```
