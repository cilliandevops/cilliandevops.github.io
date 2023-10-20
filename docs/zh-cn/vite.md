# 创建一个vite项目
## 时间：2023年10月19日

## 官网教程

https://cn.vitejs.dev/guide/#scaffolding-your-first-vite-project

```js
npm create vite@latest my-vue-app -- --template vue
```

这里从js项目开始

首先更新依赖，ncu -u




```js
@vitejs/plugin-vue  ^4.2.3  →  ^4.4.0
 vite                ^4.4.5  →  ^4.5.0
 ```

```js
{
  "name": "aiops-vite",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "vue": "^3.3.4"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.4.0",
    "vite": "^4.5.0"
  }
}
```

**vue版本**

https://cn.vuejs.org/about/releases.html


当前 Vue 的最新稳定版本是 v3.3.4。


## 安装elmentplus和icon

```
  http://element-plus.org/zh-CN/guide/installation.html

  pnpm install element-plus

  pnpm install @element-plus/icons-vue
```

## 安装vuerouter

pnpm install vue-router@latest

anzhuan
安装完成后：
```js
{
  "name": "aiops-vite",
  "private": true,
  "version": "0.0.1-beta",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "@element-plus/icons-vue": "^2.1.0",
    "element-plus": "^2.4.1",
    "vue": "^3.3.4",
    "vue-router": "^4.2.5"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^4.4.0",
    "vite": "^4.5.0"
  }
}
```
## 安装windicss

```pnpm i -D vite-plugin-windicss windicss```


## 引入配置

**vite.config.js**

```js
import WindiCSS from 'vite-plugin-windicss'

export default {
  plugins: [
    WindiCSS(),
  ],
}
```

**main.js**

```js
import { createApp } from 'vue'
import './style.css'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

import * as ElementPlusIconsVue from '@element-plus/icons-vue'

const app = createApp(App)
for (const [key, component] of Object.entries(ElementPlusIconsVue)) {
app.component(key, component)
}

import 'virtual:windi.css'


app.use(ElementPlus)
app.mount('#app')
```

