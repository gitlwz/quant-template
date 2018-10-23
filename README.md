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
