# weapp-workflow(v0.0.2)

> 微信小程序开发工作流

欢迎fork、提issue

## 简介

### 为什么会有这套工作流？

在开发小程序的时候，发现有很多不舒服的的地方，但又不想违背小程序原生开发的方式，所以创建了这个小程序开发工作流。

对于了解gulp的人，这套工具流几乎没有任何学习成本（它不是框架），可以在几分中学会如何使用它。

### 工作流能解决什么问题？

#### 已经实现

* pug 转 wxml（也支持直接使用wxml）
* less 转 wxss（也支持直接使用wxss）
* sfc 转 wxml、wxss、json、js（使用vue的单文件组件方式来写小程序）
* 压缩gif/jpge/png/svg
* 自动编译，仅处理修改过的文件，编译极快（除了压缩图片比较耗时）
* js、css风格统一
* 打包npm script

#### 未来实现

* 图片支持使用 CDN
* 增加一些封装好的常用组件

## 使用

### 1、开始

* 克隆本仓库
* 请务必开启如下功能`微信开发者->工具详情`
  * ES6 转 ES5
  * 上传代码时样式自动补全
  * 上传代码时自动压缩

> 为什么这套工作流没有提供压缩wxml、wxss、es5转es6这些功能呢？

这套工作流专注的是小程序开发工具不能处理的事情，希望开发流程更加接近微信小程序原生的模式。

不过，后续这些功能可能会被添加进来。

### 2、目录结构

```tree
root
  - build                      构建相关代码
  - dist                       构建后生成的小程序
  - src                        开发目录
    - components               组件目录
    - pages                    页面目录
    - npm
      * index.js               用于引入用到的npm script，方便打包处理
    - imgs                     图片资源
    - utils                    工具类
    * app.js                   app.js
    * app.wxss                 app.wxss
    * app.json                 app.json
    * config.js                config.js
  - supports                   辅助工具
    * weapp.code-snippets      将该文件导入vscode中，可以在sfc中获得代码片段提示
  - typings
    * wx.d.ts                  微信小程序接口的类型文件，在vscode中可以获得代码提示
  * .csscomb.json              对css进行格式化、排序，统一
  * .eslintignore              eslint忽略文件
  * .eslintrc.js               eslint规则
  * jsconfig.json              配合typings下的ts文件，引导vscode去提示代码
  * package.json               ...
  * package-lock.json          ...
  * project.config.json        小程序的配置文件（注意将配置里的小程序目录指向./dist目录）
  * readme.md                  ...
```

三种不同的实例：

* pages - index页面用了less和pug

* pages - logs页面用了原生写法

* components - UserInfo组件用了sfc（.vue）的方式

### 3、命令

* `npm build`   构建模式
* `npm run dev` 开发模式，执行之前会自动执行一遍npm build
* `npm run eslint` 使用eslint检查所有的js、sfc文件
* `npm run style-unify` 使用csscomb统一所有的less、css书写规范（还不支持在sfc文件中做处理）

### 4、gulp4

`npm build`和`npm run dev`的背后是两个不同的gulp任务。

除了这两个任务以外，我们还提供了两个辅助任务:

* `cancel-sfc` 取消使用sfc文件，该任务会将`src`目录下所有的`.vue`文件在期目录下拆分为`wxss/less`、`js`、`json`、`wxml/pug`文件。（针对不想使用单文件组件的人）
* `del-sfc` 删除所有src目录下的sfc文件（.vue文件）。请谨慎使用该命令，除非你确认所有的sfc文件已经拆分完成！

## Thanks

* Blocks.Tech - 技术团队