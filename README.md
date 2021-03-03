# B2B 运营中台

B2B 运营中台

### 依赖安装

```
npm install
```

### 启动开发服务

```
npm run dev
```

### 构建，env: test | prod

```
npm run build:[env]
```

### 视图列表

### 组件列表

### 接口列表

## 注意

1. views 入口里给 vue 类添加了原型方法\$open，用来打开标签卡页面，也可以调用路由的`push`或`replace`
2. 第一期开发者只需关注 views 入口，项目迁移成本低
3. 全局注册了几个使用频次极高的组件
4. 配置了组件库按需加载
5. 独立 axios 的基础配置
6. 支持使用[vue-cli](https://cli.vuejs.org/zh/guide/cli-service.html#%E4%BD%BF%E7%94%A8%E5%91%BD%E4%BB%A4)管理本地项目和依赖分析

## Layout 组件

main 入口使用 Layout 组件，该组件处理系统子项目间交互，标签卡操作

## 环境配置

1. vue.config.js 可根据环境`process.env.BUILD_ENV`配置对应环境的变量
2. 脚手架默认提供请求路径的配置`FETCH_BASEURL`

## views 目录规范

1. 视图内的目录层级和菜单层级保持一致，假设菜单层级为`订单/订单列表`，那么 views 里的目录结构应该是`/order/orderList/index.vue`
2. 样式不写在组件内，单独目录单独文件
3. 图片单独目录

```node
views
└─order
│   └── orderList
│   │     │ index.vue
│   │     │ styles
│   │     │    └── index.scss
│   │     │ images
│   │     │    └── xx.png
```

4. 使用以下设置以避免小驼峰命名在 windows 系统下修改文件名无法不识别的问题

```
git config core.ignorecase false
git config --global core.ignorecase false // 全局设置
```

### 强制的代码风格标准

用 git commit 提交代码之前，利用 pre-commit git 钩子，实现代码规范检测（eslint、standard 规范），符合规范之后才可以提交到 git 仓库。这样在团队合作开发时，可以统一代码风格，如果某些同志代码不符合规范，是无法进行提交代码的。

1. 规范 doc
   [standard 规范](https://github.com/standard/standard/blob/master/docs/README-zhcn.md)
   [eslint 规范](https://github.com/eslint/eslint)

2. git 钩子
   [git 钩子](https://github.com/typicode/husky)

3. 若想绕过代码检测强制提交

```
git add . && git commit --no-verify -m "代码规范强制提交测试"
```

###  Mock数据
新增命令便宜快速切换mock数据和开发环境
```
 npm run dev:mock
```

### 路由缓存
开启标签卡级别的路由缓存，关闭标签卡则从缓存中清除

特殊情况：

如果打开多个同一个动态路由的标签卡，关掉其中一个，不会清除缓存，直到关闭所有同一个动态路由的标签卡，才会清除缓存

如何加入路由缓存?

1. routerPath去掉动态路由部分，比如`/:id`
2. view组件的name属性设置为`view`+`routerPath.replace(/\//g, '.')`

