---
title: 插件
---

>How do I use a plugin?

> 如何使用插件？

在命令行中使用
--------------------------------------

If you are using lessc, the first thing you need to do is install that plugin. We recommend the plugin starts with "less-plugin" though that isn't required. For the clean-css plugin you would install with

如果你使用 lessc，你需要做的第一件事情就是安装插件。我们推荐插件的以"less-plugin"开头，但这不是必要的。如果想使用 clean-css 插件，你应该这样子安装：

```
npm install less-plugin-clean-css
```

To use the plugin, if you specify a unrecognised option, we attempt to load that, for example

在使用插件过程中，如果指定了一个非默认的选项，我们将尝试加载它，例如：

```
lessc --clean-css="advanced"
```

Will use the plugin you just installed. You can also be more direct, for example

我们将使用你已经安装的插件。你也可以更直接地指定插件，例如：

```
lessc --plugin=path_to_plugin=options
```

在代码中使用插件
----------------------

In Node, require the plugin and pass it to `less` in an array as an option plugins. E.g.

在 Node 中，插件通过数组的形式传递给 `less` ，例如：

```js
var myPlugin = require("my-plugin");
less.render(myCSS, { plugins: [myPlugin] })
   .then(function(output) {
    },
    function(error) {
    });
```

在浏览器中使用
-------------------

Plugin authors should provide a javascript file, just include that in the page *before* the less.js script.

插件的作者应该提供一个 javascript 文件，并且必须在 less.js 脚本**之前**引入。

```html
<script src="plugin.js"></script>
<script>
less = { 
    plugins: [plugin]
};
</script>  
<script src="less.min.js"></script>
```

Less 插件列表
--------------------

> Available Less plugins. Find more at [GitHib](https://github.com/search?q=topic%3Aless-plugin&type=Repositories) and [NPM Registry](https://www.npmjs.com/search?q=%22less-plugin%22) 

> 可用的 Less 插件列表。可以在 [GitHib](https://github.com/search?q=topic%3Aless-plugin&type=Repositories) 和 [NPM Registry](https://www.npmjs.com/search?q=%22less-plugin%22) 上找到更多插件。

#### Postprocessor/Feature Plugins
| | |
|---|---|
| [Autoprefixer](https://github.com/less/less-plugin-autoprefix) | Add vendor prefixes
| [CSScomb](https://github.com/bassjobsen/less-plugin-csscomb/) | Beautify/format
| [clean-css](https://github.com/less/less-plugin-clean-css) | Compress/minify
| [CSSWring](https://github.com/bassjobsen/less-plugin-csswring) | Compress/minify
| [css-flip](https://github.com/bassjobsen/less-plugin-css-flip) | Generate left-to-right (LTR) or right-to-left (RTL) CSS
| [functions](https://github.com/seven-phases-max/less-plugin-functions) | Write custom Less functions in Less itself
| [group-css-media-queries](https://github.com/bassjobsen/less-plugin-group-css-media-queries) | Group CSS media queries
| [inline-urls](https://github.com/less/less-plugin-inline-urls) | Convert `url()` to a call to `data-uri()`
| [lesshint](https://github.com/lesshint/lesshint) | Lint your Less
| [lists](https://github.com/seven-phases-max/less-plugin-lists) | Lists/arrays manipulation (incl. loops)
| [pleeease](https://github.com/bassjobsen/less-plugin-pleeease) | Postprocess using pleeease
| [rtl](https://github.com/less/less-plugin-rtl) | Reverse from ltr to rtl
| [variables-output](https://github.com/Craga89/less-plugin-variables-output) | Export top-level variables to a JSON file

#### Preprocessors
| | |
|---|---|
| [sass2less](https://github.com/mediafreakch/less-plugin-sass2less) | Import and convert Sass/SCSS files into your Less code (incl. variables, mixins and more)

#### Import Plugins
| | |
|---|---|
| [bower-resolve](https://github.com/Mercateo/less-plugin-bower-resolve) | Import from a Bower package
| [glob](https://github.com/just-boris/less-plugin-glob) | Globbing support in Less imports
| [npm-import](https://github.com/less/less-plugin-npm-import) | Import from npm packages
| [resolve-blocks](https://github.com/Dalee/less-plugin-resolve-blocks) | Going up a tree to find specified component

#### Function Libraries
| | |
|---|---|
| [advanced-color-functions](https://github.com/less/less-plugin-advanced-color-functions/) | Functions to find more contrast colors
| [cubehelix](https://github.com/bassjobsen/less-plugin-cubehelix) | A `cubehelix` function
| [lists](https://github.com/seven-phases-max/less-plugin-lists) | Lists/arrays manipulation functions
| [urlencode](https://github.com/calvinjuarez/less-plugin-urlencode) | URL Encode function
| [util](https://github.com/FaberVitale/less-plugin-util) | A set of utility functions

#### Framework Importers
| | |
|---|---|
| [Bootstrap](https://github.com/bassjobsen/less-plugin-bootstrap/) | Bootstrap
| [Cardinal](https://github.com/bassjobsen/less-plugin-cardinal) | Cardinal
| [Flexbox Grid](https://github.com/bassjobsen/less-plugin-flexboxgrid)  | [Flexbox Grid](http://flexboxgrid.com/)
| [Flexible Grid System](https://github.com/bassjobsen/less-plugin-flexiblegs) | [Flexible Grid System](http://flexible.gs/)
| [Ionic](https://github.com/bassjobsen/less-plugin-ionic) | Ionic
| [Lesshat](https://github.com/bassjobsen/less-plugin-lesshat/) | Lesshat
| [Skeleton](https://github.com/bassjobsen/less-plugin-skeleton) | Skeleton

致插件开发者
--------------------------

Less supports some entry points that allow an author to integrate with it. We may add some more in the future.

Less 为集成插件的开发者提供了一些入口。我们将在未来添加更多的入口。

The plugin itself has a very simple signature, like this

插件本身有一个简单的签名，例如：

```js
{
    install: function(less, pluginManager) {
    },
    minVersion: [2, 0, 0] /* optional */
}
```
So, the plugin gets the `less` object, which in v2 has more classes on it (making it easy to extend), a plugin manager which provides some hooks to add visitors, file managers and post processors.

因此，插件能够获取到 `less` 对象，在 V2 中有不同的类型，（这将让它更好地被扩展）。插件管理将提供一些钩子函数、访问对象、文件管理器和后处理器。

If your plugin supports `lessc`, there are a few more details and the signature looks like this

如果你的插件支持 `lessc`，它的细节和签名类似这样：

```js
{
    install: function(less, pluginManager) {
    },
    setOptions: function(argumentString) { /* optional */
    },
    printUsage: function() { /* optional */
    },
    minVersion: [2, 0, 0] /* optional */
}
```
The additions are the `setOptions` function which passes the string the user enters when specifying your plugin and also the `printUsage` function which you should use to explain your options and how the plugin works.

添加的 `setOptions` 函数，它接收的是用户调用插件时传递进来的输入字符串。同时，你需要在 `printUsage` 中解释你的选项的意义，并告诉插件如何工作。

Here are some example repos showing the different plugin types:

下面是一些参考的不同类型插件的仓库：
 - post-processor: https://github.com/less/less-plugin-clean-css
 - visitor: https://github.com/less/less-plugin-inline-urls
 - file-manager: https://github.com/less/less-plugin-npm-import

Note: Plugins are different from creating a version of less for a different environment but they do have similarities, for example node provides 2 file managers by default and browser provides one and that is the main step in getting less to run within a specific environment. The plugin allows you to add file managers.

注意：创建相同版本的 less 不同的运行环境的插件的是不一样的，但是他们是相似的。例如，运行于 node 环境的会默认提供两个文件管理器，而运行于浏览器的只提供一个。不同的部分就是 Less 在特定环境下运行的主要步骤。这个插件允许你添加文件管理器。
