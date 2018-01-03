---
layout: post
title: Angular 依赖包详解说明
category: 前端
date: 2017-06-03 18:17:14
---

Angular 应用程序以及 Angular 本身都依赖于很多第三方包 ( 包括 Angular 自己 ) 提供的特性和功能。这些包由 Node 包管理器 (npm) 负责安装和维护。
Angular2开发时依赖的包在package.json文件中都有定义。
{
  "dependencies": {
    "@angular/common": "~2.1.1",
    "@angular/compiler": "~2.1.1",
    "@angular/core": "~2.1.1",
    "@angular/forms": "~2.1.1",
    "@angular/http": "~2.1.1",
    "@angular/platform-browser": "~2.1.1",
    "@angular/platform-browser-dynamic": "~2.1.1",
    "@angular/router": "~3.1.1",
    "@angular/upgrade": "~2.1.1",
    "angular-in-memory-web-api": "~0.1.13",
    "core-js": "^2.4.1",
    "reflect-metadata": "^0.1.8",
    "rxjs": "5.0.0-beta.12",
    "systemjs": "0.19.39",
    "zone.js": "^0.6.25"
  },
  "devDependencies": {
    "@types/core-js": "^0.9.34",
    "@types/node": "^6.0.45",
    "concurrently": "^3.0.0",
    "lite-server": "^2.2.2",
    "typescript": "^2.0.3"
  }
}
dependencies 和 devDependencies

package.json 包含两组包： dependencies 和 devDependencies 。

dependencies 下的这些包是 运行 本应用的基础，而 devDependencies 下的只在 开发 此应用时才用得到。 通过为 install 命令添加 --production 参数，你在产品环境下安装时排除 devDependencies 下的包，就像这样：

COPY CODE
npm install my-application --production
dependencies

应用程序的 package.json 文件中， dependencies 区下有三类包：

特性 - 特性包为应用程序提供了框架和工具方面的能力。

填充 (Polyfills) - 填充包弥合了不同浏览器上的 JavaScript 实现方面的差异。

其它 - 其它库对本应用提供支持，比如 bootstrap 包提供了 HTML 中的小部件和样式。
特性包
@angular/core - 框架中关键的运行期部件，每一个应用都需要它。 包括所有的元数据装饰器： Component 、 Directive ，依赖注入系统，以及组件生命周期钩子。

@angular/core - Critical runtime parts of the framework needed by every application. Includes all metadata decorators, Component,Directive, dependency injection, and the component lifecycle hooks.

@angular/common - 常用的那些由 Angular 开发组提供的服务、管道和指令。

@angular/compiler - Angular 的 模板编译器 。 它会理解模板，并且把模板转化成代码，以供应用程序运行和渲染。 开发人员通常不会直接跟这个编译器打交道，而是通过 platform-browser-dynamic 或离线模板编译器间接使用它。

@angular/platform-browser - 与 DOM 和浏览器相关的每样东西，特别是帮助往 DOM 中渲染的那部分。 这个包还包含 bootstrapStatic 方法，用来引导那些在产品构建时需要离线预编译模板的应用程序。

@angular/platform-browser-dynamic - 为应用程序提供一些 提供商 和 bootstrap 方法，以便在客户端编译模板。不要用于离线编译。 我们使用这个包在开发期间引导应用，以及引导 plunker 中的范例。

@angular/http - Angular 的 HTTP 客户端。

@angular/router - 路由器。

@angular/upgrade - 一组用于升级 Angular 1 应用的工具。

system.js - 是一个动态的模块加载器， 与 ES2015 模块 规范兼容。 还有很多其它选择，比如广受欢迎的 webpack 。 SystemJS 被用在了我们的文档范例中。因为它能工作。

今后，应用程序很可能还会需要更多的包，比如 HTML 控件、主题、数据访问，以及其它多种工具。

填充 (Polyfill) 包
在应用程序的运行环境中， Angular 需要某些 填充库 。 我们通过特定的 npm 包来安装这些填充库， Angular 本身把它列在了package.json 中的 peerDependencies 区。

但我们必须把它列在我们 package.json 文件的 dependencies 区。

查看下面的“ 为什么用 peerDependencies? ”，以了解这项需求的背景。

core-js - 为全局上下文 (window) 打的补丁，提供了 ES2015(ES6) 的很多基础特性。 我们也可以把它换成提供了相同内核 API 的其它填充库。 一旦所有的“主流浏览器”都实现了这些 API ，这个依赖就可以去掉了。

reflect-metadata - 一个由 Angular 和 TypeScript 编译器共享的依赖包。 开发人员需要能单独更新 TypeScript 包，而不用升级 Angular 。这就是为什么把它放在本应用程序的依赖中，而不是 Angular 的依赖中。

rxjs - 一个为 可观察对象 (Observable) 规范 提供的填充库，该规范已经提交给了 TC39 委员会，以决定是否要在 JavaScript 语言中进行标准化。 开发人员应该能在兼容的版本中选择一个喜欢的 rxjs 版本，而不用等 Angular 升级。

zone.js - 一个为 Zone 规范 提供的填充库，该规范已经提交给了 TC39 委员会，以决定是否要在 JavaScript 语言中进行标准化。 开发人员应该能在兼容的版本中选择一个喜欢的 zone.js 版本，而不用等 Angular 升级。

其它辅助库
angular-in-memory-web-api - 一个 Angular 的支持库，它能模拟一个远端服务器的 Web API ，而不需要依赖一个真实的服务器或发起真实的 HTTP 调用。 对演示、文档范例和开发的早期阶段 ( 那时候我们可能还没有服务器呢 ) 非常有用。 请到 Http 客户端 一章中了解更多知识。

bootstrap - bootstrap 是一个广受欢迎的 HTML 和 CSS 框架，可用来设计响应式网络应用。 有些文档中的范例使用了 bootstrap 来强化它们的外观。

devDependencies

列在 package.json 文件中 devDependencies 区的包会帮助我们开发该应用程序。 我们不用把它们部署到产品环境的应用程序中——虽然这样做也没什么坏处。

concurrently - 一个用来在 OS/X 、 Windows 和 Linux 操作系统上同时运行多个 npm 命令的工具

lite-server - 一个轻量级、静态的服务器， 由 John Papa 开发和维护。对使用到路由的 Angular 程序提供了很好的支持。

typescript - TypeScript 语言的服务器，包含了 TypeScript 编译器 tsc 。

@types/* - “ TypeScript 定义”文件管理器。 要了解更多，请参见 TypeScript 配置 页。

为什么使用 peerDependencies ？

在“快速起步”的 package.json 文件中，并没有 peerDependencies 区。 但是 Angular 本身在 它自己的 package.json 中有， 它对我们的应用程序有重要的影响。

它解释了为什么我们要在“快速起步”的 package.json 文件中加载这些 填充库 (polyfill) 依赖包， 以及为什么我们在自己的应用中会需要它们。

然后是对 平级依赖 (peer dependencies) 的简短解释。

每个包都依赖其它的包，比如我们的应用程序就依赖于 Angular 包。

两个包， "A" 和 "B" ，可能依赖共同的第三个包 "C" 。 "A" 和 "B" 可能都在它们的 dependencies 中列出了 "C" 。

如果 "A" 和 "B" 依赖于 "C" 的不同版本 ("C1" 和 "C2") 。 npm 包管理系统也能支持！ 它会把 "C1" 安装到 "A" 的 node_modules 目录下给 "A" 用，把 "C2" 安装到 "B" 的 node_modules 目录下给 "B" 用。 现在， "A" 和 "B" 都有了它们自己的一份 "C" 的复本，它们运行起来也互不干扰。

但是有一个问题。包 "A" 可能只需要 "C1" 出现就行，而实际上并不会直接调用它。 "A" 可能只有当 每个人都使用 "C1" 时 才能正常工作。如果程序中的任何一个部分依赖了 "C2" ，它就会失败。

要想解决这个问题， "A" 就需要把 "C1" 定义为它的 平级依赖 。

在 dependencies 和 peerDependencies 之间的区别大致是这样的：

dependency 说：“我需要这东西 对我 直接可用。”

peerDependency 说：“如果你想使用我，你得先确保这东西 对你 可用”

Angular 就存在这个问题。 因此， Angular 的 package.json 中指定了一系列 平级依赖 包， 把每个第三方包都固定在一个特定的版本上。

我们必须自己安装 Angular 的 peerDependencies 。
当 npm 安装那些在 我们的 dependencies 区指定的包时， 它也会同时安装上在 那些包 的 dependencies 区所指定的那些包。 这个安装过程是递归的。

但是在 npm 的第三版中， 它不会 安装列在 peerDependencies 区的那些包。

这意味着，当我们的应用程序安装 Angular 时， npm 将不会自动安装列在 Angular 的 peerDependencies 区的那些包

幸运的是， npm 会在下列情况下给我们警告： (a) 当任何 平级依赖 缺失时或 (b) 当应用程序或它的任何其它依赖安装了与 平级依赖 不同版本的包时。

这些警告可以避免因为版本不匹配而导致的意外错误。 它们让我们可以控制包和版本的解析过程。

我们的责任是，把所有 平级依赖 包都 列在我们自己的 devDependencies 中 。

PEERDEPENDENCIES 的未来

Angular 的填充库依赖只是一个给开发人员的建议或提示，以便它们知道 Angular 期望用什么。 它们不应该像现在一样是硬需求，但目前我们也不知道该如何把它们设置为可选的。

不过，有一个 npm 的新特性申请，叫做“可选的 peerDependencies ”，它将会允许我们更好的对这种关系建模。 一旦它被实现了， Angular 将把所有填充库从 peerDependencies 区切换到 optionalPeerDependencies 区。
