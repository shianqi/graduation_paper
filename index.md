---
内蒙古大学
本科生毕业设计（论文）
---
# 基于 React， Redux 和 Webpack 的云音乐播放器

## 论文摘要

本文通过理论分析与已有文献进行对接，从前端组件化、工程化展开。包括使用 React 进行组件化开发，使用 Redux 管理 SPA 中的数据交互和运行状态，使用 Webpack 对项目进行打包优化。并根据以上理论构建出一个 SPA 云音乐客户端来研究在具体项目中 React、Redux 和 Webpack 各自的功能和使用方法。

## 论文关键词

React、 Redux、 Webpack、 SAP、 播放器、 前端

## 引言

从1991年 Tim Berners-Lee 公开提及 HTML 描述，到1994年网景推出了第一版 Navigator，同年为动态 web 网页设计的服务端脚本 PHP 诞生。1995年网景推出了 JavaScript，实现了客户端的计算任务。再到1999年 W3C 发布 HTML4，网页的出现是为了更好的交流彼此的想法，整个 IT 行业的概念和雏形逐渐形成。

2004年10月 O'Reilly Media、Battelle 和 MediaLive 引导了第一个 Web2.0 大会，Web2.0 时代正式来临。Blog，Wiki，RSS 各种网站逐渐走进大家的视野。2006年8月，jQuery 的第一个版本发布。jQuery 主要用于操作DOM，其优雅的语法、事件驱动型的编程思维使其极易上手，因此很快风靡全球。大量基于 jQuery 的插件构成了一个庞大的生态系统，更加稳固了 jQuery 的地位。

随着 W3C 规范和标准进一步推动，大家对 Web 页面复杂度进一步的加剧，人们不再满足于 jQuery 面条式的开发，出现了许多用于简化客户端开发的框架，诸如 Backbone，Ember，AngularJS，Vue，Avalon，Knockout，React 等等各种各样的框架。

[](https://www.cnblogs.com/kidney/p/6079530.html)
[](https://zhuanlan.zhihu.com/p/23858051)

## 正文

### 相关技术分析

#### React

React 是一个用于构建用户界面的 JavaScript 库，起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。一经开源，广受开源社区的好评。React 能有如今的火爆程度，和它拥有如下的的特点是密不可分的：

1. **声明式设计** - React 采用声明范式，可以轻松描述应用。
1. **高效** - 通过使用虚拟 DOM，最大限度的减少与 DOM 的交互。
1. **灵活** - 可以与已知的库和框架很好的配合。
1. **组件化** - 天生的组件化，可以使代码复用变得十分容易。能够十分容易的构建大型项目。
1. **单向响应的数据流** 数据流动方向可以跟p踪，流动单一，利于追踪问题。

我们知道，DOM 操作是非常耗时的，如果我们把一个简单的 div 元素属性都打印出来，你会看到如下的结果。而这只是第一层，真正的 DOM 元素是非常庞大的。而且操作的时候要非常的小心，可能一个轻微的触碰，就会导致整个页面重排，这就是影响性能的罪魁祸首。
[](https://github.com/livoras/blog/issues/13)

相对于直接对 DOM 进行操作，处理原生的 JavaScript 就非常快了，而且更加简单。

```javascript
var element = {
  tagName: 'div', // 节点标签名
  props: {        // DOM的属性，用一个对象存储键值对
    id: 'article'
  },
  children: [     // 该节点的子节点
    {tagName: 'h1', props: {class: 'title'}, children: ["Title"]},
    {tagName: 'p', props: {class: 'text'}, children: ["Text"]},
  ]
}
```

上面对应的HTML写法是：

```html
<article id='article'>
  <h1 class='title'>Title</h1>
  <p class='text'>Text</p>
</article>
```

既然原来的 DOM 树可以用 JavaScript 对象表示，那么反过来也可以用这个 JavaScript 对象来还原 DOM 树。

那么我们就可以用 JavaScript 对象表示 DOM 信息和解构，当状态发生变化的时候，我们可以用新的对象树和旧的对象树进行比较，记录这两棵树的差异。记录下来的不同的就是我们需要真正更新的 DOM 元素。然后将其应用到真正的 DOM 树上，页面就更新了。

这就是所谓的 Virtual DOM 算法，包括如下步骤：

* 用 JavaScript 对象表示 DOM 树的解构；然后用这个树构建一个真正的 DOM 树，插到文档中。
* 当状态更新的时候，重新构造一棵新的树。然后用新的树和旧的树对比，记录两棵树的差异。
* 把所记录的两棵树的差异应用到真实的 DOM 上，视图就更新了。

Virtual DOM 本质上就是在 JavaScript 和 DOM 之间做了一个缓存。可以类比 CPU 和内存，既然操作内存这么慢，我们可以在 CPU 上加入 Cache Memory 来加速这一操作。

#### Redux

React 是一个 UI 库，单靠 React 不足以搭建一个完整的 web 应用。因此，我们要结合其他框架，才能搭建一个完整的 web 应用。2014年，Facebook 发布了 Flux 就提供了一种架构思想。2015年 Redux 出现，将 Flux 和 函数式编程 结合在一起，成为了一时前端框架的热门。Redux 的出现就是为了更复杂的业务逻辑设计的，如果是简单的业务逻辑，可以完全不使用 Redux。

为了便于管理和跟踪状态，在 react 中数据是单向流动的，也就是数据总是从父组件传递到子组件的。如果子组件想更新父组件的状态，只能通过父组件给子组件暴露的方法。所以数据由始至终都是从父组件流向子组件，我们称为单向数据流。

这也是深层次的组件之间通讯困难的原因：数据的传递是单向的，子组件的数据只能就近获取，但是真正的数据源却离得太远，没有捷径可以直接通知数据源更新状态。而 Redux 的出现改变了 react 的这种窘迫处境，它提供了整个应用的唯一数据源 store，这个数据源是随处可以访问的，不需要靠父子相传，并且还提供了（间接）更新这个数据源的方法，并且是随处可使用的！

Redux 借鉴了设计模式中的命令模式（Command Pattern），将一个请求封装成一个对象，从而让你使用不同的请求把客户端参数化，对请求排队或者记录请求日志，可以提供命令的撤销和恢复功能。

要理解 Redux 首先要理解这四个概念： store、action、reducer、dispatch

![redux](./img/redux.png)

* Store 就是保存共享数据的地方，你可以把它看成一个容器。整个应用只能有一个 Store。
* Action 是用来描述当前发生的事情。State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，用户想要改变 State 需要通过一个媒介来完成，这个媒介就是 Action，用户每一次请求改变状态都会产生一个相应的 Action。
* Reducer 是处理 Action 的地方，是一个函数，它接受 Action 并且根据当前的 State，返回一个新的 State。
* Dispatch 是 View 通知 Reducer 接收 Action 的唯一方法。

所以整个数据流就变成这样：整个应用的共享数据存在 Store 中， React 根据 Store 和自身的 State 渲染出 View。当用户想更新 Store 中的数据，则要生成相应的 Action，并且调用 store 所暴露出的 dispatch 方法，将 Action 传递给 Reducer 。Reducer 接收到 Action 并且根据当前的 State，返回一个新的 State 去更新 Store 中的数据。从而再由 React 更新 View。

#### Webpack

随着前端的发展，现有很多网站都能看做是一个功能丰富的应用，他们拥有着复杂的 JavaScript 代码和一大堆相关依赖。为了简化开发的复杂度，前端社区出现了很多好的实践方法。

* 模块化，将复杂的程序细化为小的代码片段
* 类似 TypeScript 这种在 JavaScript 基础上拓展的开发语言：使我们能够实现目前版本 JavaScript 不能直接使用的特性，并且之后还能转化为 JavaScript 文件在浏览器上执行。
* Scss，Less 等 CSS 预处理语言
* Babel 通过语法转换器支持最新版本的 JavaScript。 允许你立刻使用新语法，无需等待浏览器支持。

Webpack 可以看作一个模块打包器，它要做的就是分析你的项目解构，找到项目所依赖的各种模块，如 JavaScript 模块，图片，字体文件，以及其他浏览器不能直接运行的拓展语言（Scss，TypeScript等），并经过一系列处理优化，将其转换打包为合适的格式供浏览器使用。

Webpack 能做的事情有很多，包括：代码的合并、压缩、混淆、自动生成哈希（优化缓存），前端自动化，热更新调试，SASS/LESS 和 ES6+ 编译和解释执行，字体文件的打包裁剪压缩等等一些列工作。更凭借其强大的 Loaders 和 Plugins 可以让我们完成更加丰富的功能。甚至可以自己拓展想要的功能。

### 软件设计及实现

#### 系统总体解构设计

整个系统采用 B/S 架构，但本文的研究范围不涉及服务器开发。

前端所采用 HTML5、CSS3、JavaScript 所开发，其中 JavaScript 采用最新的 ES2017(ES8) 规范，并使用 Babel 通过语法转换器支持最新版的 JavaScript 语法。

#### 项目搭建

#### 开发环境

首先安装 node.js 环境和 npm，我这里采用的版本是 node.js v8.9.0 和 npm v5.5.1。之后下载 git 二进制安装包安装，用来对项目进行版本控制。



## 结论

## 主要参考文献

[1] [A JavaScript library for building user interfaces.](https://reactjs.org/) 2018

[2] [Declarative routing for React](https://reacttraining.com/react-router/) 2018

[2] [Redux is a predictable state container for JavaScript apps.](http://redux.js.org/) 2018

[3] [webpack is a module bundler for modern JavaScript applications.](https://webpack.js.org/) 2018

[4] [基于Dom Diff算法分析React刷新机制](http://www.cnki.com.cn/Article/CJFDTOTAL-DNZS201718033.htm)

[5] [基于React的远程会诊系统设计](http://www.cnki.com.cn/Article/CJFDTOTAL-XXDL201722043.htm)
