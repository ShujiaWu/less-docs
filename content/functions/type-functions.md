### isnumber

> Returns `true` if a value is a number, `false` otherwise.

> 如果一个值是数字则返回 `true`，否则则返回 `false`。

参数： `value` - 待验证的值或变量。

返回： 如果值是数字则返回 `true` 否则返回 `false`。

例子：

```less
isnumber(#ff0);     // false
isnumber(blue);     // false
isnumber("string"); // false
isnumber(1234);     // true
isnumber(56px);     // true
isnumber(7.8%);     // true
isnumber(keyword);  // false
isnumber(url(...)); // false
```


### isstring

> Returns `true` if a value is a string, `false` otherwise.

> 如果一个值是字符串则返回 `true`，否则则返回 `false`。

参数： `value` - 待验证的值或变量。

返回： 如果值是字符串则返回 `true`, 否则则返回 `false`。

例子：

```less
isstring(#ff0);     // false
isstring(blue);     // false
isstring("string"); // true
isstring(1234);     // false
isstring(56px);     // false
isstring(7.8%);     // false
isstring(keyword);  // false
isstring(url(...)); // false
```


### iscolor

> 如果一个值是颜色则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值是颜色则返回 `true`, 否则则返回 `false`。

例子：

```less
iscolor(#ff0);     // true
iscolor(blue);     // true
iscolor("string"); // false
iscolor(1234);     // false
iscolor(56px);     // false
iscolor(7.8%);     // false
iscolor(keyword);  // false
iscolor(url(...)); // false
```


### iskeyword

> 如果一个值是关键字则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值是关键字串则返回 `true`, 否则则返回 `false`。

例子：

```less
iskeyword(#ff0);     // false
iskeyword(blue);     // false
iskeyword("string"); // false
iskeyword(1234);     // false
iskeyword(56px);     // false
iskeyword(7.8%);     // false
iskeyword(keyword);  // true
iskeyword(url(...)); // false
```


### isurl

> 如果一个值是 url 地址则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值是 url 地址则返回 `true`, 否则则返回 `false`。

例子：

```less
isurl(#ff0);     // false
isurl(blue);     // false
isurl("string"); // false
isurl(1234);     // false
isurl(56px);     // false
isurl(7.8%);     // false
isurl(keyword);  // false
isurl(url(...)); // true
```


### ispixel

> 如果一个值是带像素单位的数字则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值带像素单位则返回 `true`, 否则则返回 `false`。

例子：

```less
ispixel(#ff0);     // false
ispixel(blue);     // false
ispixel("string"); // false
ispixel(1234);     // false
ispixel(56px);     // true
ispixel(7.8%);     // false
ispixel(keyword);  // false
ispixel(url(...)); // false
```


### isem

> 如果一个值是带 em 单位的数字则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值是的单位是 em 则返回 `true`, 否则则返回 `false`。

例子：

```less
isem(#ff0);     // false
isem(blue);     // false
isem("string"); // false
isem(1234);     // false
isem(56px);     // false
isem(7.8em);    // true
isem(keyword);  // false
isem(url(...)); // false
```


### ispercentage

> 如果一个值是百分数则返回 `true` 否则则返回 `false` 。

参数： `value` - 待验证的值或变量。

返回： 如果值是百分数则返回 `true`, 否则则返回 `false`。

例子：

```less
ispercentage(#ff0);     // false
ispercentage(blue);     // false
ispercentage("string"); // false
ispercentage(1234);     // false
ispercentage(56px);     // false
ispercentage(7.8%);     // true
ispercentage(keyword);  // false
ispercentage(url(...)); // false
```


### isunit

> 如果一个值是指定单位的数字则返回 `true` 否则则返回 `false` 。

参数：
* `value` - 待验证的值或变量。
* `unit` - 单位标示符 (可加引号) 。

返回： 如果值包含指定的单位则返回 `true`, 否则则返回 `false`。

例子：

```less
isunit(11px, px);  // true
isunit(2.2%, px);  // false
isunit(33px, rem); // false
isunit(4rem, rem); // true
isunit(56px, "%"); // false
isunit(7.8%, '%'); // true
isunit(1234, em);  // false
isunit(#ff0, pt);  // false
isunit("mm", mm);  // false
```


### isruleset

> 如果一个值是样式集则返回 `true` 否则则返回 `false` 。

参数：
* `value` - 待验证的值或变量。

返回： 如果值是样式集则返回 `true`, 否则则返回 `false`。

例子：

```less
@rules: {
    color: red;
}

isruleset(@rules);   // true
isruleset(#ff0);     // false
isruleset(blue);     // false
isruleset("string"); // false
isruleset(1234);     // false
isruleset(56px);     // false
isruleset(7.8%);     // false
isruleset(keyword);  // false
isruleset(url(...)); // false
```
