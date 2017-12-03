### color

> Parses a color, so a string representing a color becomes a color.

> 颜色解析器，将代表颜色的字符串编程颜色。

参数: `string`: 特定颜色的字符串。

返回: `color`

例子: `color("#aaa");`

输出: `#aaa`

### image-size

> Gets the image dimensions from a file.

> 从一个图片文件中获取图片的尺寸。

参数： `string`: 要获取尺寸的文件。

返回： `dimension`

例子：`image-size("file.png");`

输出： `10px 10px`

Note: this function needs to be implemented by each environment. It is currently only available in the node environment.

注意：这个函数需要在各个环境中实现。它目前只能在 node 环境下可用。

新增于： v2.2.0

### image-width

> Gets the image width from a file.

> 从一个图片文件中获取图片的宽度。

参数： `string`: 要获取尺寸的文件。

返回： `dimension`

例子：`image-width("file.png");`

输出： `10px`

Note: this function needs to be implemented by each environment. It is currently only available in the node environment.

注意：这个函数需要在各个环境中实现。它目前只能在 node 环境下可用。

新增于： v2.2.0

### image-height

> Gets the image height from a file.

> 从一个图片文件中获取图片的高度。

参数： `string`: 要获取尺寸的文件。

返回： `dimension`

例子：`image-height("file.png");`

输出： `10px`

Note: this function needs to be implemented by each environment. It is currently only available in the node environment.

注意：这个函数需要在各个环境中实现。它目前只能在 node 环境下可用。

新增于： v2.2.0

### convert

> Convert a number from one unit into another.

> 将数字从一种单位转换成另外一种单位。

The first argument contains a number with units and second argument contains units. If the units are compatible, the number is converted. If they are not compatible, the first argument is returned unmodified.

第一个参数是包含单位的数字，第二参数是要转换的单位。如果单位是兼容的，那么数据会被转换。如果参数不兼容，则不做任何修改返回第一个参数。

See [unit](#misc-functions-unit) for changing the unit without conversion.

阅读 [unit](#misc-functions-unit) 了解单位不被转换的情况。

_Compatible unit groups_:

_兼容的单位_:

* 长度: `m`, `cm`, `mm`, `in`, `pt` , `pc`,
* 时间: `s` , `ms`,
* 角度: `rad`, `deg`, `grad` , `turn`.

参数：
* `number`: 带单位的浮点数
* `identifier`, `string` 或者 `escaped value`: 单位

返回： `number`

例子：

```less
convert(9s, "ms")
convert(14cm, mm)
convert(8, mm) // 不兼容的单位类型
```

输出：

```
9000ms
140mm
8
```


### data-uri

> Inlines a resource and falls back to `url()` if the ieCompat option is on and the resource is too large, or if you use the function in the browser. If the MIME type is not given then node uses the mime package to determine the correct mime type.

> 将资源关联进样式表，如果使用了 ieCompat 选项，并且资源太大，或者在浏览器下使用函数，则会回退为使用 `url()` 。如果 MIME 类型没有指定，那么 node 会使用 mine 包来决定恰当的 mime 类型。

参数：

* `mimetype`: （可选）MIME 类型字符串。
* `url`: 内联文件的 URL 地址。

If there is no mimetype, data-uri function guesses it from filename suffix. Text and svg files are encoded as utf-8 and anything else is encoded as base64.

如果没有指定 MIME 类型，那么 data-uri 函数会从文件的后缀名猜测 MIME 类型。文本和 SVG 文件会被 utf-8 编码，其他文件会被 base64 编码。

If user provided mimetype, the function uses base64 if mimetype argument ends with ;base64. For example, `image/jpeg;base64` is encoded into base64 while `text/html` is encoded into utf-8.

如果用户提供了 mime 类型并且以 ;base64 结尾作为参数，则函数会使用 base64 编码文件。例如：`image/jpeg;base64` 会被编码成 base64，`text/html` 会被编码成 utf-8。 

例子：`data-uri('../data/image.jpg');`

输出： `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

浏览器模式下输出: `url('../data/image.jpg');`

例子：`data-uri('image/jpeg;base64', '../data/image.jpg');`

输出： `url('data:image/jpeg;base64,bm90IGFjdHVhbGx5IGEganBlZyBmaWxlCg==');`

例子：`data-uri('image/svg+xml;charset=UTF-8', 'image.svg');`

输出： `url("data:image/svg+xml;charset=UTF-8,%3Csvg%3E%3Ccircle%20r%3D%229%22%2F%3E%3C%2Fsvg%3E");`

### default

> Available only inside guard conditions and returns `true` only if no other mixin matches, `false` otherwise.

> 只在守卫的条件中使用，当没有匹配任何混合（mixin）的情况下返回 `true`， 否则返回 `false`。

例子：

```less
.mixin(1)                   {x: 11}
.mixin(2)                   {y: 22}
.mixin(@x) when (default()) {z: @x}

div {
  .mixin(3);
}

div.special {
  .mixin(1);
}
```
输出：

```css
div {
  z: 3;
}
div.special {
  x: 11;
}
```

It is possible to use the value returned by `default` with guard operators. For example `.mixin() when not(default()) {}` will match only if there's at least one more mixin definition that matches`.mixin()` call:

使用 `default` 守卫的返回值是可能的。例如 `.mixin() when not(default()) {}` 会被匹配，当调用`.mixin()`至少有一个混合（mixin）匹配的时候。

```less
.mixin(@value) when (ispixel(@value)) {width: @value}
.mixin(@value) when not(default())    {padding: (@value / 5)}

div-1 {
  .mixin(100px);
}

div-2 {
  /* ... */
  .mixin(100%);
}
```

结果：

```css
div-1 {
  width: 100px;
  padding: 20px;
}
div-2 {
  /* ... */
}
```

It is allowed to make multiple `default()` calls in the same guard condition or in a different conditions of a mixins with the same name:

这同样允许在相同名字的同一个守卫条件、不同守卫条件的混合（mixin）中使用多个 `default()` 调用。

```less
div {
  .m(@x) when (default()), not(default())    {always: @x}
  .m(@x) when (default()) and not(default()) {never:  @x}

  .m(1); // OK
}
```

However Less will throw a error if it detects a *potential* conflict between multiple mixin definitions using `default()`:

然而当 Less 监测到在使用 `default()` 的混合（mixin）定义中存在潜在的冲突时会抛出一个错误。

```less
div {
  .m(@x) when (default())    {}
  .m(@x) when not(default()) {}

  .m(1); // Error
}
```

In above example it is impossible to determine what value each `default()` call should return since they recursively depend on each other.

在上面的例子，不能确定每一个 `default()` 调用应该返回的值，他们递归地依赖对方。

Advanced multiple `default()` usage:

多个 `default()` 的推荐用法：

```less
.x {
  .m(red)                                    {case-1: darkred}
  .m(blue)                                   {case-2: darkblue}
  .m(@x) when (iscolor(@x)) and (default())  {default-color: @x}
  .m('foo')                                  {case-1: I am 'foo'}
  .m('bar')                                  {case-2: I am 'bar'}
  .m(@x) when (isstring(@x)) and (default()) {default-string: and I am the default}

  &-blue  {.m(blue)}
  &-green {.m(green)}
  &-foo   {.m('foo')}
  &-baz   {.m('baz')}
}
```

结果：

```css
.x-blue {
  case-2: #00008b;
}
.x-green {
  default-color: #008000;
}
.x-foo {
  case-1: I am 'foo';
}
.x-baz {
  default-string: and I am the default;
}
```

The `default` function is available as a Less built-in function _only inside guard expressions_. If used outside of a mixin guard condition it is interpreted as a regular CSS value:

`default` 函数仅作为守卫表达式中 Less 内置函数才可用。如果在混合守卫条件之外的其他地方使用，则会被理解为常规的 CSS 值：

例子：

```less
div {
  foo: default();
  bar: default(42);
}
```

结果：

```css
div {
  foo: default();
  bar: default(42);
}
```

### unit

> Remove or change the unit of a dimension

> 移除或者修改一个尺寸的单位

参数：

* `dimension`: 带或不带单位的数字
* `unit`: （可选的）目标单位，如果忽略则移除单位。

See [convert](#misc-functions-convert) for changing the unit with conversion.

阅读 [convert](#misc-functions-convert) 获取更多转换改变单位的信息

例子：`unit(5, px)`

输出： `5px`

例子：`unit(5em)`

输出： `5`



### get-unit

> Returns units of a number.

> 返回数字的单位。

If the argument contains a number with units, the function returns its units. The argument without units results in an empty return value.

如果参数是一个带单位的数字，调用函数将返回它的单位。如果参数中不带单位，则返回空。

参数：

* `number`: 带或不带单位的数字。

例子：`get-unit(5px)`

输出： `px`

例子：`get-unit(5)`

输出： ` //nothing` 



### svg-gradient

> Generates multi-stop svg gradients.

> 生成多点 svg 渐变。

Svg-gradient function generates multi-stop svg gradients. It must have at least three parameters. First parameter specifies gradient type and direction and remaining parameters list colors and their positions. The position of first and last specified color are optional, remaining colors must have positions specified.

Svg-gradient 函数生成多天 svg 渐变。它必须至少包含三个参数。第一个参数指定渐变的类型、方向，剩下的参数是渐变点颜色和位置的列表。第一个颜色和最后一个颜色的位置可选的，其他点颜色的位置必须指定。

The direction must be one of `to bottom`, `to right`, `to bottom right`, `to top right`, `ellipse` or `ellipse at center`. The direction can be specified as both escaped value `~'to bottom'` and space separated list of words `to bottom`.

渐变方向的值必须是以下的值：`to bottom`, `to right`, `to bottom right`, `to top right`, `ellipse` 或者 `ellipse at center`。渐变方向可以被指定为编码后的值 `~'to bottom'` 或者是使用空格分隔的单词列表 `to bottom`。

The direction must be followed by two or more color stops. They can be supplied either inside a list or you can specify each color stops in separate argument. 

渐变的方向必须拥有两个以上的渐变点。它们可以在列表中提供，也可以在单独的参数中指定每一个颜色。

Parameters - colors stops in list:

参数 - 渐变点颜色在列表中提供：

* `escaped value` 或者 `list of identifiers`: 渐变的方向
* `list` - 包含所有的颜色和他们位置的列表

Parameters - color stops in arguments:

参数 - 渐变点颜色在参数中提供：

* `escaped value` 或者 `list of identifiers`: 渐变的方向
* `color [percentage]` 成对存在: 第一个渐变点的颜色和相对位置（位置是可选的）
* `color percent` 成对存在: （可选的）第二个渐变点颜色和相对位置
* ...
* `color percent` 成对存在: （可选的）第 N 个渐变点的颜色和相对位置
* `color [percentage]` 成对存在: 最后一个渐变点的颜色和相对位置（位置是可选的）

返回： “URI编码”的 SVG 渐变 `url`。

例子 - 渐变点颜色在列表中提供：

```less
div {
  @list: red, green 30%, blue;
  background-image: svg-gradient(to right, @list);
}
```

等同于 - 渐变点颜色在参数中提供：

```less
div {
  background-image: svg-gradient(to right, red, green 30%, blue);
}
```

都输出为：

```css
div {
  background-image: url('data:image/svg+xml,%3C%3Fxml%20version%3D%221.0%22%20%3F%3E%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20version%3D%221.1%22%20width%3D%22100%25%22%20height%3D%22100%25%22%20viewBox%3D%220%200%201%201%22%20preserveAspectRatio%3D%22none%22%3E%3ClinearGradient%20id%3D%22gradient%22%20gradientUnits%3D%22userSpaceOnUse%22%20x1%3D%220%25%22%20y1%3D%220%25%22%20x2%3D%22100%25%22%20y2%3D%220%25%22%3E%3Cstop%20offset%3D%220%25%22%20stop-color%3D%22%23ff0000%22%2F%3E%3Cstop%20offset%3D%2230%25%22%20stop-color%3D%22%23008000%22%2F%3E%3Cstop%20offset%3D%22100%25%22%20stop-color%3D%22%230000ff%22%2F%3E%3C%2FlinearGradient%3E%3Crect%20x%3D%220%22%20y%3D%220%22%20width%3D%221%22%20height%3D%221%22%20fill%3D%22url(%23gradient)%22%20%2F%3E%3C%2Fsvg%3E');
}
```

Note: in versions before 2.2.0 the result is `base64` encoded .

注意：在 2.2.0 版本之前结果是以 `base64` 编码的。

Generated background image has red color on the left, green at 30% of its width and ends with a blue color. Base64 encoded part contains following svg-gradient:

生成左边是红色，宽度30%处为绿色，蓝色结尾的渐变背景图片。Base64 编码的内容包含下面的 svg 渐变。

```xml
<?xml version="1.0" ?>
<svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="100%" height="100%" viewBox="0 0 1 1" preserveAspectRatio="none">
    <linearGradient id="gradient" gradientUnits="userSpaceOnUse" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="#ff0000"/>
        <stop offset="30%" stop-color="#008000"/>
        <stop offset="100%" stop-color="#0000ff"/>
    </linearGradient>
    <rect x="0" y="0" width="1" height="1" fill="url(#gradient)" />
</svg>
```
