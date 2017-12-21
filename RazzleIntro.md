## 什么是同构：

> * 客户端渲染：页面在 JavaScript，CSS 等资源文件加载完毕后开始渲染，路由为客户端路由，也就是我们经常谈到的 SPA（Single Page Application）。
> * 服务端渲染：页面由服务端直接返回给浏览器，路由为服务端路由，URL 的变更会刷新页面，原理与 ASP，PHP 等传统后端框架类似。
> * 同构：英文表述为 Isomorphic 或 Universal，即编写的 JavaScript 代码可同时运行于浏览器及 Node.js 两套环境中，用服务端渲染来提升首屏的加载速度，首屏之后的路由由客户端控制，即在用户到达首屏后，整个应用仍是一个 SPA。

简而言之，同构是服务端直出和客户端渲染的结合

---

## 同构的优点：
1. SEO更友好。
2. 整个页面级别的应用会使得浏览器在解析dom完成之后马上有东西可以渲染,减少渲染时间（首屏优化）。
3. 服务端和客户端维护一份代码就行了。
4. 开源福利：React16的[发布](https://reactjs.org/blog/2017/09/26/react-v16.0.html)通过重写了用于服务端渲染的renderToString函数，将渲染速度提升至v15的3倍。
5. 等等

当然，同构也没有这么好，具体的的选择还是看业务的，权衡开发(迁移)成本，性能影响等等诸多因素。

---

## 那么问题来了:)
如果，我尝试下 **React服务端渲染**，但又不想自己一开始就纠结于较繁琐的配置呢？

很多人的开发都会选用一个现有的脚手架开始，那么如何选用一个脚手架呢？

---

### 关于一个框架的脚手架，在网上经常看到开发者这样说：
> I'm looking for a very simple starter pack... I don't need all the hoopla.

的确，对一个脚手架项目而言，它需要有所有你想要的，不需要有你不想要的。

react官方的脚手架create-react-app的README中提到 **现阶段不支持直接提供服务端渲染**。

### 那么有哪些支持同构渲染的脚手架呢？

比如这些：
* [next.js](https://github.com/zeit/next.js)
* [react-server](https://github.com/redfin/react-server)
* [beidou](https://github.com/alibaba/beidou)
* [razzle](https://github.com/jaredpalmer/razzle)
* ...

这些脚手架各有各的特点，有的依赖多，有的依赖少，有的性能好，有的针对某一个痛点解决...

## 下面隆重介绍今天的主角 ———— [razzle](https://github.com/jaredpalmer/razzle):
razzle 是一个把所有于服务端渲染相关的繁琐配置抽象成了单独的一个依赖，给你类似于create-react-app的开发体验，但是把剩下的架构决策权，比如 框架选用，路由系统的选择、数据获取方式全都交给了开发者自己，充分符合上面说的 `have everything you need and nothing you don't.`

razzle 和上述提到的其他支持同构渲染的框架的 ***最大不同*** 在于他能过抽象依赖，能够提供类似<code>create-react-app</code>的开发体验，这就意味了给了开发者很大的自由度去选择自己顺手的，自己看得上眼的react生态里的库，razzle提供丰富的examples，帮助开发者能够快速的结合一些流行的成熟的库，比如用typescript进行开发，通过结合react-redux做状态管理，比如通过结合react-router做路由系统，通过结合react-loadable做到组件级别的代码分割和懒加载等等很多。

#### razzle 的理念决定了它不只只支持React，还支持Reason,Elm,Vue,Angular,和未来的新框架:)

项目的主要的优点有：
1. 开发环境模块热替换，无需重启就可以看到效果
2. 你最喜欢的ES6 支持
3. 与create-react-app 相同的 css 设置
4. 很多框架的支持
5. 默认Jest
6. 零配置服务端渲染

---

## 关于同构有一些误区，列几个熟悉的：
1. 同构性能没有客户端渲染好？网络流量高峰的时候，转到客户端渲染并不会起很大作用。ssr在服务端的渲染其实是非常快的，尽管这里提供不了精确的数据支持，但是看了很多博客上都提到过这种观点。

2. 同构容易引起内存泄漏？其实并不是，只要注意不要盲目的在定时的函数体中向全局的数组push东西等等，注意组建生命周期componentDidmount中放置服务端执行不了的代码，并且注意在用一些如window变量前先进行判断就好，并不是很容易导致内存泄漏。

---

理解还不是很成熟，希望能与大家交流讨论。
笔者是razzle的项目使用者，受益者，希望能让更多的人看到这个项目，未来一起让他更好。

## 关于同构的一些其他文章，也是本文的很多参考：
[What is an isomorphic application?](https://www.lullabot.com/articles/what-is-an-isomorphic-application)
[D2 - 打造高可靠与高性能的React同构解决方案](https://zhuanlan.zhihu.com/p/32124393)
[Here’s Why Client-side Rendering Won](https://medium.freecodecamp.org/heres-why-client-side-rendering-won-46a349fadb52)
[服务端渲染与 Universal React App](https://zhuanlan.zhihu.com/p/30580569)