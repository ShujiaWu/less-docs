### ceil

> Rounds up to the next highest integer.

> 向上取整

参数： `number` - 浮点数

返回： `integer`

例子： `ceil(2.4)`

输出： `3`


### floor

> Rounds down to the next lowest integer.

> 向下取整

参数： `number` - 浮点数

返回： `integer`

例子： `floor(2.6)`

输出： `2`


### percentage

> Converts a floating point number into a percentage string.

> 将浮点数转换成百分比字符转。

参数： `number` - 浮点数

返回： `string`

例子： `percentage(0.5)`

输出： `50%`


### round

> Applies rounding.

> 四舍五入取整。

参数：
* `number`: 浮点数
* `decimalPlaces`: Optional: The number of decimal places to round to. Defaults to 0.

返回： `number`

例子： `round(1.67)`

输出： `2`

例子： `round(1.67, 1)`

输出： `1.7`

### sqrt

> Calculates square root of a number. Keeps units as they are.

> 计算一个数字的平方根，并保留单位。

参数： `number` - floating point number.

返回： `number`

例子：

```less
sqrt(25cm)
```

输出：

```css
5cm
```

例子：

```less
sqrt(18.6%)
```

输出：

```js
4.312771730569565%;
```

### abs

> Calculates absolute value of a number. Keeps units as they are.

> 计算一个数字的绝对值，并保留单位。

参数： `number` - 浮点数

返回： `number`

例子: `abs(25cm)`

输出： `25cm`

例子: `abs(-18.6%)`

输出： `18.6%;`


### sin

> Calculates sine function.

> 正弦函数。

Assumes radians on numbers without units.

没有单位的数字会被当成弧度。

参数： `number` - 浮点数

返回： `number`

例子：

```less
sin(1); // sine of 1 radian
sin(1deg); // sine of 1 degree
sin(1grad); // sine of 1 gradian
```

输出：

```
0.8414709848078965; // sine of 1 radian
0.01745240643728351; // sine of 1 degree
0.015707317311820675; // sine of 1 gradian
```


### asin

> Calculates arcsine (inverse of sine) function.

> 反余弦函数。

Returns number in radians e.g. a number between `-π/2` and `π/2`.

返回以弧度为单位的角度，区间在 `-π/2` 到 `π/2`。

参数： `number` - `[-1, 1]` 之间的浮点数。

返回： `number`

例子：

```less
asin(-0.8414709848078965)
asin(0)
asin(2)
```

输出：

```
-1rad
0rad
NaNrad
```


### cos

> Calculates cosine function.

> 余弦函数

Assumes radians on numbers without units.

没有单位的数字会被当成弧度。

参数： `number` - 浮点数

返回： `number`

例子：

```less
cos(1) // cosine of 1 radian
cos(1deg) // cosine of 1 degree
cos(1grad) // cosine of 1 gradian
```

输出：

```
0.5403023058681398 // cosine of 1 radian
0.9998476951563913 // cosine of 1 degree
0.9998766324816606 // cosine of 1 gradian
```


### acos

> Calculates arccosine (inverse of cosine) function.

> 反余弦函数

Returns number in radians e.g. a number between 0 and π.

返回以弧度为单位的角度，区间在 `0` 到 `π`。

参数： `number` - [-1, 1] 之间的浮点数.

返回： `number`

例子：

```less
acos(0.5403023058681398)
acos(1)
acos(2)
```

输出：

```
1rad
0rad
NaNrad
```


### tan

> Calculates tangent function.

> 正切函数。

Assumes radians on numbers without units.

没有单位的数字会被当成弧度。

参数： `number` - 浮点数

返回： `number`

例子：

```less
tan(1) // tangent of 1 radian
tan(1deg) // tangent of 1 degree
tan(1grad) // tangent of 1 gradian
```

输出：

```
1.5574077246549023   // tangent of 1 radian
0.017455064928217585 // tangent of 1 degree
0.015709255323664916 // tangent of 1 gradian
```


### atan

> Calculates arctangent (inverse of tangent) function.

> 反正切函数。

Returns number in radians e.g. a number between `-π/2` and `π/2`.

返回以弧度为单位的角度，区间在 `-π/2` 到 `π/2`。

参数： `number` - 浮点数

返回： `number`

例子：

```less
atan(-1.5574077246549023)
atan(0)
round(atan(22), 6) // arctangent of 22 rounded to 6 decimal places
```

输出：

```
-1rad
0rad
1.525373rad;
```


### pi

> Returns &pi; (pi);

> 返回 π (pi);

参数： `none`

返回： `number`

例子：

```less
pi()
```

输出：

```
3.141592653589793
```


### pow

> Returns the value of the first argument raised to the power of the second argument.

> 返回第一个参数的第二个参数次方。

Returned value has the same dimension as the first parameter and the dimension of the second parameter is ignored.

返回值的单位与第一个参数一致，第二个参数的单位会被忽略。

参数：
* `number`: 基数 - 浮点数
* `number`: 指数 - 浮点数

返回： `number`

例子：

```less
pow(0cm, 0px)
pow(25, -2)
pow(25, 0.5)
pow(-25, 0.5)
pow(-25%, -0.5)
```

输出：

```
1cm
0.0016
5
NaN
NaN%
```


### mod

> Returns the value of the first argument modulus second argument.

> 返回第一个参数模第二个参数的值。

Returned value has the same dimension as the first parameter, the dimension of the second parameter is ignored. The function is able to handle also negative and floating point numbers.

返回值的单位与第一个参数一致，第二个参数的单位会被忽略。这个函数同样可以处理负数和浮点数。

参数：
* `number`: 浮点数
* `number`: 浮点数

返回： `number`

例子：

```less
mod(0cm, 0px)
mod(11cm, 6px);
mod(-26%, -5);
```

输出：

```
NaNcm;
5cm
-1%;
```


### min

> Returns the lowest of one or more values.

> 返回多个值中的最小值。

参数： `value1, ..., valueN` - 一个或多个参与比较的值。

返回： 最小值.

例子： `min(5, 10);`

输出： `5`

例子： `min(3px, 42px, 1px, 16px);`

输出： `1px`


### max

> Returns the highest of one or more values.

> 返回一个或多个值中的最大值。

参数： `value1, ..., valueN` - 一个或多个参与比较的值。

返回： 最大值。

例子： `max(5, 10);`

输出： `10`

例子： `max(3%, 42%, 1%, 16%);`

输出： `42%`
