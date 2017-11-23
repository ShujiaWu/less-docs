---
title: 语言特性快速预览
---

> As an extension to CSS, Less is not only backwards compatible with CSS, but the extra features it adds use existing CSS syntax. This makes learning Less a breeze, and if in doubt, lets you fall back to vanilla CSS.

> Less 作为 CSS 的扩展，不仅能够兼容 CSS 语法 ，而且新增的扩展特性也是使用原有的语法。这使得学习 Less 更为简单，而且你可以在任何时候回退到普通的 CSS。

### 1. 变量

These are pretty self-explanatory:

这是非常好理解的：

```less
@nice-blue: #5B83AD;
@light-blue: @nice-blue + #111;

#header {
  color: @light-blue;
}
```

输出:

```css
#header {
  color: #6c94be;
}
```

Note that variables are actually "constants" in that they can only be defined once.

注意：变量实际上应该说是“常量”更合适，他们只能被定义一次。


### 2. 混合（Mixins）

Mixins are a way of including ("mixing in") a bunch of properties from one rule-set into another rule-set. So say we have the following class:

混合（Mixins）是一种将一系列属性从一个样式集包含到另外一个样式集的方法。例如我们有下面一个类样式：

```css
.bordered {
  border-top: dotted 1px black;
  border-bottom: solid 2px black;
}
```

And we want to use these properties inside other rule-sets. Well, we just have to drop in the name of the class where we want the properties, like so:

如果我们想在另外一个样式集中包含这个样式集的所有属性，我们只需要在我们希望加入的地方写上对应的类名即可，例如：

```less
#menu a {
  color: #111;
  .bordered;
}

.post a {
  color: red;
  .bordered;
}
```

The properties of the `.bordered` class will now appear in both `#menu a` and `.post a`. (Note that you can also use `#ids` as mixins.)

`.bordered` 中的样式就出现在 `#menu a` 和 `.post a`。（当然你也可以在混合中使用 `id选择器`）

**获取更多信息**

* [关于混合（Mixins）的更多信息](#mixins-feature)
* [带参数的混合（Mixins）](#mixins-parametric-feature)


### 3. 嵌套规则

Less gives you the ability to use nesting instead of, or in combination with cascading. Let's say we have the following CSS:

Less 让你在 CSS 中可以使用嵌套或者组合级联，让我们来看一下下面的 CSS：

```css
#header {
  color: black;
}
#header .navigation {
  font-size: 12px;
}
#header .logo {
  width: 300px;
}
```

In Less, we can also write it this way:

在 Less 中我们可以这么写：

```less
#header {
  color: black;
  .navigation {
    font-size: 12px;
  }
  .logo {
    width: 300px;
  }
}
```

The resulting code is more concise, and mimics the structure of your HTML.

这样写使代码更加简洁，有点类似于 HTML 的结构。

You can also bundle pseudo-selectors with your mixins using this method. Here's the classic clearfix hack, rewritten as a mixin (`&` represents the current selector parent):

你也可以用这种方法捆绑使用伪选择器。下面是重写后的经典清除浮动的hack （`&`表示的是当前的选择器）

```less
.clearfix {
  display: block;
  zoom: 1;

  &:after {
    content: " ";
    display: block;
    font-size: 0;
    height: 0;
    clear: both;
    visibility: hidden;
  }
}
```

**参见**

* [父选择器](#parent-selectors-feature)

### 4. 嵌套指令和冒泡

Directives such as `media` or `keyframe` can be nested in the same way as selectors. Directive is placed on top and relative order against other elements inside the same ruleset remains unchanged. This is called bubbling.

`media` 或 `keyframe` 等指令同样可以使用相同的方法进行嵌套。相对于同一规则集，除指令外的其他元素的位置是固定不变的，而指令会被放到相应规则集的前面，这个被称为冒泡。

Conditional directives e.g. `@Media`, `@supports` and `@document` have also selectors copied into their bodies:

条件指令例如 `@Media`, `@supports` 和 `@document` 会对选择器进行复制：

```less
.screen-color {
  @media screen {
    color: green;
    @media (min-width: 768px) {
      color: red;
    }
  }
  @media tv {
    color: black;
  }
}

```

输出:

```css
@media screen {
  .screen-color {
    color: green;
  }
}
@media screen and (min-width: 768px) {
  .screen-color {
    color: red;
  }
}
@media tv {
  .screen-color {
    color: black;
  }
}
```

Remaining non-conditional directives, for example `font-face` or `keyframes`, are bubbled up too. Their bodies do not change:

剩下的非条件指令，例如 `font-face` or `keyframes`，同样会冒泡，但是他们不会复制选择器：

```less
#a {
  color: blue;
  @font-face {
    src: made-up-url;
  }
  padding: 2 2 2 2;
}
```

输出:

```less
#a {
  color: blue;
}
@font-face {
  src: made-up-url;
}
#a {
  padding: 2 2 2 2;
}
```

### 5. 运算

Arithmetical operations `+`, `-`, `*`, `/` can operate on any number, color or variable. If it is possible, mathematical operations take units into account and convert numbers before adding, subtracting or comparing them. The result has leftmost explicitly stated unit type. If the conversion is impossible or not meaningful, units are ignored. Example of impossible conversion: px to cm or rad to %.

算术运算符 `+`, `-`, `*`, `/` 能够运用在任意的数字、颜色或者变量上。算术运算符还可以理解单位，他们在做运算之前会进行转换。运算的结果包含正确的单位。如果转换后的单位不正确或者没有意义，那么单位将会被忽略。可以被理解转换的单位有：px => cm 或者 rad => %。

```less
// 算术运算将会被转换成相同的单位
@conversion-1: 5cm + 10mm; // result is 6cm
@conversion-2: 2 - 3cm - 5mm; // result is -1.5cm

// 以下单位转换是可行的
@incompatible-units: 2 + 5px - 3cm; // result is 4px

// 包含变量的算术运算
@base: 5%;
@filler: @base * 2; // result is 10%
@other: @base + @filler; // result is 15%
```

Multiplication and division do not convert numbers. It would not be meaningful in most cases - a length multiplied by a length gives an area and css does not support specifying areas. Less will operate on numbers as they are and assign explicitly stated unit type to the result.

乘法运算和除法运算是不会进行算术转换的。在大多数情况下是没有意义的， 在数学上，长度乘以长度将等到一个面积，然而 CSS 是不支持面积的。Less 只会在明确规定的单位类型上做算术运算。

```less
@base: 2cm * 3mm; // result is 6cm
```

Colors are split into their red, green, blue and alpha dimensions. The operation is applied to each color dimension separately. E.g., if the user added two colors, then the green dimension of the result is equal to sum of green dimensions of input colors. If the user multiplied a color by a number, each color dimension will get multiplied.

颜色将会被拆分成红、绿、蓝、透明度四个维度。颜色运算是分别对颜色的每一个维度进行运算。例如，如果你将两个颜色进行相加，那么绿色维度的结果是两个颜色的绿色维度的值进行相加。如果你将颜色值乘以一个数字，那么每个维度的值都会乘以这个数字。

Note: arithmetic operation on alpha is not defined, because math operation on colors do not have standard agreed upon meaning. Do not rely on current implemention as it [may change](https://github.com/less/less.js/issues/2694) in later versions.

注意：颜色值透明度维度在数学运算上暂时没有被定义，因为在颜色上的数学运算没有标准的约定。不要依赖当前的实现，在下一个版本或许会发生[改变](https://github.com/less/less.js/issues/2694)

An operation on colors always produces valid color. If some color dimension of the result ends up being bigger than `ff` or smaller than `00`, the dimension is rounded to either `ff` or `00`. If alpha ends up being bigger than `1.0` or smaller than `0.0`, the alpha is rounded to either `1.0` or `0.0`.

任意一个颜色运算都将产生合法的颜色值。如果任意一个维度的值超过 `ff` 或者小于 `00`, 那么他们会被设置为 `ff` 或者 `00`。如果透明度超过 `1.0` 或者小于 `0.0`,同样会被设置为 `1.0` 或 `0.0`。

```less
@color: #224488 / 2; //results in #112244
background-color: #112244 + #111; // result is #223355
```

### 6. 转义

Escaping allows you to use any arbitrary string as property or variable value. Anything inside `~"anything"` or `~'anything'` is used as is with no changes except [interpolation](#variables-feature-variable-interpolation).

转义允许你使用任意的字符串作为属性或者变量的值。`~"anything"` 或 `~'anything'` 常当做原始值使用，除了[插值](#variables-feature-variable-interpolation)。

```less
.weird-element {
  content: ~"^//* some horrible but needed css hack";
}
```

结果:

```less
.weird-element {
  content: ^//* some horrible but needed css hack;
}
```

### 7. 函数

Less provides a variety of functions which transform colors, manipulate strings and do maths. They are documented fully in the function reference.

Less 提供了一系列用于颜色转换、字符串操作、数学运算的函数。在函数参考中可以查阅详细的文档。

Using them is pretty straightforward. The following example uses percentage to convert 0.5 to 50%, increases the saturation of a base color by 5% and then sets the background color to one that is lightened by 25% and spun by 8 degrees:

使用函数非常简单。下面是例子展示将 0.5 转换成 50% ，将一个颜色的饱和度增加 5%，将一个颜色的亮度提高 25%，将色相旋转 8 度并设置为背景颜色。

```less
@base: #f04615;
@width: 0.5;

.class {
  width: percentage(@width); // returns `50%`
  color: saturate(@base, 5%);
  background-color: spin(lighten(@base, 25%), 8);
}
```

### 8. Namespaces and Accessors

(Not to be confused with [CSS `@namespace`](http://www.w3.org/TR/css3-namespace/) or [namespace selectors](http://www.w3.org/TR/css3-selectors/#typenmsp)).

(不要跟 [CSS `@namespace`](http://www.w3.org/TR/css3-namespace/) 或 [namespace selectors](http://www.w3.org/TR/css3-selectors/#typenmsp) 混淆).

Sometimes, you may want to group your mixins, for organizational purposes, or just to offer some encapsulation. You can do this pretty intuitively in Less, say you want to bundle some mixins and variables under `#bundle`, for later reuse or distributing:

有时候，你可能为了组织目的或者提供一些封装，想将混合（mixins） 进行分组。在 Less 中这中做法非常直观，比如你为了以后重用或者发布想将一些混合（mixins）或者变量捆绑到 `#bundle` 中：

```less
#bundle {
  .button {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover {
      background-color: white
    }
  }
  .tab { ... }
  .citation { ... }
}
```

Now if we want to mixin the `.button` class in our `#header a`, we can do:

如果你想将 `.button` 类选择器的样式混合到 `#header a` 中，我们可以这么做：

```less
#header a {
  color: orange;
  #bundle > .button;
}
```

Note that variables declared within a namespace will be scoped to that namespace only and will not be available outside of the scope via the same syntax that you would use to reference a mixin (`#Namespace > .mixin-name`). So, for example, you can't do the following: (`#Namespace > @this-will-not-work`).

注意：在命名空间中声明的变量只能作用于该命名空间，你不能在作用域之外像使用混合（mixin）语法 (`#Namespace > .mixin-name`) 一样使用边用。例如：这样是不允许的 (`#Namespace > @this-will-not-work`)。

### 9. 作用域

Scope in Less is very similar to that of programming languages. Variables and mixins are first looked for locally, and if they aren't found, the compiler will look in the parent scope, and so on.

Less 的作用域与其他编程语言的作用域非常类似。使用变量、混合（mixins）时，会首先在本地（当前作用域）寻找，如果找不到，编译器会在他的父作用域继续寻找，直到找到为止。

```less
@var: red;

#page {
  @var: white;
  #header {
    color: @var; // white
  }
}
```

Variables and mixins do not have to be declared before being used so the following Less code is identical to the previous example:

变量和混合（mixins）的声明不需要强制放在它们的使用之前，下面的代码与前面的代码是一致的：

```less
@var: red;

#page {
  #header {
    color: @var; // white
  }
  @var: white;
}
```

**参见**

* [Lazy Loading](#variables-feature-lazy-loading)


### 10. 注释

Both block-style and inline comments may be used:

Less 可以使用块级注释和行内注释：

```less
/* One hell of a block
style comment! */
@var: red;

// Get in line!
@var: white;
```

### 11. 导入

Importing works pretty much as expected. You can import a `.less` file, and all the variables in it will be available. The extension is optionally specified for `.less` files.

和你预期的工作方式一样。你可以导入一个 `.less` 文件， 此文件中的所有变量都可以使用。如果导入的文件以 `.less` 为扩展名名，则可以省略该扩展名

```css
@import "library"; // library.less
@import "typo.css";
```
