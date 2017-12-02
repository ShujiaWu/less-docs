---
title: 第三方编译器
---

## Node.js 编译器

* **[grunt-contrib-less](https://github.com/gruntjs/grunt-contrib-less)**
* **[assemble-less](https://github.com/assemble/assemble-less)**: Full-featured Grunt.js plugin for compiling Less files to CSS, with additional options for maintaining libraries of Less components and themes. For advanced users, this plugin allows you to define and manage Less "packages" or "bundles" using JSON, [Lo-dash](https://github.com/bestiejs/lodash)(underscore) templates (e.g. `<%= bootstrap.less %>`), and [node-glob](https://github.com/isaacs/node-glob) / [minimatch](https://github.com/isaacs/minimatch) (e.g. `'../src/**/*.less"`). _assemble-less_ also has a number of options including minifying CSS.全特性的将 Less 编译成 CSS 的 Grunt.js 插件，为维护 Less 组件和主题提供附加选项。对于高级用户，改插件允许你定义和管理 Less 的 "packages" 或 "bundles" 通过使用 JSON， [Lo-dash](https://github.com/bestiejs/lodash)(underscore) 模板（例如：`<%= bootstrap.less %>`）或者[node-glob](https://github.com/isaacs/node-glob) / [minimatch](https://github.com/isaacs/minimatch)（例如：`'../src/**/*.less"`）。_assemble-less_同样拥有与一系列包括压缩 CSS 等的选项。

* **[gulp-less](https://github.com/plus3network/gulp-less)**: Please note that this plugin discards `source-map` options, opting to instead using the [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) library.注意，这个插件废弃 `source-map` 选项，使用 [gulp-sourcemaps](https://github.com/floridoo/gulp-sourcemaps) 代替。
* **[autoless](https://github.com/jgonera/autoless)**: A Less files watcher, with dependency tracking (changes to imported files cause other files to be updated too) and growl notifications. Less 文件监视器，依赖跟踪（对导入文件的更改导致其他文件的更改也被更新）和消息通知。
* **[Connect Middleware for Less](https://github.com/emberfeather/less.js-middleware)**: Connect Middleware for Less compiling。Less 编译的的中间件。


## 其他技术

**Wro4j Runner CLI**
Download the [wro4j-runner.jar](http://wro4j.googlecode.com/files/wro4j-runner-1.4.1-jar-with-dependencies.jar) file and run the following command:

下载 [wro4j-runner.jar](http://wro4j.googlecode.com/files/wro4j-runner-1.4.1-jar-with-dependencies.jar) 文件，并使用下面的命令运行：

```bash
java -jar wro4j-runner-1.5.0-jar-with-dependencies.jar --preProcessors lessCss
```

More details can be found here: [Wro4j Runner CLI](http://code.google.com/p/wro4j/wiki/wro4jRunner)

更多信息查看：[Wro4j Runner CLI](http://code.google.com/p/wro4j/wiki/wro4jRunner)

**CSS::LESSp**

http://search.cpan.org/~drinchev/CSS-LESSp/

```bash
lessp.pl styles.less > styles.css
```

**Windows Script Host**

Note - the official Less node runs on windows, so we are not sure why you would use this.

注意，这是运行在windows node上的官方 Less 编译器，我们也不确定你是否会使用这个。

[Less.js for Windows](https://github.com/duncansmart/less.js-windows) with this usage:

```bash
cscript //nologo lessc.wsf input.less [output.css] [-compress]
```
or

```bash
lessc input.less [output.css] [-compress]
```

**dotless**

[dotless for Windows](http://www.dotlesscss.org/) can be run like this:

[dotless for Windows](http://www.dotlesscss.org/) 像下面一样运行:

```bash
dotless.Compiler.exe [-switches] <inputfile> [outputfile]
```

**另见:**

* [Ports of Less](/about/#ports)
