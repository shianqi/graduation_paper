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

从1991年 Tim Berners-Lee 公开提及 HTML 描述，到1994年网景推出了第一版 Navigator，同年为动态 web 网页设计的服务端脚本 PHP 诞生。1995年网景推出了 JavaScript，实现了客户端的计算任务。再到1999年 W3C 发布 HTML4，网页的出现是为了更好的交流彼此的想法。与此同时，整个 IT 行业的概念和雏形逐渐形成。

2004年10月 O'Reilly Media、Battelle 和 MediaLive 引导了第一个 Web2.0 大会，Web2.0 时代正式来临。Blog，Wiki，RSS 各种网站逐渐走进大家的视野。2006年8月，jQuery 的第一个版本发布。jQuery 主要用于操作 DOM，其优雅的语法、事件驱动型的编程思维使其极易上手，因此很快风靡全球。大量基于 jQuery 的插件构成了一个庞大的生态系统，更加稳固了 jQuery 的地位。

但随着 W3C 规范和标准进一步推动，大家对 Web 页面复杂度进一步的加剧，人们不再满足于 jQuery 面条式的开发，各种用于简化客户端开发的框架层出不穷，诸如 Backbone，Ember，AngularJS，Vue，Avalon，Knockout，React 等等各种各样的框架。与此同时，在我们看不到的背后，浏览器第二次大战打响，V8 引擎开始大放异彩，Web 标准也在推动 ECMAScript5.0 进化着。node.js 发布了，意味着我们前端的领域已经拓展到服务端了。

2015年，Facebook 在 React.js Conf 2015 大会上推出了基于 JavaScript 的开源框架 React Native。再一次将 React 推向了一个新的高度，learn once, write everywhere. 这是属于 React 的一年。与此同时，构建打包工具也在不停的迭代，Grunt 的辉煌不复存在，Gulp 刚刚兴起，Webpack 的浪潮就席卷而来。

2016年，Webpack 成为主流的前端构建工具。Vue 凭借广大的中国开发者强势崛起。AngularJS2 也完成发布。主流的 JavaScript 框架也形成了三足鼎立之势（React，Vue，AngularJS）

到如今，React 仍然是最主流的前端开发框架。虽然 Rollup 和 Parcel 也强势崛起，但 Webpack 仍是当下最主流的前端构建工具。本文就使用 React、Redux、Webpack 构建一个完善的 SPA 云音乐客户端，并从中窥视一下当今的前端主流解决方案。

[](https://www.cnblogs.com/kidney/p/6079530.html)
[](https://zhuanlan.zhihu.com/p/23858051)

## 正文

### 相关技术分析

#### React

React 是一个用于构建用户界面的 JavaScript 库，最初起源于 Facebook 的内部项目，用来架设 Instagram 的网站，并于 2013 年 5 月开源。一经开源，广受开源社区的好评。React 能有如今的火爆程度，和它拥有如下的的特点是密不可分的：

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

首先安装 node.js 环境和 npm，我这里采用的版本是 node.js v8.9.0 和 npm v5.5.1。之后下载 git 二进制安装包安装，用来对项目进行版本控制。

首先初始化 npm 配置文件和 git 项目

```bash
npm init -y
git init
```

然后安装必要的依赖，包括 react、webpack、babel、react-router、redux、eslint、stylelint 等。

```bash
npm install
```

##### babel 配置

因为我们所采用的 JavaScript 是最新的 ES2017(ES8) 规范，甚至目前主流的 Chrome 浏览器还没有完全实现该规范，更不用说还要兼容低版本的 IE 浏览器。而通过 Babel 我们就可以提前使用 ES6+ 的功能，Babel 是一个被广泛使用的转码器，可以将 ES6+ 的代码转换为浏览器可以识别的低版本 JavaScript 代码。并且可以根据需要适配的浏览器版本，选择合适的 polyfills，来兼容低版本的浏览器。并且因为使用 ES6 Modules，故可以将没有使用的代码不打包在最终生成的文件中，在兼容低版本浏览器的同时下还保证了程序不会变的臃肿。并且可以通过添加 babel-preset-react 插件来识别 react 所依赖的 jsx 语法。通过 babel-preset-stage-x 插件，可以使用目前未被标准化，但被广泛认同，未来可能会纳入标准的语法。

例如如下的 ES6+ 语法：

```javascript
[1, 2, 3].map(n => n ** 2);
```

可以转换为：

```javascript
[1, 2, 3].map(function (n) {
  return Math.pow(n, 2);
});
```

##### eslint & stylelint 配置

代码风格和整洁程度也是衡量代码质量的重要指标，毕竟程序是写给人看的，顺便让计算机去执行。不同风格混杂在一起极大的影响代码的可读性与质量。所以，我们的项目也要加入静态检查和统一编码风格的检测。eslint 和 stylelint 就是分别是对 JavaScript 和 CSS 做静态检查和统一编码风格。并且都使用当下开源社区都认可的 standard 配置。

##### CSS 优化

为项目添加 PostCSS 支持，PostCSS 是一个利用 JavaScript 插件来对 CSS 进行转换的工具，这些插件非常强大，强大到无所不能。其中，Autoprefixer 就是众多 PostCSS 插件中最流行的一个，他能通过配置的要兼容的浏览器版本，自动为 css 添加相应的前缀。

每个经验丰富的软件开发人员都知道，一旦你使用了全局命名空间（Global namespaces），就相当于打开了一扇充满麻烦的大门。如果在代码中没有为对象提供唯一的名称，那么你将不可避免地面临命名冲突、各种副作用以及无法维护的代码问题相继到来。几乎所有的编程语言都支持带有作用域隔离(Isolated scope)的模块。即使是一直与 CSS 密切相关的JavaSript，也具有 AMD、CommonJS 和 ES6 模块。然而 CSS 并没有这样的模块。CSS-Modules 的出现填补了这样的空白。CSS-Modules 可以使用 node.js 自动处理所有的 CSS 类，默认情况这些类都是本地的（局部的），也是唯一的。然后生成一个JSON文件来存储原始类和映射出来的类。这样就解决了 css 的全局污染。可以使开发者更高效的开发，并且对项目重构也更加友好。因为每个模块的 CSS 都是相互独立的，不会因为全局命名空间而导致牵一发而动全身的情况了。

##### webpack 性能优化

对 webpack 进行性能优化其实分为两个方面，第一是开发时候需要进行的优化，其次是生成环境需要进行的优化。

###### 开发环境优化

模块热替换：开发网页时，每当写完一个小功能或调整一个样式，总要切换到浏览器，然后刷新浏览器查看效果。这就造成了开发效率的低下，调试的时候大部分时间都浪费在无意义的应用切换和点击刷新按钮。这时候就要使用 webpack 提供的模块热替换(Hot Module Replacement 或 HMR)。热模块替换是 webpack 提供的最有用的功能之一。其内部是使用 node.js 开启一个开发服务器，并监听本地代码文件变化，当代码发生变化的时候会重新编译项目，并找到两次版本不同的部分，通过 json 的形式发送给浏览器中的 HMR Runtime。浏览器再解析 json 文件，动态更新修改的部分，就实现了模块热替换。从而当代码发生变化的时候，浏览器也给出相应反馈，大大提高开发效率。

生成 source map：我们的源代码是用 ES2017(ES8) 写的，但是运行在浏览器中的是经过 Babel 编译后的代码，调试的时候就很痛苦了。这时我们就需要 source map 来映射编译前前的代码。而且要确保生成 source map 的时候要足够快，不然编译的过程就太慢了。所以采用了 cheap-source-map 这种编译速度快，但是不太安全的方法。在生产环境一定不能采用这种方法。

分离第三方库：第三方库是比较稳定的，不会轻易改变，利用浏览器缓存后，用户再次加载页面会减少服务器请求，提高速度优化体验。而且还能够减少热模块替换时的编译速度，使改变更快的应用到浏览器上。这样做的好处是，只要库文件不变，只需要打包一次，以后再打包业务代码和库文件没关系啦，这样一来真正做到了库文件永远是那个库文件，只要库文件不变，缓存永远有效

编译文件分析：一个成熟的项目，需要的 npm 依赖包也是十分多的。就拿本项目说就已经 69 个依赖了，如果这当中有写没有用到的被打包进项目中，那岂不是太影响最终的效果了。所以我们需要 webpack-bundle-analyze 这个插件，来帮我们可视化的分析出项目每个依赖的大小和依赖关系，使我们能更加极致的优化依赖关系。

###### 生产环境优化

自动添加 hash 优化缓存：

缓存是浏览器对静态资源加载的一种非常重要的优化方式，但有时我们更新了某个 css 文件，或者更新了某个图片。网页上并没有改变，这时候我们就要在 css 或者图片等资源后加上类似于这样 "base.css?v=0.3" 版本号，但是手动改版本号太过于繁琐，往往会因为程序员疏忽漏掉。而这种活交给 webpack 干就非常容易了。webpack 可以在生成每个文件的时候，将文件的名字替换成文件的 hash。所以只要两份代码完全相同，那么他们的名字也就相同，起到了缓存优化的作用。

分离打包 css 和 js：

webpack 把所有的资源都当成了一个模块，JavaScript、css、图片、字体等资源，都可以打包在一个 bundle.js 中。但是如果我们改变部分 js 代码，会导致整个应用的 hash 发生变化，所以 css 缓存也会失效。使用 extract-text-webpack-plugin 插件，我们可以将 css 和 js 分别打包，将业务逻辑从样式中抽离出来，从而更好的利用缓存。

压缩混淆 js：

通过 UglifyPlugin 可以将 webpack 编译后代码进行压缩，并且使用更短的变量名代替原来的变量名。使生产环境的代码变得更小，下载源文件所需要的时间大大缩短。还有一个好处就是别人更难破解你的代码，因为经过混淆后的代码十分晦涩难懂。

### 软件测试

靠人工来保证项目的维护总是不错差错是不靠谱的，人总有健忘和糊涂的时候，尤其是当项目越来越复杂的时候，一个人甚至无法了解项目的全部逻辑，这时我们就要依靠测试来保证项目的可靠性了，这里所说的测试包括但不限于，单元功能测试，UI测试，兼容性测试。

#### 自动化测试

一个自动化测试体系一般包括如下四个部分：

* 测试运行器（Test Runner）：edp-test karma
* 测试框架（Testing Framework）：jasmine mocha qunit Jest
* 断言库（Assertion Library）：expect.js should chai
* 覆盖率（Coverage Library）：istanbul

本文所用到的是 karma + jasmine + istanbul。jasmine 是一个比较完善的测试框架，自带了丰富的断言函数，在编写测试用例的时候能够不用引用第三方断言库。

#### 持续集成

持续集成是一种软件开发实践，即一个团队的开发成员每天都要集成他们的工作，并且每天至少集成一次，也就意味着每天可能会发生多次集成。每一次的集成都通过自动化的构建（包括编译，自动化测试，发布等）来验证，从而尽可能早的发现问题。

GitHub 上比较主流的持续集成工具有 Travis CI 和 Circle CI。我们以 Travis CI 为例：

在项目根目录下创建 Travis 的配置文件，并写下如下配置：

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

我们需要告诉我们的测试代码是用什么语言（language）编写的、相应版本（version）、每次构建如何安装依赖包（install）、怎么执行测试程序（script）。当完成这些配置后，每次将代码提交到 GitHub 上时就会自动触发测试脚本，如果产生问题会给项目提交者发送邮件提醒。通过日志查询具体问题，从而尽早发现问题所在。

当完成测试时，会调用 after_script 中的 npm 脚本，进行代码覆盖率检查，代码覆盖率报告可以通过一系列工具可视化的将代码测试情况反馈给用户，让用户感知这个程序的测试覆盖情况。

[](http://blog.csdn.net/zhangzq86/article/details/55657322)

#### 跨浏览器集成测试

我们的代码最终是运行在浏览器中，所以在各个浏览器端的兼容性也是非常重要的。很多项目会选择使用 PhantomJS/jsdom 当作浏览器环境来运行代码，虽然这样很方便，但是毕竟是模拟浏览器环境，无法完全代替真实的浏览器环境，并且各个浏览器的差异还是十分大的，甚至同一浏览器不同版本也存在巨大的差异。为此，我们需要 SauceLabs 这个平台帮助我们提供多重浏览器环境（包括 PC 端和移动端），并且帮助我们实现在多个浏览器中自动运行脚本。

我需要做的就是安装 karma-sauce-launcher 这个 karma 插件，这个插件可以帮我们自动调起相应的浏览器。并且在 karma 的配置文件中注册 SauceLabs 服务并填写所需测试的各种浏览器版本。

## 结论

![nusic](./img/music.png)

## 主要参考文献

[1] [A JavaScript library for building user interfaces.](https://reactjs.org/) 2018

[2] [Declarative routing for React](https://reacttraining.com/react-router/) 2018

[2] [Redux is a predictable state container for JavaScript apps.](http://redux.js.org/) 2018

[3] [webpack is a module bundler for modern JavaScript applications.](https://webpack.js.org/) 2018

[4] [The compiler for writing next generation JavaScript](http://babeljs.io/) 2018

[5] [基于Dom Diff算法分析React刷新机制](http://www.cnki.com.cn/Article/CJFDTOTAL-DNZS201718033.htm) 2017
