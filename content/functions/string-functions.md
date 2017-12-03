### escape

> Applies [URL-encoding](http://en.wikipedia.org/wiki/Percent-encoding) to special characters found in the input string.

> 对指定的字符串进行 [URL-encoding](http://en.wikipedia.org/wiki/Percent-encoding) 编码。

* 这些字符不会被编码： `,`, `/`, `?`, `@`, `&`, `+`, `'`, `~`, `!` 和 `$`.
* 被编码的字符是: `\<space\>`, `#`, `^`, `(`, `)`, `{`, `}`, `|`, `:`, `>`, `<`, `;`, `]`, `[` 和 `=`.

参数： `string`: 被转义的字符串。

返回： 转以后不带引号的 `string` 字符串。

例子：

```less
escape('a=1')
```

输出：

```css
a%3D1
```

Note: if the parameter is not a string, output is not defined. The current implementation returns `undefined` on color and unchanged input on any other kind of argument. This behavior should not be relied on and may change in the future.

注意：如果传入的参数不是一个字符串，输出是没有被定义的。目前的是现是传入的是颜色值则返回 `undefined`，其他类型的值不变。不要依赖这个特性，它有可能在未来被改变。

### e

> CSS escaping, replaced with `~"value"` syntax.

> 转义 CSS，已被 `~"value"` 语法代替。

It expects string as a parameter and return its content as is, but without quotes. It can be used to output CSS value which is either not valid CSS syntax, or uses proprietary syntax which Less doesn't recognize.

它接收一个字符串参数，并原样返回它包含的内容内容，但不包含括号。它常用于输出不合法的 CSS 值或者使用 Less 不能识别的属性。

参数： `string` - 需要转义的字符串.

返回： `string` - 不含引号的转义后的字符串.

例子：

```less
filter: e("ms:alwaysHasItsOwnSyntax.For.Stuff()");
```

输出：

```css
filter: ms:alwaysHasItsOwnSyntax.For.Stuff();
```

Note: The function accepts also `~""` escaped values and numbers as parameters. Anything else returns an error.

注意：函数也接受经 `~""` 转义的值或者是数字作为参数。任何其它的值将产生错误。

### % format

> The function `%(string, arguments ...)` formats a string.

> `%(string, arguments ...)` 对字符串进行格式化。

The first argument is string with placeholders. All placeholders start with percentage symbol `%` followed by letter `s`,`S`,`d`,`D`,`a`, or `A`. Remaining arguments contain expressions to replace placeholders. If you need to print the percentage symbol, escape it by another percentage `%%`.

第一个参数是一个包含占位符的字符串。所有的占位符以百分号 `%` 开始，后面跟随着字母`s`,`S`,`d`,`D`,`a`, 或者 `A`。剩下的参数用于替换这些占位符。如果你想输出百分号，你需要使用另外一个百分号来转义 `%%`。

Use uppercase placeholders if you need to escape special characters into their utf-8 escape codes.
The function escapes all special characters except `()'~!`. Space is encoded as `%20`. Lowercase placeholders leave special characters as they are.

使用大写的占位符，将特殊的字符按照 UTF-8 编码进行转义。
这个函数转义所有的特殊字符，除了 `()'~!`。空格被转义为 `%20`。小写占位符按原字符输出。

Placeholders:

* `d`, `D`, `a`, `A` - can be replaced by any kind of argument (color, number, escaped value, expression, ...). If you use them in combination with string, the whole string will be used - including its quotes. However, the quotes are placed into the string as they are, they are not escaped by "/" nor anything similar.
* `s`, `S` - can be replaced by any expression. If you use it with string, only the string value is used - quotes are omitted.

占位符：

* `d`, `D`, `a`, `A` - 可以被任意的类型参数替换 (颜色, 数字, 转以后的值, 表达式, ...)。 如果你将他们和字符串一起使用，整个字符串将会被使用，包括括号。但是字符串会被原样放在字符串中，不会被使用 "/" 或者其他类似的形式转义。
* `s`, `S` - 可以被任意的字符串替换。如果你使用一个字符串的值替换，只有字符串中的值会被使用，引号会被忽略。

参数：

* `string`: 含有占位符的待格式化字符串
* `anything`* : 替换占位符的值

返回： 格式化的 `string`.

例子：

```less
format-a-d: %("repetitions: %a file: %d", 1 + 2, "directory/file.less");
format-a-d-upper: %('repetitions: %A file: %D', 1 + 2, "directory/file.less");
format-s: %("repetitions: %s file: %s", 1 + 2, "directory/file.less");
format-s-upper: %('repetitions: %S file: %S', 1 + 2, "directory/file.less");
```
输出：

```css
format-a-d: "repetitions: 3 file: "directory/file.less"";
format-a-d-upper: "repetitions: 3 file: %22directory%2Ffile.less%22";
format-s: "repetitions: 3 file: directory/file.less";
format-s-upper: "repetitions: 3 file: directory%2Ffile.less";
```


### replace

> Replaces a text within a string.

> 使用字符串代替一段文本。

发布于 [v1.7.0]({{ less.master.url }}CHANGELOG.md)

参数：

* `string`: 用于搜索、替换的字符串。
* `pattern`: 用于搜索匹配的字符串或正则表达式。
* `replacement`: 用于替换匹配项的字符串。
* `flags`: (可选) 正则表达式参数。

返回： 被替换之后的字符串。

例子：

```less
replace("Hello, Mars?", "Mars\?", "Earth!");
replace("One + one = 4", "one", "2", "gi");
replace('This is a string.', "(string)\.$", "new $1.");
replace(~"bar-1", '1', '2');
```

结果：

```css
"Hello, Earth!";
"2 + 2 = 4";
'This is a new string.';
bar-2;
```
