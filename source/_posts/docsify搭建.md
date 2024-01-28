---
title: docsify搭建
author: 少年
tags:
  - docsify
  - nodejs
categories: 建站篇
abbrlink: docsify
date: 2021-02-23 12:00:00
---

### 概述

docsify 可以快速帮你生成文档网站。不同于 GitBook、Hexo 的地方是它不会生成静态的 `.html` 文件，所有转换工作都是在运行时。如果你想要开始使用它，只需要创建一个 `index.html` 就可以开始编写文档并直接[部署在 GitHub Pages](https://docsify.js.org/#/zh-cn/deploy)。

### 安装环境

nodejs

![](https://gitee.com/kuiler/imgaes/raw/master/img/node.png)

### 快速开始

推荐全局安装 `docsify-cli` 工具，可以方便地创建及在本地预览生成的文档

```bash
npm i docsify-cli -g
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node1.png)

### 初始化项目

如果想在项目的 `./docs` 目录里写文档，直接通过 `init` 初始化项目。

```bash
docsify init ./docs
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node2.png)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node3.png)

### 开始写文档

初始化成功后，可以看到 `./docs` 目录下创建的几个文件

- `index.html` 入口文件
- `README.md` 会做为主页内容渲染
- `.nojekyll` 用于阻止 GitHub Pages 忽略掉下划线开头的文件

直接编辑 `docs/README.md` 就能更新文档内容，当然也可以[添加更多页面](https://docsify.js.org/#/zh-cn/more-pages)。

### 本地预览

通过运行 `docsify serve` 启动一个本地服务器，可以方便地实时预览效果。默认访问地址 [http://localhost:3000](http://localhost:3000/) 

```bash
docsify serve ./docs
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node4.png)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node5.png)

### Loading 提示

初始化时会显示 `Loading...` 内容，你可以自定义提示信息。

```bash
 <!-- index.html -->   <div id="app">加载中</div>
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node6.png)

### 多页文档

如果需要创建多个页面，或者需要多级路由的网站，在 docsify 里也能很容易的实现。例如创建一个 `guide.md` 文件，那么对应的路由就是 `/#/guide`。

```text
假设你的目录结构如下：

. └── docs  
	├── README.md   
    ├── guide.md   
    └── zh-cn   
    	├── README.md      
        └── guide.md
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node7.png)

### 定制侧边栏

为了获得侧边栏，您需要创建自己的_sidebar.md，你也可以自定义加载的文件名。默认情况下侧边栏会通过 Markdown 文件自动生成，效果如当前的文档的侧边栏。

首先配置 `loadSidebar` 选项，具体配置规则见[配置项#loadSidebar](https://docsify.js.org/#/zh-cn/configuration?id=loadsidebar)。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

接着创建 `_sidebar.md` 文件，内容如下

<!-- docs/_sidebar.md -->

* [首页](zh-cn/)
* [指南](zh-cn/guide)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node8.png)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node9.png)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node10.png)

### 显示目录

自定义侧边栏同时也可以开启目录功能。设置 `subMaxLevel` 配置项，具体介绍见 [配置项#sub-max-level](https://docsify.js.org/#/zh-cn/configuration?id=sub-max-level)。

```html
<!-- index.html -->

<script>
  window.$docsify = {
    loadSidebar: true,
    subMaxLevel: 2
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
```

![](https://gitee.com/kuiler/imgaes/raw/master/img/node11.png)

![](https://gitee.com/kuiler/imgaes/raw/master/img/node12.png)

### 封面

通过设置 `coverpage` 参数，可以开启渲染封面的功能。具体用法见[配置项#coverpage](https://docsify.js.org/#/configuration?id=coverpage)。

### 基本用法

封面的生成同样是从 markdown 文件渲染来的。开启渲染封面功能后在文档根目录创建 `_coverpage.md` 文件。渲染效果如本文档。

*index.html*

```html
<!-- index.html -->

<script>
  window.$docsify = {
    coverpage: true
  }
</script>
<script src="//cdn.jsdelivr.net/npm/docsify/lib/docsify.min.js"></script>
<!-- _coverpage.md -->

![logo](_media/icon.svg)

# docsify <small>3.5</small>

> 一个神奇的文档网站生成器。

- 简单、轻便 (压缩后 ~21kB)
- 无需生成 html 文件
- 众多主题

[GitHub](https://github.com/docsifyjs/docsify/)
[Get Started](#docsify)
```

![](C:\Users\ZZZYY\Desktop\node13.png)