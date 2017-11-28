---
title: 命令行使用说明
---

> Compile `.less` files to `.css` using the command line

> 使用命令行将 `.less` 文件编译成 `.css` 文件

<span class="warning">Heads up! If the command line isn't your thing, learn more about [GUIs for Less](#guis-for-less).</span>
<span class="warning">注意! 如果你不擅长使用命令行, 请阅读 [图形化 Less 编译器](#guis-for-less).</span>

### 1. 全局安装 `lessc`

Install with [npm](https://www.npmjs.org/)

使用 [npm](https://www.npmjs.org/) 安装。

```bash
npm install less -g
```

and then you will have the `lessc` command available globally. For a specific version (or tag) you can add `@VERSION` after our package name, e.g. `npm install less@1.6.2 -g`.

安装完成后你就可以在全局使用 `lessc`。 你可以在包名后面添加 `@VERSION` 指定版本安装的版本号，例如：`npm install less@1.6.2 -g`。

### 2. 在Node开发环境中安装

Alternatively if you don't use the compiler globally, you may be after

如果你没有在全局安装编译器，那么你可以这样做：

```bash
npm i less --save-dev
```

This will install the latest official version of lessc in your project folder, also adding it to the `devDependencies` in your project's `package.json`.

这在将你的工程项目中安装官方最新的 lessc ，并将它添加到项目工程中 `package.json` 的 `devDependencies`。

Note that a [caret version range][] will be automatically specified in `package.json`. This is good, as new minor releases of the latest version will be installable by npm.

注意, `package.json` 中[插入的版本范围][]会自动指定。这是非常好的，npm 会安装最新的版本。

#### 2.2 lessc 的 Beta 版本

Periodically, as new functionality is being developed, lessc builds will be published to npm, tagged as beta. These builds will _not_ be published as a `@latest` official release, and will typically have beta in the version (use `lessc -v` to get current version).

周期性地，当一个新的功能被开发出来，lessc 会编译并发布到 npm 中，并打上 beta 的标记。这些编译不会作为 `@latest` 的官方发布版本，通常只作为开发版本使用。（使用 `lessc -v` 获取当前的版本号）。

Since patch releases are non-breaking we will publish patch releases immediately and alpha/beta/candidate versions will be published as minor or major version upgrades (we endeavour since 1.4.0 to follow [semantic versioning]c).

由于补丁的发布是不间断的，我们会立即发布补丁版本。alpha/beta/candidate 版本会作为次要版本或者主要版本的升级。（我们从1.4.0开始进可能地遵循[语意版本](http://semver.org/)）

#### 2.3 安装一个未发布的lessc开发版本

If you want to install a bleeding-edge, unpublished version of lessc, follow the instructions for specifying a [git URL as a dependency][] and be sure to specify an actual commit SHA (not a branch name) as the `commit-ish`. This will guarantee that your project always uses that exact version of lessc.

如果你想安装一个前沿的、未发布的 lessc 版本, 遵循 [使用 git URL 作为依赖][] 的指南，并且确切指定 commit SHA （而不是branch name）作为 `commit-ish`， 这将保证你的工程使用特定的 less 版本。

The specified git URL may be that of the official lessc repo or a fork.

指定的 git URL 可以使官方的 less repo 或者一个 fork 。

[caret version range]: https://www.npmjs.org/doc/misc/semver.html#ranges
[git URL as a dependency]: https://npmjs.org/doc/json.html#Git-URLs-as-Dependencies

[插入的版本范围]: https://www.npmjs.org/doc/misc/semver.html#ranges
[使用 git URL 作为依赖]: https://npmjs.org/doc/json.html#Git-URLs-as-Dependencies
### 3. 在服务端和命令行使用

The binary included in this repository, `bin/lessc` works with [Node.js](http://nodejs.org/) on *nix, OS X and Windows.

仓库中的 二进制文件 `bin/lessc` 能够在 *nix, OS X 和 Windows 操作系统上运行。

**用法**: `lessc [option option=parameter ...] <source> [destination]`

### 4. 在命令行中使用

```bash
lessc [option option=parameter ...] <source> [destination]
```

If source is set to `-' (dash or hyphen-minus), input is read from stdin.

如果 source 被设置为 '-' (破折号 或者 减号)， 将以 stdin 作为输入。

#### 4.1 例子

```bash
# compile bootstrap.less to bootstrap.css
$ lessc bootstrap.less bootstrap.css

# compile bootstrap.less to bootstrap.css with strict math expressions
$ lessc -sm=on bootstrap.less bootstrap.css
```

### 5. Options

#### 5.1 Help

```bash
lessc --help
lessc -h
```

Prints a help message with available options and exits.

打印所有可用的可选项的帮助信息

#### 5.2 Include Paths

```bash
lessc --include-path=PATH1;PATH2
```

Sets available include paths. Separated by ':' or ';' on Windows.

设置可用的 include paths 。在 Windows 上使用 ':' 或 ';' 进行分隔。 

If the file in an `@import` rule does not exist at that exact location, less will look for it at the location(s) passed to this option. You might use this for instance to specify a path to a library which you want to be referenced simply and relatively in the less files.

如果在指定的位置不存在 `@import` 的文件，less 会在传递给选项的位置进行查找。你可以通过指定一个路径作为类库，简化文件在less中相对路径的引用。

In node, set a paths option

在 node 中设置 paths ：

```js
{ paths: ['PATH1', 'PATH2']  }
```

#### 5.3 Makefile

```bash
lessc -M
lessc --depends
```

#### 5.4 No Color

```bash
lessc --no-color
```

#### 5.5 No IE Compatibility

```bash
lessc --no-ie-compat
```

Currently only used for the data-uri function to ensure that images aren't created that are too large for the browser to handle.

目前只作用于 data-uri 函数，用于确保创建的图片不会太大以至于浏览器无法处理。

#### 5.6 禁用 JavaScript

```bash
lessc --no-js
```

#### 5.5 Lint

```bash
lessc --lint
lessc -l
```

Runs the less parser and just reports errors without any output.

运行 less 转换器，只输出错误信息，不输结果。

#### 5.6 Silent

```bash
lessc -s
lessc --silent
```

Stops any warnings from being shown.

不显示任何警告信息。

#### 5.7 Strict Imports

```bash
lessc --strict-imports
```

#### 5.8 允许从不安全的 HTTPS 导入

```bash
lessc --insecure
```

#### 5.9 获取版本号

```bash
lessc -v
lessc --version
```

#### 5.10压缩

*Deprecated*. Use [compression plugins](#plugins-postprocessor-feature-plugins) instead.

*已废弃*。使用 [压缩插件](#plugins-postprocessor-feature-plugins) 代替。

```bash
lessc -x
lessc --compress
```

Compress using built-in compression.

使用内嵌的压缩。

#### 5.11 Clean CSS
```bash
less --clean-css
```
In v2 of less, Clean CSS is no longer included as a direct dependency. To use `clean-css` with `lessc`, use the [`clean-css` plugin](https://github.com/less/less-plugin-clean-css).

在 less 的 v2 版本，Clean CSS 不再作为 less 的直接依赖。通过 [`clean-css` 插件](https://github.com/less/less-plugin-clean-css)来使用 `lessc` 的 `clean-css`。

#### 5.12 Source Map 输出的文件名

```bash
lessc --source-map
lessc --source-map=file.map
```

Tells Less to generate a sourcemap. If you have the sourcemap option without a filename it will use the source Less file name but with the extension map.

告诉 less 生成 sourcemap。 如果你在选项中指定 sourcemap 的文件名，那么 less 会使用 less 文件的文件名作为 sourcemap 的文件名，并以 map 为扩展名。

#### 5.13 Source Map Rootpath

```bash
lessc --source-map-rootpath=dev-files/
```

Specifies a rootpath that should be prepended to each of the less file paths inside the sourcemap and also to the path to the map file specified in your output css.

指定附加到 sourcemap 中每一个 less 文件的路径前面的 rootpath，同时指定输出的 css 的 map 文件的路径。

Because the basepath defaults to the directory of the input less file, the rootpath defaults to the path from the sourcemap output file to the base directory of the input less file.

因为 basepath 默认是 less 文件所在的路径，rootpath 默认是从 less 文件的 sourcemap 文件的输出目录到 less 文件所在目录的路径。

Use this option if for instance you have a css file generated in the root on your web server but have your source less/css/map files in a different folder. So for the option above you might have

如果你生成的 CSS 文件位于 web 服务器的根目录，但是你的源 less/css/map 文件在不同的目录，那么你就得像上面一样设置 source-map-rootpath。

```bash
output.css
dev-files/output.map
dev-files/main.less
```

#### 5.14 Source Map Basepath

```bash
lessc --source-map-basepath=less-files/
```

This is the opposite of the rootpath option, it specifies a path which should be removed from the output paths. For instance if you are compiling a file in the less-files directory but the source files will be available on your web server in the root or current directory, you can specify this to remove the additional `less-files` part of the path.

这与 rootpath 选项相反，它指定应该从输出路径中删除的路径。例如你在 less 文件的目录下编译，但是在你的服务器的根目录或者当前目录存在源文件，你可以移除附加在 less 文件的路径。

It defaults to the path to the input less file.

它默认是 less 文件所在的路径。

#### 5.15 Source Map Less Inline

```bash
lessc --source-map-less-inline
```

This option specifies that we should include all of the Less files in to the sourcemap. This means that you only need your map file to get to your original source.

这个选项指定我们将在 sourcemap 中宝航所有的 Less 文件。这意味着你只需要 map 文件就可以获得所有的源代码。

This can be used in conjunction with the map inline option so that you do not need to have any additional external files at all.

它可以跟 map inline 选择组合使用，这样你就不需要再附加其他的文件。

#### 5.16 Source Map Map Inline

```bash
lessc --source-map-map-inline
```

This option specifies that the map file should be inline in the output CSS. This is not recommended for production, but for development it allows the compiler to produce a single output file which in browsers that support it, use the compiled css but show you the non-compiled less source.

这个选项指定输出的 CSS 文件必须包含 map 文件。这在生产上是不推荐使用的，但在开发过程中允许生成一个浏览器支持的文件，它是编译后的 CSS，但你可以查看编译前的 less 源码。 

#### 5.17 Source Map URL

```bash
lessc --source-map-url=../my-map.json
```

Allows you to override the URL in the css that points at the map file. This is for cases when the rootpath and basepath options are not producing exactly what you need.

允许你重写指向 map 文件的 URL。这适用于 rootpath 和 basepath 选项不能满足生成所需要的情况时。

#### 5.18 Rootpath

```bash
lessc -rp=resources/
lessc --rootpath=resources/
```

Allows you to add a path to every generated import and url in your css. This does not affect Less import statements that are processed, just ones that are left in the output css.

允许添加一个路径到css中每一个生成的import 和 url。这不会影响已经被处理的 less 表达式，只会影响那些输出的 css 。

For instance, if all the images the css use are in a folder called resources, you can use this option to add this on to the URL's and then have the name of that folder configurable.

例如，css 中使用的图片都存放在一个叫 resources 的文件夹，你可以使用这个选项，添加 URL 地址，使得文件夹的名字可配置。

#### 5.19 Relative URLs

```bash
lessc -ru
lessc --relative-urls
```

By default URLs are kept as-is, so if you import a file in a sub-directory that references an image, exactly the same URL will be output in the css. This option allows you to re-write URL's in imported files so that the URL is always relative to the base imported file. E.g.

默认情况下，URL 是保持不变的。所以如果你引用了一个子目录的文件，文件中使用了一张图片，期望在 css 得到图片正确的 URL 地址。这个选项允许你重写导入文件中的 URL 地址，所以所有的 URL 地址都是相对于导入的文件。例如：

```less
# main.less
@import "files/backgrounds.less";
# files/backgrounds.less
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

this will output the following normally

正常情况下将输出：

```css
.icon-1 {
  background-image: url('images/lamp-post.png');
}
```

but with this option on it will instead output

但是如果使用了这个选项，那么将得到下面的输出：

```css
.icon-1 {
  background-image: url('files/images/lamp-post.png');
}
```

You may also want to consider using the data-uri function instead of this option, which will embed images into the css.

你也许会考虑使用 data-uri 函数代替这个选项，它会在 CSS 中包含图片。

#### 5.20 Strict Math

```bash
lessc -sm=on
lessc --strict-math=on
```

Defaults to Off.

默认是 off。

Without this option on Less will try and process all maths in your css e.g.

如果没有设置这个选项，Less 会尝试计算 CSS 中的所有数学运算，例如：

```less
.class {
  height: calc(100% - 10px);
}
```

will be processed currently.

将会被处理。

With strict math on, only maths that is inside un-necessary parenthesis will be processed. For instance.

在开启严格模式下，只有在非必要的括号内的数学运算才会被处理，例如：

```less
.class {
  width: calc(100% - ((10px  - 5px)));
  height: (100px / 4px);
  font-size: 1 / 4;
}
```

```css
.class {
  width: calc(100% - 5px);
  height: 25px;
  font-size: 1 / 4;
}
```

We originally planned to default this to true in the future, but it has been a controversial option and we are considering whether we have solved the problem in the right way, or whether less should just have exceptions for instances where `/` is valid or calc is used.

我们原本计划将这个选项的默认值设置为 true ，但这是一个有争议的选项，我们在考虑以正确的方式解决这个问题，或者 less 是否应该有例外，如合法使用 `/` 或者使用 calc。

#### 5.21 Strict Units

```bash
lessc -su=on
lessc --strict-units=on
```

Defaults to off.

默认值是 off。

Without this option, less attempts to guess at the output unit when it does maths. For instance

如果没有这个选项，当输出的单位不匹配的时候 less 会附加一个猜测的单位。例如：

```less
.class {
  property: 1px * 2px;
}
```

In this case, things are clearly not right - a length multiplied by a length gives an area, but css does not support specifying areas. So we assume that the user meant for one of the values to be a value, not a unit of length and we output `2px`.

在这种情况下，事情显然是不对的。一个长度乘以一个长度得到的应该是一个面积，但是 CSS 不支持指定一个面积。所以我们假设用户的用意是其中一个值是一个数值，而不是一个带单位的长度，多以我们输出 `2px`。

With strict units on, we assume this is a bug in the calculation and throw an error.

在严格单位模式下，我们假定这是计算中的错误，并抛出一个错误。

#### 5.22 全局变量

```bash
lessc --global-var="my-background=red"
```

This option defines a variable that can be referenced by the file. Effectively the declaration is put at the top of your base Less file, meaning it can be used but it also can be overridden if this variable is defined in the file.

这个选项定义一个我们可以在任意文件引用的变量。实际上是在你的基础 less 文件的最顶部声明变量。同样的。你可以通过在文件中定义相同的变量来重写它。

#### 5.23 修改变量

```bash
lessc --modify-var="my-background=red"
```

As opposed to the global variable option, this puts the declaration at the end of your base file, meaning it will override anything defined in your Less file.

与全局变量选项相反，在基础 less 文件末尾添加声明变量，这意味着会重写任何你定义在 Less 中的变量。

#### 5.24 URL 参数

```bash
lessc --url-args="cache726357"
```

This option allows you to specify a argument to go on to every URL. This may be used for cache-busting for instance.

这个选项允许指定每一个 URL 的参数，常用于清理缓存。

#### 5.25 行号

*Deprecated*.

*废弃*

```bash
lessc --line-numbers=comments
lessc --line-numbers=mediaquery
lessc --line-numbers=all
```

Generates inline source-mapping. This was the only option before browsers started supporting sourcemaps.

生成内联 source-mapping 。这是浏览器开始支持 sourcemaps 之前的唯一选择。

#### 5.26 插件

```bash
lessc --clean-css
lessc --plugin=clean-css="advanced"
```

--plugin Loads a plugin. You can also omit the --plugin= if the plugin begins
less-plugin. E.g. the clean css plugin is called less-plugin-clean-css
once installed (npm install less-plugin-clean-css), use either with
--plugin=less-plugin-clean-css or just --clean-css
specify options afterwards e.g. --plugin=less-plugin-clean-css="advanced"
or --clean-css="advanced"

使用 --plugin 加载插件。如果插件以 less-plugin 开头，你可以省略 --plugin= 。例如：clean css 插件名称为 less-plugin-clean-css。安装后（npm install less-plugin-clean-css）无论是使用 --plugin=less-plugin-clean-css 还是只使用 --clean-css 指定之后的选项。例如 --plugin=less-plugin-clean-css="advanced" or --clean-css="advanced"
