---
title: 编程方式使用说明
---

The main entry point into `less` is the `less.render` function. This takes the following format

`less` 的入口函数为 `less.render`。格式如下：

```js
less.render(lessInput, options)
    .then(function(output) {
        // output.css = string of css
        // output.map = string of sourcemap
        // output.imports = array of string filenames of the imports referenced
    },
    function(error) {
    });

// or...

less.render(css, options, function(error, output) {})
```

The options argument is optional. If you specify a callback then a promise will not be returned, where as if you do not specify a callback a promise will be given.
Under the hood, the callback version is used so that less can be used synchronously.

选项参数是可选的。如果你指定了回调函数，那么它将不会返回一个 promise ，如果你们有指定一个回调函数，那么它将返回一个 promise 。在这个钩子的作用下，使用回调的版本，可以异步使用 less。

If you wanted to render a file, you would first read it into a string (to pass to less.render) and then set the filename field on options to be the filename of the main file. less will handle all the processing of the imports.

如果你想渲染一个文件，你需要先将文件内容读取到一个字符串（然后传递给 less.render）并且在选项中设置文件名字段作为主文件的文件名。less 会处理所有的导入。

The `sourceMap` option is an object which enables you to set sub sourcemap options. Available sub options are: `sourceMapURL`,`sourceMapBasepath`,`sourceMapRootpath`,`outputSourceFiles` and `sourceMapFileInline`. Notice that the `sourceMap` option is not available for the less.js in browser compiler now.

`sourceMap` 选项允许你设置子 sourcemap 选项。可用的子选项有： `sourceMapURL`,`sourceMapBasepath`,`sourceMapRootpath`,`outputSourceFiles` 和 `sourceMapFileInline`。注意：`sourceMap` 在浏览器编译时是不可用的

```js
less.render(lessInput)
    .then(function(output) {
        // output.css = string of css
        // output.map = undefined
}
//,
less.render(lessInput, {sourceMap: {}})
    .then(function(output) {
        // output.css = string of css
        // output.map = string of sourcemap
}
//or,
less.render(lessInput, {sourceMap: {sourceMapFileInline: true}})
    .then(function(output) {
        // output.css = string of css \n /*# sourceMappingURL=data:application/json;base64,eyJ2ZXJ..= */
        // output.map = undefined
}
```

Previously we also recommended creating a less.Parser and then calling toCSS on the result. However this had 2 serious drawbacks - it meant that our parser was in fact tied to all of less and 2nd it meant that the toCSS call had to be synchronous.

在以前，我们也建议创建一个 less.Parser 并在结果调用 toCSS 。但是，这有两个缺陷 —— 这意味着事实上我们的转换器依赖所有的 less，第二是我们必须以同步的方式调用 toCSS 。

You can still get the less parse tree, but it requires more steps. You can see how this is done [in the render function](https://github.com/less/less.js/blob/master/lib/less/render.js) but we *do not* support using less in this way and may change this function in a minor release version bump (we will not break it in a patch release).

我们也可以获得 less 的转换树，但是这需要更多的步骤。你可以在 [in the render function](https://github.com/less/less.js/blob/master/lib/less/render.js) 中查看如何实现。但是我们不建议以这种方式使用 less ，或许会在一个小版本中改变这个功能。（我们不会在一个补丁版本中做出改变）

### 获取日志

You can add a log listener with the following code

你可以按一下代码添加日志监听器：

```js
less.logger.addListener({
    debug: function(msg) {
    },
    info: function(msg) {
    },
    warn: function(msg) {
    },
    error: function(msg) {
    }
});
```

Note: all functions are optional. An error will not be logged, but instead is passed back to the callback or promise in less.render

所有的函数都是可选的。错误将不会被记录，但是他会被传递给回调行数或者是 less.render 中的 promise 。
