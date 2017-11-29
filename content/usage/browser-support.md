---
title: 浏览器支持
---

Less only supports running on modern browsers (recent versions of Chrome, Firefox, Safari and IE). While it is possible to use Less on the client side in production, please be aware that there are performance implications for doing so (although the latest releases of Less are quite a bit faster). Also, sometimes cosmetic issues can occur if a JavaScript error occurs. This is a trade off of flexibility vs. speed. For the fastest performance possible for a static web site, we recommend compiling Less on the server side.

Less 只支持现代浏览器（最新版本的Chrome, Firefox, Safari 和 IE）。在生产环境中的客户端使用 Less 是可能的，但是请注意这将带来性能上的影响（虽然最新新版本的 Less 速度相当快）。另外，如果 JavaScript 发生错误，还会产生美观问题。这是对灵活性和速度的权衡。对于一个静态网站的最快性能，我们推荐在服务端编译 Less。

Note that PhantomJS does not currently implement `Function.prototype.bind` so you will require a es-5 shim for this function to run under PhantomJS (We use PhantomJS for tests and we append an es5-shim to make it work).

注意：PhantomJS 目前还没有实现 `Function.prototype.bind` ，所以在 PhantomJS 下调用这个函数你需要引入一个 es-5 的 shim 。（我们使用 PhantomJS 作为测试工具，并通过给它附加 es5-shim 使它能够正常工作。）

There are reasons to use client-side script in production, such as if you want to allow users to tweak variables which will affect the theme and you want to show it to them in real-time - in this instance a user is not worried about waiting for a style to update before seeing it.

在生产环境中使用客户端 less 是有理由的，如果你希望允许用户对影响主题的变量进行调整，并且实时地展示变化。在这个例子中，用户不用当心等待样式的变更。

If you need to run less.js in an older browser, please use an [es-5 shim](https://github.com/kriskowal/es5-shim) which will add the javascript features that less.js requires.

如果你想在一个较老的浏览器上使用 less.js ,请使用 [es-5 shim](https://github.com/kriskowal/es5-shim) 添加 less.js 需要的 javascript 特性。

In addition, if you use options as attributes on the script or link tags, you will require browser support for `JSON.parse` or an appropriate polyfill.

另外，如果你想在 script 或 link 标签上使用选项作为属性，你的浏览器必须支持 `JSON.parse` 或者使用恰当的 polyfill 。
