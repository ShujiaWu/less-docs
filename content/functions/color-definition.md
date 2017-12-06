### rgb

> Creates an opaque color object from decimal red, green and blue (RGB) values.

> 从十进制的红、绿、蓝（RGB）三种值创建不透明的颜色对象。

Literal color values in standard HTML/CSS formats may also be used to define colors, for example `#ff0000`.

在标准的 HTML/CSC 中也会用文本定义颜色的值，例如：`#ff0000`。

参数：
* `red`: 0-255的整数或0-100%的百分比。
* `green`: 0-255的整数或0-100%的百分比。
* `blue`: 0-255的整数或0-100%的百分比。

返回： `color`

例子： `rgb(90, 129, 32)`

输出： `#5a8120`


### rgba

> Creates a transparent color object from decimal red, green, blue and alpha (RGBA) values.

> 从十进制的红、绿、蓝、alpha（RGBA）四种值创建不透明的颜色对象。

参数：

* `red`: 0-255的整数或0-100%的百分比。
* `green`: 0-255的整数或0-100%的百分比。
* `blue`: 0-255的整数或0-100%的百分比。
* `alpha`: A number 0-1 or percentage 0-100%.

返回： `color`

例子： `rgba(90, 129, 32, 0.5)`

输出： `rgba(90, 129, 32, 0.5)`


### argb

> Creates a hex representation of a color in `#AARRGGBB` format (**NOT** `#RRGGBBAA`!).

> 创建格式为 `#AARRGGBB` 的十六进制颜色值（注意！不是 `#RRGGBBAA` ！）

This format is used in Internet Explorer, and .NET and Android development.

这种格式用于 Internet Explorer， NET 和 Android 开发。

参数： `color`, 颜色对象。

返回： `string`

例子： `argb(rgba(90, 23, 148, 0.5));`

输出： `#805a1794`


### hsl

> Creates an opaque color object from hue, saturation and lightness (HSL) values.

> 通过色相、饱和度、亮度（HSL）三种值创建不透明颜色对象。

参数：

* `hue`: 0-360的整数，用于代表度数。
* `saturation`: 0-100%的百分比，或0-1的数字。
* `lightness`: 0-100%的百分比，或0-1的数字。

返回： `color`

例子： `hsl(90, 100%, 50%)`

输出： `#80ff00`

This is useful if you want to create a new color based on another color's channel, forExample: `@new: hsl(hue(@old), 45%, 90%);`

当你想基于一个已有的颜色通道创建新颜色时，这非常有用。例如：`@new: hsl(hue(@old), 45%, 90%);`

`@new` will have `@old`'s *hue*, and its own saturation and lightness.

`@new` 将会拥有 `@old` 的色相，不同的饱和度和亮度。

### hsla

> Creates a transparent color object from hue, saturation, lightness and alpha (HSLA) values.

> 通过色相、饱和度、亮度（HSL）、alpha（HSLA）四种值创建透明颜色对象。

参数：
* `hue`: 0-360的整数，用于代表度数。
* `saturation`: 0-100%的百分比，或0-1的数字。
* `lightness`: 0-100%的百分比，或0-1的数字。
* `alpha`: 0-100%的百分比，或0-1的数字。

返回： `color`

例子： `hsla(90, 100%, 50%, 0.5)`

输出： `rgba(128, 255, 0, 0.5)`


### hsv

> Creates an opaque color object from hue, saturation and value (HSV) values.

> 通过色相、饱和度、色调（HSV）三种值创建不透明颜色。

Note that this is a color space available in Photoshop, and is not the same as `hsl`.

注意，与 `hsl` 不同，这是另一种在 Photoshop 中可用的色彩空间。

参数：
* `hue`: 0-360的整数，用于代表度数。
* `saturation`: 0-100%的百分比，或0-1的数字。
* `value`: 0-100%的百分比，或0-1的数字。

返回： `color`

例子： `hsv(90, 100%, 50%)`

输出： `#408000`


### hsva

> Creates a transparent color object from hue, saturation, value and alpha (HSVA) values.

> 通过色相、饱和度、色调、alpha（HSVA）四种值创建不透明颜色。

Note that this is not the same as `hsla`, and is a color space available in Photoshop.

注意，与 `hsla` 不同，这是另一种在 Photoshop 中可用的色彩空间。

参数：
* `hue`: 0-360的整数，用于代表度数。
* `saturation`: 0-100%的百分比，或0-1的数字。
* `value`: 0-100%的百分比，或0-1的数字。
* `alpha`: 0-100%的百分比，或0-1的数字。

返回： `color`

例子： `hsva(90, 100%, 50%, 0.5)`

输出： `rgba(64, 128, 0, 0.5)`
