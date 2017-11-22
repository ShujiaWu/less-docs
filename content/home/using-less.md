---
title: Server-side Usage
---

> Less can be used on the command line via npm, downloaded as a script file for the browser or used in a wide variety of third party tools. See the [Usage]({{resolve 'usage'}}) section for more
detailed information.

> Less 可以通过 npm 在命令行下使用，或者通过脚本文件在客户端浏览器上使用，或者在其他第三方工具中使用。更多信息请在[使用说明]({{resolve 'usage'}})中查看。

## 安装 Installation

The easiest way to install Less on the server, is via npm, the [node.js](http://nodejs.org/) package manager, as so:

在服务器上安装 Less 最简单的方法是通过 [node.js](http://nodejs.org/) 的 npm 包管理工具进行安装，安装方法如下：

```bash
$ npm install -g less
```

## 在命令行中使用 Command-line Usage

Once installed, you can invoke the compiler from the command-line, as such:

一旦安装完成，你可以在命令行中调用编译命令，如下：

```bash
$ lessc styles.less
```

This will output the compiled CSS to `stdout`. To save the CSS result to a file of your choice use:

上面命令将编译好的 CSS 输出到`标准输出流`中。如果想要将编译后的 CSS 结果保存到文件，你可以使用下面的命令：

```bash
$ lessc styles.less styles.css
```

To output minified CSS you can use the [`clean-css` plugin](https://github.com/less/less-plugin-clean-css). When the plugin is installed, a minified CSS output is specified with `--clean-css` option: 

如果想要输出压缩后的 CSS 文件，你可以使用 [`clean-css` 插件](https://github.com/less/less-plugin-clean-css)。如果你已经安装了该插件，你可以通过在命令中加入 `--clean-css` 选项来压缩输出：

```bash
$ lessc --clean-css styles.less styles.min.css
```

To see all the command line options run `lessc` without parameters or see [Usage]({{resolve 'usage'}}).

你可以通过运行没有使用任何参数 `lessc` 的命令来查看所有的参数，或者查看[使用说明]({{resolve 'usage'}})。

## 在代码中使用 Usage in Code

You can invoke the compiler from node, as such:

你可以在 node 程序中调用编译器：

```js
var less = require('less');

less.render('.class { width: (1 + 1) }', function (e, output) {
  console.log(output.css);
});
```

which will output

上面的代码将输出以下结果：

```css
.class {
  width: 2;
}
```

## 配置 Configuration

You may pass some options to the compiler:

你可以传递部分选项参数给编译器：

```js
var less = require('less');

less.render('.class { width: (1 + 1) }',
    {
      paths: ['.', './lib'],  // Specify search paths for @import directives
      filename: 'style.less', // Specify a filename, for better error messages
    },
    function (e, output) {
       console.log(output.css);
    });
```

See [Usage]({{resolve 'usage'}}) for more information.

阅读 [使用说明]({{resolve 'usage'}}) 获取更多信息。

## 第三方工具 Third Party Tools

See the [Usage]({{resolve 'usage'}}) section for details of other tools.

阅读 [使用说明]({{resolve 'usage'}}) 获取更多关于其他第三方工具的相关信息。

<!-- # Command-line with Rhino
> Each Less release contains also rhino-compatible version.

Command line rhino version requires two files:
* less-rhino-&lt;version&gt;.js - compiler implementation,
* lessc-rhino-&lt;version&gt;.js - command line support.

Command to run the compiler:
````
java -jar js.jar -f less-rhino-<version>.js lessc-rhino-<version>.js styles.less styles.css
````

This will compile styles.less file and save the result to styles.css file. The output file parameter is optional. If it is missing, less will output the result to `stdout`.-->

# 客户端使用 Client-side Usage

> Using less.js in the browser is great for development, but it's not recommended for production

> 在客户端中使用 less.js 适用于开发阶段，但不建议在生产环境中使用。

Client-side is the easiest way to get started and good for developing with Less, but in production, when performance and reliability is important, _we recommend pre-compiling using node.js or one of the many third party tools available_.

在客户端浏览器中使用 Less 是开始学习使用、开发阶段最简单的方式，但是在生产环境中性能和可靠性是非常重要的，_因此我们推荐使用 node.js 或者可用的第三方工具进行预编译_。

To start off, link your `.less` stylesheets with the `rel` attribute set to "`stylesheet/less`":

首先，在将你的 `.less` 使用 `<link>` 标签链接到页面中，并将 `rel` 属性设置为 "`stylesheet/less`"：

```html
<link rel="stylesheet/less" type="text/css" href="styles.less" />
```

Next, [download less.js](https://github.com/less/less.js/archive/master.zip) and include it in a `<script></script>` tag in the `<head>` element of your page:

接下来，[下载 less.js](https://github.com/less/less.js/archive/master.zip) 并把它引入到你页面的 `<head>` 元素的 `<script></script>` 标签中：

```html
<script src="less.js" type="text/javascript"></script>
```

### 提示 Tips

* Make sure you include your stylesheets **before** the script.
* When you link more than one `.less` stylesheet each of them is compiled independently. So any variables, mixins or namespaces you define in a stylesheet are not accessible in any other.
* Due to the same origin policy of browsers loading external resources requires [enabling CORS](http://enable-cors.org/)


* 确保你的样式是在脚本**之前**引入。
* 当你引入多个 `.less` 样式的时候，他们之间是彼此独立的。所以任何你在样式文件中定义的变量、混合（mixins）或者命名空间都不能互相访问。
* 由于浏览器同源策略的关系，加载其他资源需要[启用 CORS](http://enable-cors.org/)。

## 浏览器参数 Browser Options

Options are defined by setting them on a global `less` object **before** the `<script src="less.js"></script>`:

通过在引入 `<script src="less.js"></script>` **之前**定义一个全局的 `less` 对象来更改配置参数

``` html
<!-- set options before less.js script -->
<script>
  less = {
    env: "development",
    async: false,
    fileAsync: false,
    poll: 1000,
    functions: {},
    dumpLineNumbers: "comments",
    relativeUrls: false,
    rootpath: ":/a.com/"
  };
</script>
<script src="less.js"></script>
```

Or for brevity they can be set as attributes on the script and link tags (requires JSON.parse browser support or polyfill).

或者通过设置 script 和 link 标签的属性进行局部更改。（需要浏览器支持 JSON.parse 或者使用 polyfill）

``` html
<script src="less.js" data-poll="1000" data-relative-urls="false"></script>
<link data-dump-line-numbers="all" data-global-vars='{ myvar: "#ddffee", mystr: "\"quoted\"" }' rel="stylesheet/less" type="text/css" href="less/styles.less">
```

Learn more about [Browser Options](usage/#using-less-in-the-browser-setting-options)

通过 [浏览器选项](usage/#using-less-in-the-browser-setting-options) 获取更多信息。
