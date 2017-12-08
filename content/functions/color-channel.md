### hue

> Extracts the hue channel of a color object in the HSL color space.

> 从 HSL 颜色空间的颜色对象中提取色相的值。

参数： `color` - 颜色对象。

返回： `integer` 0-360

例子： `hue(hsl(90, 100%, 50%))`

输出： `90`


### saturation

> Extracts the saturation channel of a color object in the HSL color space.

> 从 HSL 颜色空间的颜色对象中提取饱和度的值。

参数： `color` - 颜色对象。

返回： `percentage` 0-100

例子： `saturation(hsl(90, 100%, 50%))`

输出： `100%`


### lightness

> Extracts the lightness channel of a color object in the HSL color space.

> 从 HSL 颜色空间的颜色对象中提取亮度的值。

参数： `color` - 颜色对象。

返回： `percentage` 0-100

例子： `lightness(hsl(90, 100%, 50%))`

输出： `50%`


### hsvhue

> Extracts the hue channel of a color object in the HSV color space.

> 从 HSV 颜色空间的颜色对象中提色相的值。

参数： `color` - 颜色对象。

返回： `integer` `0-360`

例子： `hsvhue(hsv(90, 100%, 50%))`

输出： `90`


### hsvsaturation

> Extracts the saturation channel of a color object in the HSV color space.

> 从 HSV 颜色空间的颜色对象中饱和度的值。

参数： `color` - 颜色对象。

返回： `percentage` 0-100

例子： `hsvsaturation(hsv(90, 100%, 50%))`

输出： `100%`


### hsvvalue

> Extracts the value channel of a color object in the HSV color space.

> 从 HSV 颜色空间的颜色对象中提色调的值。

参数： `color` - 颜色对象。

返回： `percentage` 0-100

例子： `hsvvalue(hsv(90, 100%, 50%))`

输出： `50%`


### red

> Extracts the red channel of a color object.

> 提取颜色对象的红色值。

参数： `color` - 颜色对象。

返回： `float` 0-255

例子： `red(rgb(10, 20, 30))`

输出： `10`


### green

> Extracts the green channel of a color object.

> 提取颜色对象的绿色值。

参数： `color` - 颜色对象。

返回： `float` 0-255

例子： `green(rgb(10, 20, 30))`

输出： `20`


### blue

> Extracts the blue channel of a color object.

> 提取颜色对象的蓝色值。

参数： `color` - 颜色对象。

返回： `float` 0-255

例子： `blue(rgb(10, 20, 30))`

输出： `30`


### alpha

> Extracts the alpha channel of a color object.

> 提取颜色对象的 alpha 值。

参数： `color` - 颜色对象。

返回： `float` 0-1

例子： `alpha(rgba(10, 20, 30, 0.5))`

输出： `0.5`


### luma

> Calculates the [luma](http://en.wikipedia.org/wiki/Luma_%28video%29) (perceptual brightness) of a color object.

> 计算颜色对象的 [luma](http://en.wikipedia.org/wiki/Luma_%28video%29) (亮度的百分比形式)

Uses **SMPTE C / Rec. 709** coefficients, as recommended in [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef). This calculation is also used in the contrast function.

使用 [WCAG 2.0](http://www.w3.org/TR/2008/REC-WCAG20-20081211/#relativeluminancedef) 推荐的 **SMPTE C / Rec. 709** 系数。这个计算也被用在对比函数中。

Before v1.7.0 the luma was calculated without gamma correction, use the luminance function to calculate these "old" values.

在 v1.7.0 之前，luma 的计算没有 gamma 修正，使用 luminance 函数计算以前的那些写。

参数： `color` - 颜色对象。

返回： `percentage` 0-100%

例子： `luma(rgb(100, 200, 30))`

输出： `44%`


### luminance

> Calculates the value of the luma without gamma correction (this function was named `luma` before v1.7.0)

计算没有 gamma 修正的 luma 值（这个函数在 v1.7.0 之前的命名是 `luma`）

参数： `color` - 颜色对象。

返回： `percentage` 0-100%

例子： `luminance(rgb(100, 200, 30))`

输出： `65%`
