iview 是一套基于 Vue.js UI 组件库

#### 安装

```javascript
npm install iview --save
```

#### 使用

引入iview
一般在 webpack 入口页面 main.js 中如下配置：

```Vue
import Vue from 'vue';
import VueRouter from 'vue-router';
import App from 'components/app.vue';
import Routers from './router.js';
import iView from 'iview';
import 'iview/dist/styles/iview.css';

Vue.use(VueRouter);
Vue.use(iView);

// The routing configuration
const RouterConfig = {
    routes: Routers
};
const router = new VueRouter(RouterConfig);

new Vue({
    el: '#app',
    router: router,
    render: h => h(App)
});
```

### 组件使用规范

使用:prop传递数据格式为 数字、布尔值或函数时，必须使用v-bind(兼容String除外，具体看组件文档)，比如：

```Vue
错误用法:
<Page :current="1" :total="100"></Page>

正确用法:
<Page current="1" total="100"></Page>
```

在非 template/render 模式下（例如使用 CDN 引用时），组件名要分隔，例如 DatePicker 必须要写成 date-picker。

以下组件，在非 template/render 模式下，需要加前缀 i-：

- Button: i-button
- Col: i-col
- Table: i-table
- Input: i-input
- Form: i-form
- Menu: i-menu
- Select: i-select
- Option: i-option
- Progress: i-progress
- Time: i-time


以下组件，在所有模式下，必须加前缀 i-，除非使用 [iview-loader](https://www.iviewui.com/docs/guide/iview-loader)：

- Switch: i-switch
- Circle: i-circle


### 具体用法可参考[iview](https://www.iviewui.com/docs/guide/install)官方文档
