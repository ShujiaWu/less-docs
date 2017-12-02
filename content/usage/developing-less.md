---
title: 开发 Less
---

Thanks for thinking about contributing. Please read the [contributing instructions]({{ less.master.url }}CONTRIBUTING.md) carefully to avoid wasted work.

很感谢你参与贡献. 请仔细阅读 [贡献指南]({{ less.master.url }}CONTRIBUTING.md) 以免浪费工作.

## 1. 安装一下工具

* **node** - <http://nodejs.org/>
* **phantomjs** - <http://phantomjs.org/download.html>

make sure the paths are setup. If you start your favourite command line and type `node -v` you should see the node compiler. If you run `phantomjs -v` you should see the phantomjs version number.

确认你已经设置好 paths 路径。运行命令行，输入 `node -v` 你将看到 node 编译器的版本， 运行 `phantomjs -v` 将看到 phantomjs 的版本号。

* clone your less.js repository locally
* navigate to your local less.js repository and run `npm install` this installs less' npm dependencies.
* If you haven't used grunt before, run `npm install grunt-cli -g` - this allows you to use the "grunt" command anywhere

* 在本地 clone 你的 less.js 项目。
* 定位到本地 less.js 仓库中的位置，运行 `npm install` 安装 less 的 npm 依赖。
* 如果你之前没有使用过，运行 `npm install grunt-cli -g` ，这将允许你在任何地方使用 "grunt" 命令。

## 2. 使用

If you go to the root of the Less repository you should be able to do `grunt test` - this should run all the tests. For the browser specific only, run `grunt browsertest` If you want to try out the current version of less against a file, from here do `node bin/lessc path/to/file.less`

如果你进入 Less 仓库的根目录，你可以运行 `grunt test` 执行所有的测试。如果想要只指定浏览器，运行`grunt browsertest`。如果你想通过一个文件测试当前版本的 Less,执行 `node bin/lessc path/to/file.less`

To debug the browser tests, run `grunt browsertest-server` then go to http://localhost:8088/tmp/browser/ to see the test runner pages.

调试浏览器测试，运行 `grunt browsertest-server`，接着打开 http://localhost:8088/tmp/browser/ 查看测试运行页面。

Optional: To get the current version of the Less compiler do `npm -g install less` - npm is the node package manager and "-g" installs it to be available globally.

可选的：通过运行 `npm -g install less` 获取当前 Less 编译器的版本。npm 是node 包管理器，通过 “-g” 进行全局安装。

You should now be able to do `lessc file.less` and if there is an appropriate `file.less` then it will be compiled and output to the stdout. You can then compare it to running locally (`node bin/lessc file.less`).

现在你可以执行 `lessc file.less`，如果 `file.less` 是恰当的，那么它将会被编译并且输出到 stdout。接着你可以执行本地的版本(`node bin/lessc file.less`)进行比较。

Other grunt commands

其他 grunt 命令：

* `grunt benchmark` - run our benchmark tests to get some numbers on performance
* `grunt stable` to create a new release
* `grunt readme` to generate a new readme.md in the root directory (after each release)

* `grunt benchmark` - 运行我们的基准测试以获得一些性能上的数据
* `grunt stable` 创建一个发布版
* `grunt readme` (在生成发布版本之后)在根目录生成一个新的 readme.md 文件

## 3. 如何在其他环境运行 Less

If you look in the libs folder you will see `less`, `less-node`, `less-browser`. The `less` folder is pure javascript with no environment
specifics. if you require `less/libs/less`, you get a function that takes an environment object and an array of file managers. The file
managers are the same file managers that can also be written as a plugin.

如果你查看 libs 文件夹，你将会看到 `less`, `less-node`, `less-browser`。`less` 文件夹是纯粹没有指定环境 javascript。如果你使用 require `less/libs/less`，你将获得一个带环境对象和一个文件管理器数组的函数。这些文件管理跟编写插件时候的文件管理器是一样的。

```js
var createLess = require("less/libs/less"),
    myLess = createLess(environment, [myFileManager]);
```

The environment api is specified in [less/libs/less/environment/environment-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/environment-api.js)
and the file manager api is specified in [less/libs/less/environment/file-manager-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/file-manager-api.js).

[less/libs/less/environment/environment-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/environment-api.js)有详细的环境 api 说明。[less/libs/less/environment/file-manager-api.js](https://github.com/less/less.js/blob/master/lib/less/environment/file-manager-api.js)有详细的文件管理api说明。

For file managers we highly recommend setting the prototype as a new AbstractFileManager - this allows you to override what is needed and allows us
to implement new functions without breaking existing file managers. For an example of file managers, see the 2 node implementations, the browser implementation or
the npm import plugin implementation.

对于文件管理器，我们强烈建议将原型设置为新的AbstractFileManager，这将允许在不破坏原先已经存在的文件管理器函数的基础上重写你需要的函数。对于文件管理器的示例，请参见2种 node 实现、浏览器实现或 npm 导入插件的实现。

## 4. 向导

If you look at [http://www.gliffy.com/go/publish/4784259](http://www.gliffy.com/go/publish/4784259),  This is an overview diagram of how less works. Warning! It needs updating with v2 changes.

如果你查看[http://www.gliffy.com/go/publish/4784259](http://www.gliffy.com/go/publish/4784259)，这个一个关于 Less 如何工作的该蓝图。注意，他需要根据 V2 进行版本更新。
