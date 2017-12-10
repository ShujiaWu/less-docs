Color operations generally take parameters in the same units as the values they are changing, and percentages are handled as absolutes, so increasing a 10% value by 10% results in 20%. Set the option method parameter to relative for relative percentages. When using relative percentages increasing a 10% value by 10% results in 11%. Values are clamped to their allowed ranges; they do not wrap around. Where return values are shown, we've used formats that make it clear what each function has done, in addition to the hex versions that you will usually be be working with.

颜色操作通常会将参数转换成相同的单位，百分比会被当成成绝对的数值进行处理，所以 10% 增加 10% 的值是20%。将可选的方法参数设置为相对于百分比，当使用相对百分比时，10% 增加 10% 的结果是 11%。值被限定在他们允许的范围，它们不会缠绕在一起。在返回值显示的地方，我们使用了一些格式，这些格式清楚地说明了每个函数所做的事情，除了您通常要处理的十六进制版本。

### saturate

> Increase the saturation of a color in the HSL color space by an absolute amount.

> 增加 HSL 颜色空间的绝对数量饱和度。

参数：

* `color`: 颜色对象。
* `amount`: 0-100%的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `saturate(hsl(90, 80%, 50%), 20%)`

输出： `#80ff00 // hsl(90, 100%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80ff00:#000000/text:80ff00)

### desaturate

> Decrease the saturation of a color in the HSL color space by an absolute amount.

> 减少 HSL 颜色空间的绝对数量饱和度。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `desaturate(hsl(90, 80%, 50%), 20%)`

输出： `#80cc33 // hsl(90, 60%, 50%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#80cc33:#000000/text:80cc33)

### lighten

> Increase the lightness of a color in the HSL color space by an absolute amount.

> 增加 HSL 颜色空间的绝对数量亮度。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `lighten(hsl(90, 80%, 50%), 20%)`

输出： `#b3f075 // hsl(90, 80%, 70%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#b3f075:#000000/text:b3f075)

### darken

> Decrease the lightness of a color in the HSL color space by an absolute amount.

> 降低 HSL 颜色空间的绝对数量亮度。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `darken(hsl(90, 80%, 50%), 20%)`

输出： `#4d8a0f // hsl(90, 80%, 30%)`

![Color 1](holder.js/100x40/#80e619:#000000/text:80e619) ➜ ![Color 2](holder.js/100x40/#4d8a0f:#000000/text:4d8a0f)

### fadein

> Decrease the transparency (or increase the opacity) of a color, making it more opaque.

> 降低颜色的透明度（或者增加不透明度），让它更加不透明。

Has no effect on opaque colors. To fade in the other direction use `fadeout`.

在不透明的颜色上没有效果。在另一个方向上淡出使用 `fadeout`。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `fadein(hsla(90, 90%, 50%, 0.5), 10%)`

输出： `rgba(128, 242, 13, 0.6) // hsla(90, 90%, 50%, 0.6)`


### fadeout

> Increase the transparency (or decrease the opacity) of a color, making it less opaque. To fade in the other direction use `fadein`.

> 增加颜色的透明度（或者减少不透明度），让它更加透明。在另一个方向上淡出使用 `fadein`。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。
* `method`: 可选的，设置 `relative` 作为调整，相对于当前的值。

返回： `color`

例子： `fadeout(hsla(90, 90%, 50%, 0.5), 10%)`

输出： `rgba(128, 242, 13, 0.4) // hsla(90, 90%, 50%, 0.4)`


### fade

> Set the absolute opacity of a color. Can be applied to colors whether they already have an opacity value or not.

> 设置一个颜色的绝对透明度。可以应用在一个不管是否已经有不透明度值的颜色上。

参数：

* `color`: 颜色对象。
* `amount`: 0-100% 的百分比。

返回： `color`

例子： `fade(hsl(90, 90%, 50%), 10%)`

输出： `rgba(128, 242, 13, 0.1) //hsla(90, 90%, 50%, 0.1)`


### spin

> Rotate the hue angle of a color in either direction.

> 旋转颜色在任意方向上色调的角度。

While the angle range is 0-360, it applies a mod 360 operation, so you can pass in much larger (or negative) values and they will wrap around e.g. angles of 360 and 720 will produce the same result. Note that colors are passed through an RGB conversion, which doesn't retain hue value for greys (because hue has no meaning when there is no saturation), so make sure you apply functions in a way that preserves hue, for example don't do this:

当角度的值是在0-360之间，它将应用模360的操作。所以你可以传递大于这个范围的值（或者附属），他们会被转换。例如，360和720将产生相同的结果。注意，颜色是通过RGB转换来传递的，它不会保留灰色的色调值(因为当没有饱和度时，色相没有意义)，所以要确保你的作用是保持色相的，例如不要这么做：

```less
@c: saturate(spin(#aaaaaa, 10), 10%);
```

Do this instead:

使用下面的代替：

```less
@c: spin(saturate(#aaaaaa, 10%), 10);
```

Colors are always returned as RGB values, so applying `spin` to a grey value will do nothing.

结果始终以 RGB 值的形式返回，所以将 `spin` 应用在一个灰色的值上面讲不会做任何的事情。

参数：

* `color`: 颜色对象。
* `angle`: 旋转角度的数字 (+ 或者 -)。

返回： `color`

例子：

```less
spin(hsl(10, 90%, 50%), 30)
spin(hsl(10, 90%, 50%), -30)
```

输出：

```css
#f2a60d // hsl(40, 90%, 50%)
#f20d59 // hsl(340, 90%, 50%)
```

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f2a60d:#000000/text:f2a60d)

![Color 1](holder.js/100x40/#f2330d:#000000/text:f2330d) ➜ ![Color 2](holder.js/100x40/#f20d59:#000000/text:f20d59)

### mix

> Mix two colors together in variable proportion. Opacity is included in the calculations.

> 将两种颜色按可变比例混合。计算中包含不透明度。

参数：

* `color1`: 颜色对象。
* `color2`: 颜色对象。
* `weight`: 可选的，两种颜色百分比的平衡点，默认是50%。

返回： `color`

例子：

```less
mix(#ff0000, #0000ff, 50%)
mix(rgba(100,0,0,1.0), rgba(0,100,0,0.5), 50%)
```

输出：

```css
#800080
rgba(75, 25, 0, 0.75)
```

![Color 1](holder.js/100x40/#ff0000:#ffffff/text:ff0000) + ![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff) ➜ ![Color 3](holder.js/100x40/#800080:#ffffff/text:800080)

### tint

> Mix color with white in variable proportion. It is the same as calling ``mix(#ffffff, @color, @weight)``

> 将颜色和白色按可变比例混合。它作用如同调用 `mix(#ffffff, @color, @weight)`。

参数：

* `color`: 颜色对象。
* `weight`: 可选的，颜色和白色的百分比平衡点，默认是50%。

返回： `color`

例子：

```less
no-alpha: tint(#007fff, 50%); 
with-alpha: tint(rgba(00,0,255,0.5), 50%); 
```

输出：

```css
no-alpha: #80bfff;
with-alpha: rgba(191, 191, 255, 0.75);
```

![Color 1](holder.js/100x40/#ff00ff:#ffffff/text:ff00ff) ➜ ![Color 2](holder.js/100x40/#ff80ff:#ffffff/text:ff80ff)

### shade

> Mix color with black in variable proportion. It is the same as calling ``mix(#000000, @color, @weight)``

> 将颜色和黑色按可变比例混合。它作用如同调用 `mix(#000000, @color, @weight)`。

参数：

* `color`: 颜色对象。
* `weight`: 可选的，颜色和黑色的百分比平衡点，默认是50%。

返回： `color`

例子：

```less
no-alpha: shade(#007fff, 50%); 
with-alpha: shade(rgba(00,0,255,0.5), 50%); 
```

输出：

```css
no-alpha: #004080;
with-alpha: rgba(0, 0, 64, 0.75);
```

![Color 1](holder.js/100x40/#ff00ff:#ffffff/text:ff00ff) ➜ ![Color 2](holder.js/100x40/#800080:#ffffff/text:800080)

### greyscale

> Remove all saturation from a color in the HSL color space; the same as calling `desaturate(@color, 100%)`.

> 移除 HSL 颜色空间颜色的所有饱和度，和调用 `desaturate(@color, 100%)` 一样。

Because the saturation is not affected by hue, the resulting color mapping may be somewhat dull or muddy; [`luma`](#color-channel-luma) may provide a better result as it extracts perceptual rather than linear brightness, for example `greyscale('#0000ff')` will return the same value as `greyscale('#00ff00')`, though they appear quite different in brightness to the human eye.

因为饱和度不会受色相影响。所以产生的颜色映射可能有些单调或者模糊。 [`luma`](#color-channel-luma)可能会提供一个更好的结果， 因为它提取感知的而不是线性的亮度，例如 `greyscale('#0000ff')`将会返回与 `greyscale('#00ff00')` 一样的值。虽然它们在人眼人眼中在亮度上有很大的不同。

参数： `color`: 颜色对象。

返回： `color`

例子： `greyscale(hsl(90, 90%, 50%))`

输出： `#808080 // hsl(90, 0%, 50%)`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#808080:#000000/text:808080)

Notice that the generated grey looks darker than the original green, even though its lightness value is the same.

注意，生成的灰色看起来比原来的绿色更暗，即使它的亮度值相同。

Compare with using `luma` (usage is different because `luma` returns a single value, not a color):

与使用 `luma` 进行比较（用法是不同的，因为 `luma` 返回单个值而不是一个颜色。）：

```less
@c: luma(hsl(90, 90%, 50%));
color: rgb(@c, @c, @c);
```

输出： `#cacaca`

![Color 1](holder.js/100x40/#80f20d:#000000/text:80f20d) ➜ ![Color 2](holder.js/100x40/#cacaca:#000000/text:cacaca)

This time the grey's lightness looks about the same as the green, though its value is actually higher.

这一次，灰色的亮度和绿色一样，尽管它的值实际上更高。

### contrast

> Choose which of two colors provides the greatest contrast with another.

> 选择两种颜色重对比度最大的。

This is useful for ensuring that a color is readable against a background, which is also useful for accessibility compliance. This function works the same way as the [contrast function in Compass for SASS](http://compass-style.org/reference/compass/utilities/color/contrast/). In accordance with [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef), colors are compared using their gamma-corrected [luma](#color-channel-luma) value, not their lightness.

这对于确保颜色在背景下可读是有用的，这对于遵从可访问性也是很有用的。这个函数跟 [contrast function in Compass for SASS](http://compass-style.org/reference/compass/utilities/color/contrast/) 的作用是一样的。跟 [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef) 一样，颜色是用他们的伽玛校正[luma](#color-channel-luma)值来比较的，而不是它们的亮度。

The light and dark parameters can be supplied in either order - the function will calculate their luma values and assign light and dark automatically, which means you can't use this function to select the *least* contrasting color by reversing the order.

亮和暗参数可以按任意的顺序提供 -- 函数将计算它们的luma值，并自动分配亮和暗，这意味着你不能使用这个函数来通过反转顺序来选择对比度*最小*的颜色。

参数：

* `color`: 用于对比的颜色对象。
* `dark`: 可选 - 指定暗的颜色（默认是黑色）。
* `light`: 可选 - 指定亮的颜色（默认是白色）。
* `threshold`: 可选 - 0-100%的百分比指定从 “暗” 到 “亮” 的过渡(默认为 43% ，匹配SASS)。这是用来对对比的一种或另一种颜色产生偏移。例如，允许你决定50%的灰色背景应该产生黑色还是白色的文本。一般来说，你会把“较浅”的调色板设置为更低，把“深色”调色板设置得更高一些。

返回： `color`

例子：

```less
p {
    a: contrast(#bbbbbb);
    b: contrast(#222222, #101010);
    c: contrast(#222222, #101010, #dddddd);
    d: contrast(hsl(90, 100%, 50%), #000000, #ffffff, 30%);
    e: contrast(hsl(90, 100%, 50%), #000000, #ffffff, 80%);
}
```

输出：

```css
p {
    a: #000000 // black
    b: #ffffff // white
    c: #dddddd
    d: #000000 // black
    e: #ffffff // white
}
```

These examples use the above calculated colors for background and foreground; you can see that you never end up with white-on-white, nor black-on-black, though it's possible to use the threshold to permit lower-contrast outcomes, as in the last example:

这些例子使用上面计算的颜色用于背景和前景;你可以看到，你永远不会得到白色-白色或黑色-黑色，虽然有可能使用阈值来允许较低对比度的结果，如上面最后一个例子：


![Color 1](holder.js/100x40/#bbbbbb:#000000/text:000000)
![Color 1](holder.js/100x40/#222222:#ffffff/text:ffffff)
![Color 1](holder.js/100x40/#222222:#dddddd/text:dddddd)
![Color 1](holder.js/100x40/#80ff00:#000000/text:000000)
![Color 1](holder.js/100x40/#80ff00:#ffffff/text:ffffff)
