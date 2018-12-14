# 快速上手 dva-js

#### 安装 dva-cli

`npm install dva-cli -g`

#### 创建新的 dva 应用
1. `dva new dva-quickstart` 搭建好的 dva 开发环境，包含 dva-quickstart 初始化目录

2. `cd quickstart` 

3. `npm start` 或者 `yarn start` 启动服务

4. `http://localhost:8000` 访问地址

#### 使用 antd 组件（可选）

1. `npm install antd babel-plugin-import --save` <br>
`babel-plugin-import` 用来按需加载 ant 的脚本和样式

2. 编辑 `.webpackrc`,使 `babel-plugin-import` 插件生效<br>
```
{
+  "extraBabelPlugins": [
+    ["import", { "libraryName": "antd", "libraryDirectory": "es", "style": "css" }]
+  ]
}
```

#### 开始写代码吧

1. 定义路由组件<br>
路由应该写在 `src/routes/` 下面，写完 `export` 出去并添加
路由信息到路由表 `src/router.js` 中

2. 定义 UI 组件<br>
UI 组件应该写在 `src/components/` 下面

3. 定义 model<br>
`dva` 通过 `model` 的概念把一个领域的模型管理起来，包含
同步更新 `state` 的 `reducers`，处理异步逻辑的 `effects`，订阅数据源的 `subscriptions`

`model` 中:
-  `namespace` 表示在全局 `state` 上的 `key`
- `state` 是初始值
- `reducers` 等同于 `redux` 里的 `reducer`，接收 `action`，同步更新 `state`

定义完的 `model` 需要在 `src/index.js` 中载入
`app.model(require('./models/products').default);`

4. 把 `model` 和 `component` 串联起来<br>
为组件添加 `connnet`
```
const xxxComponent = ({ dispatch, xxxNamespace }) => {
  return (
    <div>
    ...
    </div>
  )
}
export default connet(({ xxxNamespace})=>{
  xxxNamespace
})(xxxComponent)
```

5. 为 `dva` 应用添加初始化数据<br>
编辑 `src/index.js`，修改如：
```
const app = dva({
  initialState: {
    xxxNamespace: [ // 定义对应的 model 的初始化 state 对象，这里是个数组
      ....
    ]
  }
})
```
