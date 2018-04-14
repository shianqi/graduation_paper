# 基于 React， Redux 和 Webpack 的前端优化方案

## 摘要

随着近几年来互联网技术的极速发展，人们对互联网的依赖也越来越强，和计算机进行交互的场景也越来越多，随之而来的是公众对用户体验的要求越来越高。前端开发技术的发展能够大大简化开发者的开发难度，从而减少开发者的开发成本并且网站的整体质量。本文主要探讨在前端开发领域方面的应用，运用 React、Redux 和 Webpack 的深度整合，来优化网页的性能和质量，在更小的打包体积下极大提升网站的响应速度和兼容性。论文主要包括使用 React 进行组件化开发，使用 Redux 管理复杂的单页 Web 应用（SPA）中的换数据和运行状态，并且使用 Webpack 对项目进行打包优化。之后根据以上理论构建出一个 SPA 云音乐客户端来研究在具体项目中通过 React、Redux 和 Webpack 来优化网站的整体性能。

## 论文关键词

React、Redux、Webpack、前端开发、网站优化

Front-end optimization solution based on React, Redux and Webpack

## ABSTRACT

Author:Shi anqi
Tutor:Xing yi

With the rapid development of Internet technology in recent years, people’s reliance on the Internet has become stronger, and more and more scenes have been interacted with computers. As a result, public demand for user experience has become higher and higher. The development of front-end development technology can greatly simplify the development of developers, thereby reducing the developer's development costs and the overall quality of the site. This article mainly discusses the application in the front-end development field, and uses the deep integration of React, Redux, and Webpack to optimize the performance and quality of the webpage, greatly improving the responsiveness and compatibility of the web site under a smaller package size. The thesis mainly includes component development using React, using Redux to manage the changing data and running status in a complex single-page Web application (SPA), and using Webpack to package and optimize the project. Based on the above theory, a SPA cloud music client was built to study the overall performance of the website through React, Redux, and Webpack in specific projects.

Keywords: React, Redux, Webpack, Front End Development, Website Optimization

## 第一章：绪论

### 选题背景及研究意义

互联网的快速发展使人们对它的依赖也变得越来强，不论是在科研机构，商业领域还是个人生活，我们无时无刻不在直接或者间接的与计算机进行交互。然而随着业务需求逐渐繁杂，用户需要的界面和数据的交互也越来越繁杂。编写传统的 HTML、CSS、JavaScript 页面的复杂度越来越大，维护成本也随之成倍的提高，往往一个小小的改动就要花费很长的时间去修改。此外各个企业之间的竞争越来越大，为了提升用户体验，并且应对多变的市场环境，各个公司也在不断探寻更好的前端技术。前端技术的发展程度关系到各行各业共同的利益，也关系到我们每个人的上网体验。所有的这些方面，都促使前端技术必须不断的发展，来适应日益增长的需求。

前端技术的发展，从1991年 Tim Berners-Lee 公开提及 HTML，到1994年 Netscape 公司推出了 Navigator 的第一个版本，再到 1995年 JavaScript 横空出世，使得在客户端进行计算得以实现。之后在1999年 W3C 组织了正式发布 HTML 4.0 版本，网页技术变的越来越成熟。与此同时，整个 IT 行业的概念和雏形也在逐渐形成。

之后是 2006年8月，jQuery 发布其第一个版本，因为其语法非常简单、基于事件驱动型的编程方法使得很容易上手，因此在之后的一段时间都非常火爆。开源社区出现了大量基于 jQuery 的相关工具，这样完善生态链更加巩固了 jQuery 的地位。

然而随着 W3C 规范和标准的进一步推动，以及 Web 页面复杂度的直线上涨。前端开发工程师们不再满足于使用 jQuery 进行面条式的开发，各种各样的前端开发的框架开始渐渐浮出水面，例如： Backbone，Ember，AngularJS，React，Vue 等等，其中最为出色的莫过于 React，一经开源，就广受开源社区的好评。在这之后，Vue 凭借广大的中国开发者强势崛起。AngularJS2 也完成发布。主流的 JavaScript 开发框架也形成了三足鼎立之势（React，Vue，AngularJS）。2008年，随着第一个版本的 Chrome 浏览器发布，V8 引擎也正式发布。Web 标准也在推动 ECMAScript5.0 进化着。V8 引擎发布后，node.js 也孕育而生，前端也逐渐扩大到服务端开发。各种构建打包工具也默默的不停迭代，Grunt 逐渐没落，Gulp 刚刚兴起，Webpack 的浪潮就席卷而来，并在 2016年成为了主流的前端构建工具。

从二十世纪的兴起，到现在的短短十几年发展，就已经表现出了强大的生命力，到目前发展来看，前端开发技术的发展时间相对较短，但是发展速度却非常快，并且技术的迭代也十分迅速，这和当前互联网的极速发展有着密不可分的关系。一个稳定、流畅、对用户友好的前端界面往往能够给用户带来非常良好的使用体验，非常大的提升了互联网用户的满意度。文本所研究的基于 React、Redux 和 Webpack 的前端优化方案，正是对当前主流前端开发技术的深度整合和性能优化，基于本方案能够在减少开发者开发难度的同时，极大的优化网页的性能和质量，在更小的打包体积下极大提升网站的响应速度和兼容性，获取更好的用户体验。

### 论文的主要内容

本文主要研究网站前端优化方案，通过 React、Redux 和 Webpack 框架的深度整合和性能优化，在减少开发者开发难度的同时来优化网页的性能和质量，在更小的打包体积下极大提升网站的响应速度和兼容性。论文包括五个部分，每一部分的内容组织如下：

* 第一章是绪论，主要介绍了论文的选题背景以及研究意义，包括当前前端技术的发展现状以及发展历程，并在最后介绍了全文的内容安排。
* 第二章是对本文相关概念的进行阐述，并且对本文主要涉及的相关技术进行深入的探讨。
* 第三章是全文的重要部分，分为三小节，分别阐述了原型的设计与实现，对原型开发和生产环境下的优化方法，以及对原型进行自动化测试和持续集成。
* 第四章是对第三章提出的方法的性能分析，主要通过对网站各项性能指标进行对比，来评估此优化方案所带来的性能提升。
* 第五章是论文的结论，指出文章的研究结果和局限性。

## 第二章：相关技术分析

本文主要涉及到的技术为 React、Redux 和 Webpack。其中，React 主要的作用是用来构建组件化的 UI；Redux是一个应用数据流框架，用来存储和维护整个应用的状态；而 Webpack 是用来对项目依赖进行分析打包，它可以分析项目的结构，找到 JavaScript 模块以及其它的拓展语言，并结合其他工具对代码进行处理，最终将其转换和打包为合适的格式供浏览器使用。

### React

React 是一个用于构建用户界面的 JavaScript 库，由 Facebook 于 2013 年 5 月开源，一经开源，广受开源社区的好评。React 能够如此受到欢迎，和它拥有如下的的特点是密不可分的：

1. **高效** - 通过使用虚拟 DOM，能够减少不必要的的交互，从而提高性能。
1. **灵活** - 可以与已知的库和框架很好的配合。
1. **组件化** - 天生的组件化思维，用过组件的方式使代码复用变得十分容易。能够十分容易的构建大型项目。
1. **单向数据流** 数据自顶上下流动，使得整个组件的状态变得可追踪。

我们知道，如果我们直接操作 DOM，那么性能是非常差的，我们可以把一个最基础的 DOM 元素属性都列出来，结果如下，因为比较长，这里只粘贴了约 1/10。

```javascript
const arr = []
const div = document.createElement('div')
for (var key in div) {
  arr.push(`[${key}]:${div[key]}`)
}
console.log(arr.join(' '))
```

```text
[align]: [title]: [lang]: [translate]:true [dir]: [dataset]:[object DOMStringMap] [hidden]:false [tabIndex]:-1 [accessKey]: [draggable]:false [spellcheck]:true [contentEditable]:inherit [isContentEditable]:false [offsetParent]:null [offsetTop]:0 [offsetLeft]:0 [offsetWidth]:0 [offsetHeight]:0 [style]:[object CSSStyleDeclaration] [innerText]: [outerText]: [onabort]:null [onblur]:null [oncancel]:null [oncanplay]:null [oncanplaythrough]:null [onchange]:null [onclick]:null [onclose]:null [oncontextmenu]:null [oncuechange]:null [ondblclick]:null [ondrag]:null [ondragend]:null [ondragenter]:null [ondragleave]:null [ondragover]:null [ondragstart]:null [ondrop]:null [ondurationchange]:null [onemptied]....
```

然而这不过是 DOM 对象第一层的属性，真正的 DOM 元素是非常庞大的。而且在操作 DOM 的时候要非常的小心，不然会导致整个页面重排，这对网站的性能有非常大的影响。

我们可以用一个简单的 JavaScript 对象来表示 DOM 节点，这样我们只要操作 JavaScript 对象就可以模拟 DOM 上的操作了。

```javascript
var element = {
  tagName: 'div', // 节点标签名
  props: {        // DOM的属性，用一个对象存储键值对
    id: 'article',
  },
  children: [     // 该节点的子节点
    {tagName: 'h1', props: {class: 'title'}, children: ["Title"]},
    {tagName: 'p', props: {class: 'text'}, children: ["Text"]},
  ],
}
```

<!-- ![code1](./img/code1-nb.png) -->

可以将上面的 JavaScript 对象转换成真实的 DOM

```html
<div id='article'>
  <h1 class='title'>Title</h1>
  <p class='text'>Text</p>
</div>
```

<!-- ![code2](./img/code2-nb.png) -->

既然原来的 DOM 树可以用 JavaScript 对象表示，那么反过来也可以用这个 JavaScript 对象来还原 DOM 树。

那么我们就可以用 JavaScript 对象表示 DOM 信息和结构，当状态发生变化的时候，我们可以用新的对象树和旧的对象树进行比较，记录这两棵树的差异。记录下来的不同的就是我们需要最后更新的内容。然后将其应用到真正的 DOM 树上，页面就更新了。这就是虚拟 DOM 算法。

### Redux

React 是一个 UI 库，单靠 React 不足以搭建一个完整的 web 应用。为了管理 React 的数据，Facebook 推出了 Flux 框架，2015年 Redux 出现，将 Flux 和函数式编程的方法合二为一，成为了一时前端框架的热门。Redux 的出现就是为了解决复杂场景下的业务逻辑设计的，如果是简单的业务逻辑，可以完全不使用 Redux。

因为在 React 中数组是从上向下单向的，子节点的数据只能从它的父节点上获取，但是如果节点的嵌套层次非常深，那么如果子节点要获取数据就要通过层层传递来获取，这样就导致了重复的编码工作，也不利于修改。而 Redux 的出现就是为了解决这个问题。

想要理解 Redux 先要理解这四个名称： store、action、reducer、dispatch

![redux](./img/redux.png)

* Store 是客户端用来存状态的地方，一个客户端只能有一个单独的 Store。
* Action 是用来描述一个特定的客户端事件，可以是输入内容，也可以是点击某个按钮。如果 State 发生变化那么 View 也会相应的变化。但是，用户无法直接改变 State，只能操作 View。所以，用户想要改变 State 需要通过一个媒介来完成，那就是 Action，用户每一次请求改变状态都会产生一个相应的 Action。
* Reducer 是处理 Action 的场所，是一个函数，它接收一个 Action 并且根据当前的 State，返回一个新的 State。
* Dispatch 是 Reducer 接收 Action 用来更新数据的唯一入口。

所以整个数据流就变成这样：整个的享数据报存在 Store 中，React 根据 Store 和自身的 State 渲染出 View。当用户想更新 Store 中的数据，则要生成相应的 Action，并且回调 store 流出的 dispatch 方法，将 Action 和存在其中的数据传递给 Reducer 。Reducer 接收到 Action 并且根据当前的 State 返回一个新的 State 去更新 Store 中的数据。从而再由 React 更新 View。

### Webpack

随着前端的发展，一个功能完备的网站所需要的依赖越来越多，几十个上百个依赖是常事。为了整合这些依赖，并且减小文件体积，我们需要用 Webpack 来简化流程。

* 模块化，将复杂的程序细化为小的代码片段
* Scss，Less 等 CSS 预处理语言
* 通过 Babel 我们就可以提前使用 ES6+ 的功能，Babel 可以将 ES6+ 的代码转换并兼容低版本浏览器。

利用 Webpack 对项目的代码和依赖进行分析，提取重复模块，并将浏览器无法识别的资源转换为可识别的格式。之后可以经过一系列处理优化，并整合成一个完整 JavaScript 文件。

在实际使用中，Webpack 能做的事情有很多，包括：代码的合并、压缩、混淆、自动生成哈希（优化缓存），前端自动化构建，热更新调试，SASS/LESS 和 ES6+ 编译和解释执行，字体文件的打包裁剪压缩等等一些列工作。更凭借其强大的 Loaders 和 Plugins 可以让我们完成更加丰富的功能，在必要时也可以自己拓展需要的功能。

## 原型设计及实现

### 总体架构设计

本原型采用 B/S 架构，并且将前后端进行分离，前端采用单页应用技术，通过 AJAX 请求与服务器进行数据交互。但本文所研究的内容只限于前端单页应用的开发，故不涉及后端服务器部分。

之所以将应用做成单页 Web 应用，是因为其有如下优点：

* 可以像客户端应用一样快速响应用户的请求、同时具备网页的所有优点。
* 用户体验好，切换界面无加载过程，给用户体验原生应用的感觉。
* 后端不用进行渲染，能够减少对服务器的压力，吞吐能力会提高几倍。
* 良好的前后端分离，后端 API 通用化。

但同样，单页 Web 应用也有着如下的缺点：

* 初次加载耗时相对较长。
* 不利于搜索机器人收录网站。
* 书签、导航需要程序实现，复杂度较高。
* 对开发者的能力要求略高。

使用 React 搭建应用，不仅能够享受单页 Web 应用带来的所有优点。并且通过 React 独有的 jsx 语法能够方便快速构建单页 Web 应用，大大降低单页 Web 应用的开发难度，节省开发人员的研发和运维成本。React 的组件化编程思维，能够达到在一次编写，在多处使用的效果。

但单纯使用 React 并不能开发一个功能完备的应用。所以我们必须加上一些必要的依赖来解决开发单页 Web 应用中的其他痛点。例如 react-router，它能够让你的单页应用像普通网站一样可以通过不同的 URL 跳转到不同的界面，可以让你通过简单的 API 实现书签，导航等功能。此外还有 Redux，它能帮助我们管理所有要在多个组件中共享的数据，并优雅的使用他们。

#### 原型搭建

首先搭建 node.js，以及 npm，我这里采用的版本是 node.js v8.9.0 和 npm v5.5.1。之后下载 git 二进制安装包安装，用来对项目进行版本控制。之后初始化 npm 配置文件和 git 项目，然后安装必要的依赖，包括 React、Webpack、Babel、react-router、Redux、eslint、stylelint 等。

```bash
npm install --save react react-dom react-router react-router-dom redux react-redux react-router-redux redux-thunk

npm install --save-dev webpack webpack-dev-server babel-core babel-loader babel-preset-dev babel-preset-stage-3 eslint
```

##### 用 babel 兼容最新版 JavaScript 规范

因为我们所采用的 JavaScript 是最新的 ES2017(ES8) 规范，甚至目前主流的 Chrome 浏览器还没有完全实现该规范，更不用说还要兼容低版本的 IE 浏览器。而通过 Babel 我们就可以提前使用 ES6+ 的功能，Babel 可以将 ES6+ 的代码转换并兼容低版本浏览器。并且因为使用 ES6 Modules，故可以将没有使用的代码不打包在最终生成的文件中，在兼容低版本浏览器的同时下还保证了程序不会变的臃肿。并且可以通过添加 babel-preset-react 插件来识别 React 所依赖的 jsx 语法。通过 babel-preset-stage-x 插件，可以使用目前未被标准化，但被广泛认同，未来可能会纳入标准的语法。

例如如下的 ES6+ 语法：

```javascript
[1, 2, 3].map(n => n ** 2);
```

<!-- ![code3](./img/code3-nb.png) -->

可以转换为：

```javascript
[1, 2, 3].map(function (n) {
  return Math.pow(n, 2);
});
```

<!-- ![code4](./img/code4-nb.png) -->

##### 用 eslint & stylelint 对代码静态检查

代码风格和整洁程度也是衡量代码质量的重要指标，毕竟程序是写给人看的，顺便让计算机去执行。如果同一个项目组不能同意一个一样的代码风格，会导致整个代码的可读性非常差。的所以，我们的项目也要加入静态检查和统一编码风格的检测。eslint 和 stylelint 就是分别是对 JavaScript 和 CSS 做静态检查和统一编码风格。并且都使用当下开源社区都认可的 standard 配置。

### 原型的优化方案

#### CSS 样式优化

为项目添加 PostCSS 支持，PostCSS 是通过 Node.js 来对 CSS 进行一系列处理的工具，它的功能十分强大。其中最被我们熟知的是 Autoprefixer，它通过配置的要兼容的浏览器版本，自动为 css 添加相应的前缀。

处理前：

```css
.example {
    background: linear-gradient(to bottom, white, black);
}
```

处理后：

```css
.example {
    background: -webkit-gradient(linear, left top, left bottom, from(white), to(black));
    background: -webkit-linear-gradient(top, white, black);
    background: -o-linear-gradient(top, white, black);
    background: linear-gradient(to bottom, white, black);
}
```

我们都知道，全局命名空间是一个强大但是非常危险的技术，一旦使用就会给未来留下不易察觉的隐患。如果在写代码的时候，如果你的类名不能保证互不相同的，那么很有可能会导致命名空间冲突，从而导致出现各种各样的问题最终整个代码难以维护。CSS 并不支持独立的作用域，但是 CSS-Modules 的出现填补了这样的空白。CSS-Modules 可以使用 node.js 处理所有出现的 CSS 类，并将每个模块单独起一个唯一的类名。然后用JSON记录原始类和当前类的对照关系。这样就解决了 css 的全局污染。可以使开发者更高效的开发，并且对项目重构也更加友好。这样每个单独模块下的 CSS 都是独立存在，互不依赖，不会因为全局命名空间而导致牵一发而动全身的情况了。

#### 资源优化

##### 图标优化

最开始的时候，网站的图标都是用 png/jpg 格式的图片来展示的，但是随着项目逐渐变大，慢慢的会发现网络请求中的图片资源的请求量占了很大一部分，减少图片资源请求量就变得至关重要了。为了解决这个问题，孕育而生的就是雪碧图。具体做法是将多个图片放在一张图片上，然后通过 background-position 定位到特定位置的图片来使用单独的图片资源。这样做虽然解决了图片细碎的麻烦，但是却依然存在难以维护的困惑。每次新增图标都要重新生成，既不能利用缓存也不太方便。

之后又出现了使用字体库来实现页面图标的，例如 Font Awesome，虽然使用起来非常的方便，但是如果要拓展也是很麻烦的。这时是阿里巴巴的图标库 fonticon 就出现了，并且可以将自己的图标上传供大家使用。iconfont 主要有三种使用方式，第一种是 Unicode、其次是 Font-class、最后是 Symbol。它们的具体区别如下：

|方式|兼容性|调整大小颜色|多色图标|使用格式|
|---|---|---|---|---|
|Unicode|ie6+|√|×|`<i class="iconfont">&#xe604;</i>`|
|Font-class|ie6+|√|×|`<i class="iconfont icon-xxx"></i>`|
|Symbol|ie9+|√|√|`<svg class="icon" aria-hidden="true"><use xlink:href="#icon-xxx"></use></svg>`|

随着 ie 浏览器逐渐退出历史舞台，使得我们不必要再去考虑兼容这样古董级的浏览器。

Symbol 在内部使用的是 svg 图标，因此有如下优点：

* 支持彩色图标，不受单色限制
* 支持通过 css 来调整样式
* 可以用 css 实现动画
* svg 为矢量图，缩放不会失真
* 相比于 img，整体更小
* 可以内联到 html 中，减少 http 请求

但是直接是使用 Symbol 还有一个很大的问题，现在所有的图标都是通过 iconfont 引入的。每次增删图标只能将整个 iconfont.js 文件一起替换。其次也无法做到 **按需加载** 不能根据使用了哪些 svg 来动态加载。也不方便将自己做的 svg 图标整合到 iconfont 上，只能上传然后再重新生成并且下载，十分繁琐。

这时候就需要我们自己制作 svg-sprite 了，不过为了工程化和自动化，我们可以使用 Webpack 编写一个 loader 来自动化整个制作 svg-sprite 的过程。结合我们的项目，我们将 src/icons 目录下的所有 svg 图标都交给 svg-sprite-loader 这个 loader 去处理，并且其他目录下的图标不受此影响。

```javascript
const svgPath = path.join(__dirname, 'src/icons')

config.loader('url-loader', {
  exclude: [svgPath],
})
config.loader('svg-sprite-loader', {
  test: /\.svg$/,
  loader: 'svg-sprite-loader?{"symbolId": "icon-[name]"}',
  include: [svgPath],
})
```

<!-- ![code5](./img/code5-nb.png) -->

配合 Webpack 的 require.context 函数，我们就可以不用手动引入 svg 图标。只需要将图标放到之前定义好的 src/icons 文件夹下，当需要这个图标时就会自动在这个文件夹中寻找。之后我们将这部分封装成一个 React 组件，就能在想使用图标的地方这样使用了：

```html
<Icon type="caret-down" />
```

<!-- ![code6](./img/code6-nb.png) -->

之后我们还要使用 svgo 来去掉 svg 里无用的信息，来进一步优化 svg 的大小，我们先看一下没有经过优化的 svg 是什么样的：

```xml
<?xml version="1.0" standalone="no"?><!DOCTYPE svg PUBLIC "-//W3C//DTD SVG 1.1//EN" "http://www.w3.org/Graphics/SVG/1.1/DTD/svg11.dtd"><svg t="1513157529483" class="icon" style="" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="7167" xmlns:xlink="http://www.w3.org/1999/xlink" width="200" height="200"><defs><style type="text/css"></style></defs><path d="M198.144 204.8l678.4 0c64 0 96.256 30.208 96.256 91.648l0 431.104c0 60.928-32.256 91.648-96.256 91.648l-678.4 0c-64 0-96.256-30.72-96.256-91.648l0-431.104c0-61.44 32.256-91.648 96.256-91.648zM537.088 645.12l345.088-283.136c12.288-10.24 22.016-33.792 6.656-54.784-14.848-20.992-41.984-21.504-59.904-8.704l-291.84 197.632-291.328-197.632c-17.92-12.8-45.056-12.288-59.904 8.704-15.36 20.992-5.632 44.544 6.656 54.784z" p-id="7168"></path></svg>
```

<!-- ![code7](./img/code7-nb.png) -->

经过 svgo 优化后，我们的图标变成了这样：

```xml
<svg class="icon" viewBox="0 0 1024 1024" xmlns="http://www.w3.org/2000/svg" width="200" height="200"><defs><style/></defs><path d="M198.144 204.8h678.4c64 0 96.256 30.208 96.256 91.648v431.104c0 60.928-32.256 91.648-96.256 91.648h-678.4c-64 0-96.256-30.72-96.256-91.648V296.448c0-61.44 32.256-91.648 96.256-91.648zm338.944 440.32l345.088-283.136c12.288-10.24 22.016-33.792 6.656-54.784-14.848-20.992-41.984-21.504-59.904-8.704l-291.84 197.632L245.76 298.496c-17.92-12.8-45.056-12.288-59.904 8.704-15.36 20.992-5.632 44.544 6.656 54.784z"/></svg>
```

<!-- ![code8](./img/code8-nb.png) -->

可以明显看出整个文件变小了很多，并且对显示没有任何影响。经过这一系列的优化，我们终于可以优雅的使用 svg。
[](https://segmentfault.com/a/1190000012213278)

#### Webpack 性能优化

对 Webpack 进行性能方面的优化其实分为两个方面，第一是开发时候需要进行的优化，其次是生成环境需要进行的优化。

##### 开发环境优化

模块热替换：开发网页时，每当写完一个小功能或调整一个样式，总要切换到浏览器，然后刷新浏览器查看效果。这就造成了开发效率的低下，调试的时候大部分时间都浪费在无意义的应用切换和点击刷新按钮。这时候就要使用 Webpack 提供的模块热替换功能了。热模块替换是 Webpack 提供的众多功能中最有用的功能之一。其内部是使用 node.js 开启一个开发服务器，并监听本地代码文件变化，当代码发生变化的时候会重新编译项目，并找到两次版本不同的部分，通过 json 的形式发送给浏览器中的 HMR Runtime。浏览器再解析 json 文件，动态更新修改的部分，就实现了模块热替换。从而当代码发生变化的时候，浏览器也给出相应反馈，大大提高开发效率。

生成 source map：我们的源代码是用 ES2017(ES8) 写的，但是运行在浏览器中的代码是经过 Babel 编译转换后的，调试的时候就很痛苦了。这时我们就需要 source map 来映射编译前前的代码。而且要确保生成 source map 的时候要足够快，不然编译的过程就太慢了。所以采用了 cheap-source-map 这种编译速度快，但是不太安全的方法。在正式上限的时候一定不能采用这种方法。

分离第三方库：第三方的代码库一般在我们架构整个项目的时候就会确定使用的库和相应的版本，并且在日后的开发维护中很少改动，所以我们可以将这些变化小的部分独立抽离出来。而且还能够减少热模块替换时的编译速度，使改变更快的应用到浏览器上。通过这种方式，每次打包的时候，都会计算库包含的所有代码，若干库中的文件不变，那么生成的 Hash 就相同。所以只需要打包一次，只要库文件不变，就可以一直使用。

编译文件分析：一个成熟的项目，需要的 npm 依赖包也是十分多的。就拿本项目说就已经 69 个依赖了，如果这当中有写没有用到的被打包进项目中，那岂不是太影响最终的效果了。所以我们需要 webpack-bundle-analyze 这个插件，来帮我们可视化的分析出项目每个依赖的大小和依赖关系，使我们能更加极致的优化依赖关系。

##### 生产环境优化

* 自动添加 hash 优化缓存：

缓存是浏览器对静态资源加载的一种非常重要的优化方式，但有时我们更新了某个文件或者图片。但是刷新网页并没有改变，这就是缓存的原因了，我们要在 css 或者图片等资源后加上类似于这样 "base.css?v=0.3" 版本号，但是手动改版本号太过于繁琐，往往会因为程序员疏忽漏掉。而这种活交给 Webpack 干就非常容易了。Webpack 可以在生成每个文件的时候，将文件的名字替换成文件的 hash。所以只要两份代码完全相同，那么他们的名字也就相同，起到了缓存优化的作用。

* 分离打包 css 和 js：

Webpack 在打包的时候，会把所有的资源都当成模块。包括 JavaScript、css、图片、字体等资源，都可以打包在一个 JavaScript 文件中。但是如果我们改变部分 js 代码，会导致整个应用的 hash 发生变化，所以 css 缓存也会失效。但是我们可以将程序中的 css 和 JavaScript 打包到不同的文件，将业务逻辑从样式中抽离出来，从而更好的利用缓存。

* 压缩混淆 js：

通过 UglifyPlugin 可以将 Webpack 编译后代码进行压缩，并且使用更短的变量名代替原来的变量名。使生产环境的代码变得更小，下载源文件所需要的时间大大缩短。经过混淆的代码十分晦涩，能够让你的代码没有那么容易被破解。

### 原型自动化测试及持续集成

项目的维护如果全部靠人来保证，那么这个项目也就存在着风险。毕竟人总有犯错的时候，尤其当项目非常庞大的时候，甚至是项目负责人都无法了解项目的全部代码，那么这个时候，测试的出现就可以很好的弥补这个缺陷。

#### 自动化测试

一个自动化测试体系一般包括如下四个部分：

* 测试运行器：edp-test karma
* 测试框架：jasmine mocha qunit Jest
* 断言库：expect.js should chai
* 覆盖率：istanbul

开发软件的时候，我们可以先写好测试，然后逐步满足测试所需的功能。这种开发方式的好处能够非常大程度上减少低级失误，在未来需要对这部分代码重构或者修改的时候，可以将修改代码带来的隐患降到最低。

本原型所采用的是 mocha + istanbul + chai。我们选用 mocha 的理由是因为 mocha 不仅可以运行在浏览器同样可以在 node 上运行，所以我们不需要 karma 框架作为测试运行器

#### 持续集成

在我们的实际开发中，一个大型项目通常都需要多人配合完成，这就需要软件的开发成员要经常同步他们的代码，也就意味着每天要多次提交他们的代码到代码仓库中。为了不将错误引入项目中，每一次的代码提交都应该通过自动化的编译、测试来进行验证，从而尽可能早的发现问题并解决问题。在我们的原型采用的是 Travis CI。

我们要在根目录下创建 .travis.yml 文件，并添加如下的配置：

```yaml
language: node_js
node_js:
    - 6
install:
|
    npm install --registry http://registry.npmjs.org
script:
    - npm run test-ci
after_script:
    - npm run coveralls
```

<!-- ![code](./img/code9-nb.png) -->

我们需要在配置文件中添加所用的语言、相应版本、如何安装所需依赖、如何执行测试代码。当配置完成后并提交代码时，Github 就会检查是否存在该配置，如果有就运行测试脚本。如果脚本运行中发生故障中断，还会给项目提交者发送一封提醒邮件。提交者可以通过日志查到具体的原因，从而尽早发现并解决问题。

当完成测试时，会调用 after_script 中的 npm 脚本，进行代码覆盖率检查，代码覆盖率报告可以通过一系列的数据可视化的手段将代码测试覆盖的情况体现出来，让用户能够清楚的知道这个软件是否经过系统的测试。

[](http://blog.csdn.net/zhangzq86/article/details/55657322)

### 第四章：优化效果评估

对第三章提出的优化方案，我们主要从以下几个性能指标去测试我们的优化效果：

* lighthouse 测试

lighthouse 能够分析网络应用程序和网页，并对比最佳实践给出一个程序的评分。

优化前：
![befor](./img/lighthouse-befor.png)

优化后：
![after](./img/lighthouse-after.png)

首先是性能指标，经过优化从36分提高到了69分，涨幅非常明显；其次是安全性，应为我们的程序还没有对安全性进行进一步的优化，所以这里的评分并没有变化；再后面是针对最佳的评分，从75分提高到了81分，已经非常不错了。最后是 SEO，这是 SAP 技术的共同缺陷，所以分数并没有提升。

我们关注的指标不仅仅有这些，还应该包括下面这些：

* 打包大小

优化之前的打包文件：

```test
-rw-r--r--  1 archie  staff   895K  4 12 20:15 bundle.ae21a79a70d0c0a92a48.js
-rw-r--r--  1 archie  staff   1.7K  4 12 20:15 favicon.ico
-rw-r--r--  1 archie  staff   437B  4 12 20:15 index.html
-rw-r--r--  1 archie  staff   149K  4 12 20:15 styles.61295b6c760ff3a938ff.css
-rw-r--r--  1 archie  staff   384K  4 12 20:15 vendor.1d33576e0fe8974a18fd.dll.js
```

优化之后的打包文件：

```test
-rw-r--r--  1 archie  staff   357K  4 12 21:18 bundle.ae21a79a70d0c0a92a48.js
-rw-r--r--  1 archie  staff   1.7K  4 12 21:18 favicon.ico
drwxr-xr-x  6 archie  staff   192B  4 12 21:18 font
-rw-r--r--  1 archie  staff   410B  4 12 21:18 index.html
-rw-r--r--  1 archie  staff    30K  4 12 21:18 styles.500dbac88cab9453febb.css
-rw-r--r--  1 archie  staff   193K  4 12 21:18 vendor.1d33576e0fe8974a18fd.dll.js
```

其中 index.html 是我们网站的入口文件；bundle.js 是程序的业务逻辑代码；vendor.dll.js 是和业务逻辑没有关系的第三方代码库，我们将其抽离出来，单独打包成一个文件，这样可以在网站更新的时候复用这部分文件的缓存；styles.css 是我们的样式文件；还有 font 文件夹，里面存放是是经过优化的图标文件，优化之前这些图标是存放在 bundle.js 中。经过整理后，我们得到如下的结果：

|文件|优化前|优化后|优化效果|
|---|---|---|---|
|index.html|437B|410B|93.82%|
|bundle.js|895K|357K+192B|39.89%|
|dll.js|384K|193K|50.26%|
|styles.css|149K|30K|20.13%|
|all|1237K|580K|46.89%|

通过上面的图表，可以看到我们的优化效果非常明显，尤其是 css 文件，少了约 4/5 的大小，整体大小减少了 53.11%。下面是打包后的模块图：

![analyze](./img/analyze.png)

### 第五章：结语

通过使用 React 进行 UI 构建，然后使用 Redux 来集中管控数据，然后利用 Webpack 对项目的代码和依赖进行分析，提取重复模块，并将浏览器无法识别的资源转换为可识别的格式。通过 babel 将 ES6+ 的代码转换并兼容低版本浏览器；PostCSS 对 css 进行兼容和拓展，并用 CSS-Moudles 来对 css 进行作用域隔离。使用 iconfont 对图标从大小到兼容性进行优化。并在此基础上添加了自动化测试以及持续集成。

经过我们的理论研究和实践测试，我们发现上述的优化方案确实非常有效果，不仅可以在减少开发者开发难度，并且可以同时优化网页的性能和质量，在更小的打包体积下极大提升网站的响应速度和兼容性。

项目截图：
![nusic](./img/music.png)

## 主要参考文献

[1] [A JavaScript library for building user interfaces.](https://reactjs.org/) 2018

[2] [Declarative routing for React](https://reacttraining.com/react-router/) 2018

[2] [Redux is a predictable state container for JavaScript apps.](http://redux.js.org/) 2018

[3] [webpack is a module bundler for modern JavaScript applications.](https://webpack.js.org/) 2018

[4] [The compiler for writing next generation JavaScript](http://babeljs.io/) 2018

[5] [基于Dom Diff算法分析React刷新机制](http://www.cnki.com.cn/Article/CJFDTOTAL-DNZS201718033.htm) 2017

<!-- https://carbon.now.sh/?bg=rgba(255,255,255,0)&t=base16-dark&l=htmlmixed&ds=false&wc=true&wa=false&pv=0px&ph=0px&ln=true&code= -->

<!-- https://carbon.now.sh/?bg=rgba(255,255,255,0)&t=base16-dark&l=javascript&ds=true&wc=true&wa=false&pv=19px&ph=15px&ln=true&code= -->

```css
.markdown-body img {
  display: block;
  margin: 0 auto;
}

.markdown-body .highlight pre, .markdown-body pre {
  white-space: pre-wrap;
}
```
