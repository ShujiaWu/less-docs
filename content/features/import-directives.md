> Import styles from other style sheets

> 从其他的样式表中导入样式

In standard CSS, `@import` at-rules must precede all other types of rules. But Less doesn't care where you put `@import` statements.

在标准的 CSS 中， `@import` 作为 CSS 规则必须放置域所有的规则之前。但是 Less 不管你在任何地方使用 `@import` 表达式。

Example:

例如：

```less
.foo {
  background: #900;
}
@import "this-is-valid.less";
```

## 文件扩展名
`@import` statements may be treated differently by Less depending on the file extension:

Less 会根据不同的文件扩展名处理 `@import` 表达式。

* If the file has a `.css` extension it will be treated as CSS and the `@import` statement left as-is (see the [inline option](#import-options-inline) below).
* If it has _any other extension_ it will be treated as Less and imported.
* If it does not have an extension, `.less` will be appended and it will be included as a imported Less file.

* 如果文件的扩展名是 `.css` ， 它将会被当做 CSS 进行处理， `@import` 作为 CSS 的表达式保持不变（见下面的[行内选项](#import-options-inline)）。
* 如果是其他的任意扩展名，将会全部当做 Less 进行处理和导入。
* 如果不包含任意的扩展名，`.less` 将会被添加到文件末尾，并被当做 Less 文件进行导入。

Examples:

例如：

```less
@import "foo";      // foo.less is imported
@import "foo.less"; // foo.less is imported
@import "foo.php";  // foo.php imported as a Less file
@import "foo.css";  // statement left in place, as-is
```

The following options can be used to override this behavior.

使用下面的选项将重写导入的默认行为。

# Import 选项
> Less offers several extensions to the CSS `@import` CSS at-rule to provide more flexibility over what you can do with external files.

> 在规则中， Less 提供一些 CSS `@import` 的扩展，以提供更多的灵活性来处理外部文件。

d语法: `@import (keyword) "filename";`

The following import directives have been implemented:

下面的导入指令已经实现：

* `reference`: use a Less file but do not output it
* `inline`: include the source file in the output but do not process it
* `less`: treat the file as a Less file, no matter what the file extension
* `css`: treat the file as a CSS file, no matter what the file extension
* `once`: only include the file once (this is default behavior)
* `multiple`: include the file multiple times
* `optional`: continue compiling when file is not found

* `reference`: 使用 Less 文件但并不作为输出
* `inline`: 在输出中包含源文件，但是不处理它
* `less`: 忽略文件的扩展名，作为 Less 文件进行处理
* `css`: 忽略文件的扩展名，作为 CSS 文件进行处理
* `once`: 相同文件只导入一次（这是默认行为）
* `multiple`: 相同的文件导入多次
* `optional`: 当文件没有找到时继续编译

> More than one keyword per `@import` is allowed, you will have to use commas to separate the keywords:

> 每个 `@import` 中允许带多个关键字，多个关键字见使用逗号隔开：

例如: `@import (optional, reference) "foo.less";`

## reference
> Use `@import (reference)` to import external files, but without adding the imported styles to the compiled output unless referenced.

> 使用 `@import (reference)` 导入外部文件，除非被引用的部分否则是不会作为编译的结果输出。

Released [v1.5.0]({{ less.master.url }}CHANGELOG.md)

例如: `@import (reference) "foo.less";`

Imagine that `reference` marks every directive and selector with a _reference flag_ in the imported file, imports as normal, but when the CSS is generated, "reference" selectors (as well as any media queries containing only reference selectors) are not output. `reference` styles will not show up in your generated CSS unless the reference styles are used as [mixins](#mixins-feature) or [extended](#extend-feature).

想象成 `reference`  将导入文件的每一个指令和选择器都标上 _reference 标记_，并被作为普通的导入方式进行导入，但是被打上 reference 标记的选择器（以及任何只包含引用选择器的媒体查询）将不会被输出。`reference` 导入的样式不会出现在编译生成的 CSS 中，除非被作为[mixins](#mixins-feature) 或 [extended](#extend-feature) 引用。

Additionally, **`reference`** produces different results depending on which method was used (mixin or extend):

另外，**`reference`** 会根据不同的使用方法（混合mixin 或 继承extend）产生不同的结果集：

* **[extend](#extend-feature)**: When a selector is extended, only the new selector is marked as _not referenced_, and it is pulled in at the position of the reference `@import` statement.
* **[mixins](#mixins-feature)**: When a `reference` style is used as an [implicit mixin](#mixins-feature), its rules are mixed-in, marked "not reference", and appear in the referenced place as normal.

* **[继承 extend](#extend-feature)**: 当一个选择器被继承，只有新的选择器会被标记为 _not referenced_，并且将会被放置在引用 `@import` 表达式的位置。
* **[混合 mixins](#mixins-feature)**: 当一个 `reference` 样式被作为 [隐式混合（implicit mixin）](#mixins-feature)，它包含的规则会被混合（mixed-in），并被标记为 "not reference"，正常出现在被引用的地方。

### reference 例子
This allows you to pull in only specific, targeted styles from a library such as [Bootstrap](https://github.com/twbs/bootstrap) by doing something like this:

这允许你从类库中引入特定的样式，例如[Bootstrap](https://github.com/twbs/bootstrap)：

```less
.navbar:extend(.navbar all) {}
```

And you will pull in only `.navbar` related styles from Bootstrap.

这样你可以从 Bootstrap 获取 `.navbar` 的样式。

## inline
> Use `@import (inline)` to include external files, but not process them.

> 使用 `@import (inline)` 包含外部的文件，但不进行处理。

Released [v1.5.0]({{ less.master.url }}CHANGELOG.md)

例如: `@import (inline) "not-less-compatible.css";`

You will use this when a CSS file may not be Less compatible; this is because although Less supports most known standards CSS, it does not support comments in some places and does not support all known CSS hacks without modifying the CSS.

当 CSS 文件与 Less 不是很兼容时使用。这是因为虽然Less支持所有已知的标准 CSS， 但是它不支持部分注解，也不支持所有的没有修改过的 CSS hack。

So you can use this to include the file in the output so that all CSS will be in one file.

因此，你可以使用它将文件包含在输出中，这样所有的CSS都将在一个文件中。

## less
> Use `@import (less)` to treat imported files as Less, regardless of file extension.

> 使用 `@import (less)` 忽略文件的扩展名，按 Less 处理导入的文件。

Released [v1.4.0]({{ less.master.url }}CHANGELOG.md)

Example:

例如：

```less
@import (less) "foo.css";
```


## css
> Use `@import (css)` to treat imported files as regular CSS, regardless of file extension. This means the import statement will be left as it is.

> 使用 `@import (css)` 忽略文件的扩展名，按 CSS 处理导入的文件。这意味着导入语句将被保留。

Released [v1.4.0]({{ less.master.url }}CHANGELOG.md)

Example:

例如：

```less
@import (css) "foo.less";
```

outputs

输出：

```less
@import "foo.less";
```


## once
> The default behavior of `@import` statements. It means the file is imported only once and subsequent import statements for that file will be ignored.

> 这是 `@import` 表达式的默认行为。这意味着文件只能被导入一次，随后的导入相同的文件将会被忽略。

Released [v1.4.0]({{ less.master.url }}CHANGELOG.md)

This is the default behavior of `@import` statements.

这是 `@import` 表达式的默认行为。

Example:

例如：

```less
@import (once) "foo.less";
@import (once) "foo.less"; // this statement will be ignored
```

## multiple
> Use `@import (multiple)` to allow importing of multiple files with the same name. This is the opposite behavior to once.

> 使用 `@import (multiple)` 允许导入多个相同的文件，这跟 once 的行为相反。

Released [v1.4.0]({{ less.master.url }}CHANGELOG.md)

Example:

例如：

```less
// file: foo.less
.a {
  color: green;
}
// file: main.less
@import (multiple) "foo.less";
@import (multiple) "foo.less";
```

Outputs

输出：

```less
.a {
  color: green;
}
.a {
  color: green;
}
```

## optional
> Use `@import (optional)` to allow importing of a file only when it exists. Without the `optional` keyword Less throws a FileError and stops compiling when importing a file that can not be found.

> 使用 `@import (optional)` 允许当文件存在时进行导入。如果没有 `optional` 关键字，当导入的文件不存在时， Less 编译时会抛出 FileError 异常并停止编译。

Released [v2.3.0]({{ less.master.url }}CHANGELOG.md)
