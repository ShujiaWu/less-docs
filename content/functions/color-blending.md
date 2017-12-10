> These operations are _similar_ (though not necessarily identical) to the blend modes found in image editors like Photoshop, Fireworks, or GIMP, so you can use them to make your CSS colors match your images.

> 这些操作和图片编辑器（例如 Photoshop、Fireworks 或 GIMP）中的混合模式很类似（虽然不是完全一致），因此，你可以通过这些函数让 CSS 中的颜色与图片中的颜色相匹配。

### multiply

> Multiply two colors. Corresponding RGB channels from each of the two colors are multiplied together then divided by 255. The result is a darker color.

> 将两个颜色相乘，相当于 RGB 的每一个通道的颜色值相乘然后除以 255. 结果是一个更暗的颜色。

参数：

* `color1`: 颜色对象。
* `color2`: 颜色对象。

返回： `color`

**例子**:

```less
multiply(#ff6600, #000000);
```
![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
multiply(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#331400:#ffffff/text:331400)

```less
multiply(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
multiply(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#993d00:#ffffff/text:993d00)

```less
multiply(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
multiply(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
multiply(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
multiply(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
multiply(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)


### screen

> Do the opposite of `multiply`. The result is a brighter color.

> 与 `multiply` 相反，结果是一个更亮的颜色。

参数：

* `color1`: 颜色对象。
* `color2`: 颜色对象。

返回： `color`

例子：

```less
screen(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
screen(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ffa366:#ffffff/text:ffa366)

```less
screen(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ffc299:#000000/text:ffc299)

```less
screen(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffe0cc:#000000/text:ffe0cc)

```less
screen(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
screen(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
screen(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffff00:#ffffff/text:ffff00)

```less
screen(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### overlay

> Combines the effects of both `multiply` and `screen`. Conditionally make light channels lighter and dark channels darker. **Note**: The results of the conditions are determined by the first color parameter.

> 结合 `multiply` 与 `screen` 两个函数的效果，令浅的颜色变得更浅，深的颜色变得更深。注意：输出结果由第一个颜色参数决定。

参数：

* `color1`: 基准颜色对象。也就是用以确定最终结果是浅些还是深些的参考色。
* `color2`: 颜色对象。

返回： `color`

例子：

```less
overlay(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
overlay(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5200:#ffffff/text:ff5200)

```less
overlay(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7a00:#ffffff/text:ff7a00)

```less
overlay(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffa300:#ffffff/text:ffa300)

```less
overlay(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
overlay(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffcc00:#ffffff/text:ffcc00)

```less
overlay(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)


### softlight

> Similar to `overlay` but avoids pure black resulting in pure black, and pure white resulting in pure white.

> 与 `overlay` 类似，但是当纯黑色或纯白色作为参数时输出结果不会是纯黑色或纯白色。

参数：

* `color1`: 用于柔光另外一个颜色的颜色对象。
* `color2`: 被柔光的颜色对象。

返回： `color`

例子：

```less
softlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#ff4100:#ffffff/text:ff4100)

```less
softlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#ff5a00:#ffffff/text:ff5a00)

```less
softlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff7200:#ffffff/text:ff7200)

```less
softlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ff8a00:#ffffff/text:ff8a00)

```less
softlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)

```less
softlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ffa100:#ffffff/text:ffa100)

```less
softlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff2900:#ffffff/text:ff2900)


### hardlight

> The same as `overlay` but with the color roles reversed.

> 和 `overlay` 类似，但是作用相反。

参数：

* `color1`: 光源颜色对象。
* `color2`: 基准色对象。它决定最终结果是亮些还是暗些。

返回： `color`

例子：

```less
hardlight(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#000000:#ffffff/text:000000)

```less
hardlight(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#662900:#ffffff/text:662900)

```less
hardlight(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#cc5200:#ffffff/text:cc5200)

```less
hardlight(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#ff8533:#ffffff/text:ff8533)

```less
hardlight(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#ffc299:#ffffff/text:ffc299)

```less
hardlight(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffffff:#000000/text:ffffff)

```less
hardlight(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff0000:#ffffff/text:ff0000)

```less
hardlight(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#00ff00:#ffffff/text:00ff00)

```less
hardlight(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#0000ff:#ffffff/text:0000ff)


### difference

> Subtracts the second color from the first color on a channel-by-channel basis. Negative values are inverted. Subtracting black results in no change; subtracting white results in color inversion.

第一个颜色减去第二个颜色（基于每一个通道的值）。负值将会被反转。减去黑色结果不变，减去白色结果反转。

参数：

* `color1`: 被减的颜色对象。
* `color2`: 减去的颜色对象。

返回： `color`

例子：

```less
difference(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
difference(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc3333:#ffffff/text:cc3333)

```less
difference(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#990066:#ffffff/text:990066)

```less
difference(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#663399:#ffffff/text:663399)

```less
difference(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#3366cc:#ffffff/text:3366cc)

```less
difference(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
difference(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
difference(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
difference(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### exclusion

> A similar effect to `difference` with lower contrast.

> 与 `difference` 效果类似，只是输出结果对比度更小。

参数：

* `color1`: 被减的颜色对象。
* `color2`: 减去的颜色对象。

返回： `color`

例子：

```less
exclusion(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
exclusion(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc7033:#ffffff/text:cc7033)

```less
exclusion(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#997a66:#ffffff/text:997a66)

```less
exclusion(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#668599:#ffffff/text:668599)

```less
exclusion(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#338fcc:#ffffff/text:338fcc)

```less
exclusion(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
exclusion(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
exclusion(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
exclusion(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#000000/text:ff66ff)


### average

> Compute the average of two colors on a per-channel (RGB) basis.

> 计算两个颜色基于 （RGB） 每个通道的平均值。

参数：

* `color1`: 颜色对象。
* `color2`: 颜色对象。

返回： `color`

例子：

```less
average(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#803300:#ffffff/text:803300)

```less
average(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#994d1a:#ffffff/text:994d1a)

```less
average(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#b36633:#ffffff/text:b36633)

```less
average(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#cc804d:#ffffff/text:cc804d)

```less
average(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#e69966:#ffffff/text:e69966)

```less
average(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#ffb380:#000000/text:ffb380)

```less
average(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#ff3300:#ffffff/text:ff3300)

```less
average(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#80b300:#ffffff/text:80b300)

```less
average(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#803380:#ffffff/text:803380)

### negation

> Do the opposite effect to `difference`.

> 与 `difference` 的效果相反。

The result is a brighter color. **Note**: The _opposite_ effect doesn't mean the _inverted_ effect as resulting from an _addition_ operation.

操作的结果是更亮的颜色。**注意**：相反的结果并不意味着做加法运算。

参数：

* `color1`: 被减的颜色对象。
* `color2`: 减去的颜色对象。

返回： `color`

例子：

```less
negation(#ff6600, #000000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#000000:#ffffff/text:000000)
![Color 3](holder.js/100x40/#ff6600:#ffffff/text:ff6600)

```less
negation(#ff6600, #333333);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#333333:#ffffff/text:333333)
![Color 3](holder.js/100x40/#cc9933:#ffffff/text:cc9933)

```less
negation(#ff6600, #666666);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#666666:#ffffff/text:666666)
![Color 3](holder.js/100x40/#99cc66:#ffffff/text:99cc66)

```less
negation(#ff6600, #999999);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#999999:#ffffff/text:999999)
![Color 3](holder.js/100x40/#66ff99:#ffffff/text:66ff99)

```less
negation(#ff6600, #cccccc);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#cccccc:#000000/text:cccccc)
![Color 3](holder.js/100x40/#33cccc:#ffffff/text:33cccc)

```less
negation(#ff6600, #ffffff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ffffff:#000000/text:ffffff)
![Color 3](holder.js/100x40/#0099ff:#ffffff/text:0099ff)

```less
negation(#ff6600, #ff0000);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#ff0000:#ffffff/text:ff0000)
![Color 3](holder.js/100x40/#006600:#ffffff/text:006600)

```less
negation(#ff6600, #00ff00);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#00ff00:#ffffff/text:00ff00)
![Color 3](holder.js/100x40/#ff9900:#ffffff/text:ff9900)

```less
negation(#ff6600, #0000ff);
```

![Color 1](holder.js/100x40/#ff6600:#ffffff/text:ff6600)
![Color 2](holder.js/100x40/#0000ff:#ffffff/text:0000ff)
![Color 3](holder.js/100x40/#ff66ff:#ffffff/text:ff66ff)
