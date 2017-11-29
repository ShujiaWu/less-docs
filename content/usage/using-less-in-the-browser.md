---
title: 在浏览器中使用 Less
---

We recommend using Less in the browser only for development or when you need to dynamically compile Less code and cannot do it serverside.
This is because less.js is a large javascript file and compiling Less before the user can see the page means a delay for the user. In addition,
consider that mobile devices will compile slower. For development consider if using a watcher and live reload (e.g. with grunt or gulp) would
be better suited.

如果你不能在服务端动态编译代码时，我们推荐在开发模式下的浏览器中使用less。
因为 less.js 是一个比较大的 js 文件，并且在用户看到页面样式之前编译 less，这意味着对于用户会有延迟。
另外，考虑到移动设备上编译速度会更慢。如果使用 watcher 和 live reload （如使用 grunt 或 gulp）会更适合开发。

To use Less in the browser, you firstly need to include the less.js script.

在浏览器中使用 Less，首先需要包含 less.js 脚本。

```html
<!-- Here: include any Less plugin scripts, any required browser shims and optionally set less = any options  -->
<script src="less.js"></script>
```

This will find any Less style tags on the page

他会在页面中寻找 less 样式的标签

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

and create style tags with the compiled css synchronously.

同时创建编译好的 css 样式标签。

### 1. 设置选项

You can set options either programmatically, by setting them on a `less` object before the script tag - this then effects all initial link tags and programmatic usage of Less.

你可以在脚本标签之前以编程化的方式设置选项，这将影响所有的初始化的链接标签和 less 的编程化使用。

```html
<script>
  less = {
    env: "development"
  };
</script>
<script src="less.js"></script>
```

The other way is to specify the options on the script tag, e.g.

另外一种方式是在脚本标签上指定选项，例如：

```html
<script>
  less = {
    env: "development"
  };
</script>
<script src="less.js" data-env="development"></script>
```

And you can also do this on link tags to override certain settings (some less settings like verbose are global and can not be overridden).

你也可以在 link 标签上设置重写某一设置。（某些 less 设置如 verbose 是全局的，是不能被重写的）

```html
<link data-dump-line-numbers="all" data-global-vars='{ "myvar": "#ddffee", "mystr": "\"quoted\"" }' rel="stylesheet/less" type="text/css" href="less/styles.less">
```

The important points for attribute options are..

 - importance level: window.less < script tag < link tag
 - data attributes names are not camelCase (e.g logLevel -> data-log-level)
 - link tag options are just render time options (e.g verbose, logLevel ... are not supported)
 - non-string data attributes values should be JSON valid (e.g use double quotes instead of single quotes like in `data-global-vars='{ "myvar": "#ddffee", "mystr": "\"quoted\"" }'`)

对于属性选项的几点重要说明：

- 权重：window.less < script tag < link tag
- data属性的名称不是驼峰式的（例如：logLevel -> data-log-level）
- link 标签选项只在渲染的时候有效。(例如 verbose, logLevel ... 是不支持的)
- 非字符串类型的属性值必须是合法的JSON（例如：在单引号内部使用双引号如`data-global-vars='{ "myvar": "#ddffee", "mystr": "\"quoted\"" }'`）

### 2. 监视模式
To enable Watch mode, option `env` must be set to `development`. Then AFTER the less.js file is included, call `less.watch()`, like this:

如果要启用监视模式，`env` 选项必须被设置为 `development`，然后在引入的 less.js 后面调用 `less.watch()`，例如：

```html
<script>less = { env: 'development'};</script>
<script src="less.js"></script>
<script>less.watch();</script>
```

Alternatively, you can enable Watch mode temporarily by appending `#!watch` to the URL.

另外，你也可以在 URL 后面附加 `#!watch` 开启监视模式

### 3. 修改变量
Enables run-time modification of Less variables. When called with new values, the Less file is recompiled without reloading. Simple basic usage:

开启 Less 变量的实时修改模式。当使用一个新值调用时，Less 文件会重新编译而不重新加载。简单的使用如下：

```js
less.modifyVars({
  '@buttonFace': '#5B83AD',
  '@buttonText': '#D9EEF2'
});
```

### 4. 调试
It is possible to output rules in your CSS which allow tools to locate the source of the rule.

这使得调试工具可以通过输出的 CSS 规则定位到源文件的规则。

Either specify the option `dumpLineNumbers` as above or add `!dumpLineNumbers:mediaquery` to the url.

要么在上面的设置中加入 `dumpLineNumbers` 选项，要么把 `!dumpLineNumbers:mediaquery` 添加到 url 末尾。

You can use the `mediaquery` option with [FireLESS](https://addons.mozilla.org/en-us/firefox/addon/fireless/) (it is identical to the SCSS media query debugging format). Also see [FireLess and Less v2](http://bassjobsen.weblogs.fm/fireless-less-v2/). The `comment` option can be used to display file information and line numbers in the inline compiled CSS code.

你可以使用 [FireLESS](https://addons.mozilla.org/en-us/firefox/addon/fireless/) 的 `mediaquery` 选项（它与SCSS媒体查询调试格式相同）。或者[FireLess and Less v2](http://bassjobsen.weblogs.fm/fireless-less-v2/)。使用 `comment` 选项可以在内联编译的 CSS 代码中显示文件信息和行号。

### 5. 选项

Set options in a global `less` object **before** loading the less.js script:

在 less.js 脚本**之前**设置一个包含选项的全局 `less` 对象：

``` html
<!-- set options before less.js script -->
<script>
  less = {
    env: "development",
    logLevel: 2,
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    globalVars: {
      var1: '"string value"',
      var2: 'regular value'
    },
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```

#### 5.1 async
Type: `Boolean`

Default: `false`

Whether to request the import files with the async option or not. See [fileAsync](#using-less-in-the-browser-fileasync).

异步导入所有的文件不管是否制定了async 选项。详见[fileAsync](#using-less-in-the-browser-fileasync)。

#### 5.2 dumpLineNumbers
Type: `String`
Options: `''`| `'comments'`|`'mediaquery'`|`'all'`
Default: `''`

When set, this adds source line information to the output css file. This helps you debug where a particular rule came from.

通过设置，可以将源文件的行号信息附加到输出的 CSS 中。这将帮助你调试来自特定文件的规则。

The `comments` option is used for outputting user-understandable content, whilst `mediaquery` is for use with a firefox extension which parses the css and extracts the information.

使用 `comments` 选项输出用户可以理解的内容，`mediaquery` 用于火狐浏览器转换 CSS 和提供额外信息的扩展组件。

In the future we hope this option to be superseded by sourcemaps.

我们希望将来这个特性能够被 sourcemaps 取代。

#### 5.3 env
Type: `String`
Default: 依赖于页面的 URL

Environment to run may be either `development` or `production`.

运行的环境可以使 `development` 或者 `production`。

In production, your css is cached in local storage and information messages are not output to the console.

在生产环境，你的 CSS 缓存在本地存储中，信息和消息不会在控制台输出。

If the document's URL starts with `file://` or is on your local machine or has a non standard port, it will automatically be set to `development`.

如果文档的 URL 以 `file://` 开头，或者存储于本地机器，或者是一个非标准的端口，它将会自动被设置为 `development` 。

e.g.
```js
less = { env: 'production' };
```

#### 5.4 errorReporting
Type: `String`

Options: `html`|`console`|`function`

Default: `html`

Set the method of error reporting when compilation fails.

设置编译失败时以哪种方式报告错误。

#### 5.5 fileAsync
Type: `Boolean`

Default: `false`

Whether to request the import asynchronously when in a page with a file protocol.

是否在一个带有文件协议的页面同步请求导入的文件。

#### 5.6 functions
Type: `object`

User functions, keyed by name.

用户函数，以名称为键。

e.g.
```js
less = {
    functions: {
        myfunc: function() {
            return new(less.tree.Dimension)(1);
        }
    }
};
```

and it can be used like a native Less function e.g.

它可以像本地 Less 函数一样使用，例如：

```less
.my-class {
  border-width: unit(myfunc(), px);
}
```

#### 5.7 logLevel
Type: `Number`

Default: 2

The amount of logging in the javascript console. Note: If you are in the `production` environment you will not get any logging.

打印在 javascript 控制台的信息数量。注意如果实在生产环境将不会有任何输出。

```bash
2 - Information and errors
1 - Errors
0 - Nothing
```

#### 5.8 poll
Type: `Integer`

Default: `1000`

The amount of time (in milliseconds) between polls while in watch mode.

监视模式下轮训的时间间隔（毫秒）。

#### 5.9 relativeUrls
Type: `Boolean`

Default: `false`

Optionally adjust URLs to be relative. When false, URLs are already relative to the entry less file.

选择性地将 URL 转换成相对路径。如果为 false，URL 的地址相对于入口的 less 文件。

#### 5.10 globalVars
Type: `Object`

Default: `undefined`

List of global variables to be injected into the code. Keys of the object are variables names, values are variables values. Variables of "string" type must explicitly include quotes if needed.

注入到代码中的全局变量列表。对象的键是变量的名称，值是变量的值，字符串类型的变量的值如果需要则引号则必须包含引号。

E.g.

```js
less.globalVars = { myvar: "#ddffee", mystr: "\"quoted\"" };
```

This option defines a variable that can be referenced by the file. Effectively the declaration is put at the top of your base Less file, meaning it can be used but it also can be overridden if this variable is defined in the file.

这个选项定义了可以被文件引用的变量。有效的变量声明将被放置于基础 less 文件的最顶部，意味着如果在文件中定义了相同的变量，它将会被重写。

#### 5.11 modifyVars
Type: `Object`

Default: `undefined`

Same format as [globalVars](#using-less-in-the-browser-globalvars).

格式和[globalVars](#using-less-in-the-browser-globalvars)一样。

As opposed to the [globalVars](#using-less-in-the-browser-globalvars) option, this puts the declaration at the end of your base file, meaning it will override anything defined in your Less file.

与[globalVars](#using-less-in-the-browser-globalvars)选项的功能相反。这将声明的变量放置于基础文件的末尾，这意味着任何你在 less 文件中定义的同名变量会被重写。

#### 5.12 rootpath
Type: `String`

Default: `false`

A path to add on to the start of every URL resource.

被添加到每一个 URL 资源前面的路径。

#### useFileCache
Type: `Boolean`

Default: `true` (V2 之前默认值是 `false`)

Whether to use the per session file cache. This caches less files so that you can call modifyVars and it will not retrieve all the less files again.
If you use the watcher or call refresh with reload set to true, then the cache will be cleared before running.

每一个会话是否使用缓存。这将缓存 less 文件，这样就可以使用modifyVars，并且不会检索所有的 less 文件。如果你使用了监视器并且将重载后刷新设置为true，那么在运行之前缓存将会被清楚。
