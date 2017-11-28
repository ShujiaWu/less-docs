---
title: V2 Upgrade Guide
---

1. 语言变化
----------------

Colours now output as they are written, so `purple` stays as `purple` and is not converted to its hex representation.

颜色的输出与书写的格式保持一致，所以写 `purple` 输出是 `purple`，它将不会被转化成以16进制形式。

2. 命令行使用说明
------------------

### Clean CSS

We have removed the dependency on `clean-css` and moved it to a [plugin](https://github.com/less/less-plugin-clean-css).
This allows us to:

我们将移除 `clean-css` 依赖，并将它移动到[插件](https://github.com/less/less-plugin-clean-css)中。这将允许我们：

1. update the dependency and integration without a Less release
2. not tie people who do not use `clean-css` into having it downloaded by npm.

1. 在不发布 Less 的情况下，更新依赖和集成。
1. 不把在npm下载 `clean-css` 捆绑到不使用它的人上。

The usage is similar, just install the plugin (`npm install -g less-plugin-clean-css`) then tell less to use it by using the
`--clean-css` argument.

在使用上是相似的，只需要安装插件(`npm install -g less-plugin-clean-css`)，然后通过参数 `--clean-css` 告诉 less 使用它。

```bash
# old
lessc --clean-css --clean-option=--compatibility:ie8 --clean-option=--advanced
# new
lessc --clean-css="--compatibility=ie8 --advanced"
```

### Sourcemaps

We have improved the source map options and path generation so the sourcemap should be generated at the correct path without specifying any options.

我们已经提供 source map 选项和生成路径，如果没有指定任意选项，则 sourcemap 会被生成到当前路径。

3. 编程方式使用说明
------------------

We have deprecated the use of less.Parser and toCss to generate the css. Instead we require you to use the `less.render` shorthand.
See [Programmatic Usage](#programmatic-usage) for more information.

我们不推荐使用 Parser 和 toCss 这种使用 less 生成CSS的方式。作为代替方案，我们要求你使用 `less.render` 这种简单的方式。查阅[编程方式使用说明](#programmatic-usage)获取更多详情。

Further, instead of returning a string which is the css, we return an object with a `css` field set to the string and a `map` field set to the sourcemap (if applicable).

在未来，（在合适的情况下）我们将返回一个对象，包含 `css` 字段的字符串和 `map` 字段的 sourcemap，而不是只是返回 css 字符串。

The sourcemap options are now to be set on sourceMap instead of directly on options. So instead of `options.sourceMapFullFilename = ` you would set `options.sourceMap = { sourceMapFullFilename: `.

sourcemap 的选项现在被设置在 sourceMap 选项上上而不是直接设置在选项上。所以 `options.sourceMapFullFilename =` 将被代替为 `options.sourceMap = { sourceMapFullFilename:`。

4. 在浏览器中使用说明
-------------

The browser usage has not changed significantly. Options set on the `less` object are exposed as `less.options` after the less script has run, rather than polluting `less`.

浏览器的使用并没有明显的改变。less 脚本运行后选项将作为 `less` 中的对象 `less.options` 被暴露出来，而不会污染 `less` 。

It is now possible to specify options on the script and Less tags, which should simplify option setting in the browser. See the browser usage section for more information.

现在可以指定脚本上 less 标签的选项，这将简化浏览器中的选项设置。通过在阅读浏览器使用章节获取更多信息。