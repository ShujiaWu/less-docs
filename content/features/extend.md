> Extend is a Less pseudo-class which merges the selector it is put on with ones that match what it references.

> 继承（Extend） 是 Less 的伪类，它将选择器与它所引用的对象相结合。

Released [v1.4.0]({{ less.master.url }}CHANGELOG.md)

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
```

In the rule set above, the `:extend` selector will apply the "extending selector" (`nav ul`) onto the `.inline` class _wherever the `.inline` class appears_. The declaration block will be kept as-is, but without any reference to the extend (because extend isn't css).

上面的样式规则集中，`:extend` 选择器将“继承选择器” ( `nav ul` ) 添加到 `.inline` 类上（不管 `.inline` 出现在哪里）。声明的代码块将保持原样，但不包含 extend 那部分（因为 extend不是 CSS 语法）。

例子:

```less
nav ul {
  &:extend(.inline);
  background: blue;
}
.inline {
  color: red;
}
```

输出

```css
nav ul {
  background: blue;
}
.inline,
nav ul {
  color: red;
}
```

Notice how the `nav ul:extend(.inline)` selector gets output as `nav ul` - the extend gets removed before output and the selector block left as-is. If no properties are put in that block then it gets removed from the output (but the extend still may affect other selectors).

注意：`nav ul:extend(.inline)` 选择器是如何从 `nav ul` 获取输出样式呢？ extend 在输出样式之前将被移除，原选择器里面的内容将保持不变。如果原来的选择器没有内容，则会被移除（但是 extend 可能对其他的选择器产生影响）。

### 1. 继承（Extend）语法
The extend is either attached to a selector or placed into a ruleset. It looks like a pseudo-class with selector parameter optionally followed by the keyword `all`:

继承（extend）不仅可以附加到选择器上，还可以放在规则集中。它看起来像一个后面带关键字`all`参数的选择器伪类。

Example:

```less
.a:extend(.b) {}

// 上面代码和下面代码的结果是一致的

.a {
  &:extend(.b);
}
```

```less
.c:extend(.d all) {
  // 继承（extend）所有包含 ".d" 的选择器 例如 ".x.d" or ".d.x"
}
.c:extend(.d) {
  // 输出结果只继承（extend）".d" 选择器
}
```

It can contain one or more classes to extend, separated by commas.

它可以继承（extend）一个或多个类选择器,多个选择器通过逗号分隔符。

例如:

```less
.e:extend(.f) {}
.e:extend(.g) {}

// 上面的代码和下面的代码做同样的事情
.e:extend(.f, .g) {}
```

### 2. 附加在选择器上的继承
Extend attached to a selector looks like an ordinary pseudo-class with selector as a parameter. A selector can contain multiple extend clauses, but all extends must be at the end of the selector.

附加在选择器上的继承（extend）看起来像是一个普通的带参数的的伪类选择器。每一个选择器可以包含多个继承（extend），但是每一个继承（extend）必须在选择器的结尾。

* Extend after the selector: `pre:hover:extend(div pre)`.
* Space between selector and extend is allowed: `pre:hover :extend(div pre)`.
* Multiple extends are allowed: `pre:hover:extend(div pre):extend(.bucket tr)` - Note this is the same as `pre:hover:extend(div pre, .bucket tr)`
* This is NOT allowed: `pre:hover:extend(div pre).nth-child(odd)`. Extend must be last.

* Extend 位于选择器后面: `pre:hover:extend(div pre)`。
* 选择器和 Extend 中间有空格是允许的： `pre:hover :extend(div pre)`。
* 可以包含多个继承（extend）：`pre:hover:extend(div pre):extend(.bucket tr)` - 这相当于 `pre:hover:extend(div pre, .bucket tr)` 。
* 这是不允许出现的： `pre:hover:extend(div pre).nth-child(odd)`。继承（extend）必须位于选择器的最后。

If a ruleset contains multiple selectors, any of them can have the extend keyword. Multiple selectors with extend in one ruleset:

如果一个规则集中包含多个选择器，他们每一个都可以使用继承（extend）。下面是一个规则集中有两个选择器使用了继承（extend）：

```less
.big-division,
.big-bag:extend(.bag),
.big-bucket:extend(.bucket) {
  // body
}
```

### 3. 位于规则集内部的继承
Extend can be placed into a ruleset's body using `&:extend(selector)` syntax. Placing extend into a body is a shortcut for placing it into every single selector of that ruleset.

继承（extend）可以使用 `&:extend(selector)` 的语法在规则集内部使用。在规则集内部使用继承（extend）是单个规则集的选择器的一种快捷方式。

Extend inside a body:

规则集内部的继承（extend）：

```less
pre:hover,
.some-class {
  &:extend(div pre);
}
```

is exactly the same as adding an extend after each selector:

上面的代码效果跟使用位于选择器后面的继承（extend）是一样的：

```less
pre:hover:extend(div pre),
.some-class:extend(div pre) {}
```

### 4. 继承嵌套的选择器
Extend is able to match nested selectors. Following less:

继承（extend）可以匹配嵌套的的选择器。

Example:

例子：

```less
.bucket {
  tr { // nested ruleset with target selector
    color: blue;
  }
}
.some-class:extend(.bucket tr) {} // nested ruleset is recognized
```

Outputs

```css
.bucket tr,
.some-class {
  color: blue;
}
```

Essentially the extend looks at the compiled css, not the original less.

实际上，继承是根据编译后的 css ，而不是原始的 less。

Example:

例如：

```less
.bucket {
  tr & { // nested ruleset with target selector
    color: blue;
  }
}
.some-class:extend(tr .bucket) {} // nested ruleset is recognized
```

Outputs

输出：

```css
tr .bucket,
.some-class {
  color: blue;
}
```

### 5. 使用精确匹配的继承
Extend by default looks for exact match between selectors. It does matter whether selector uses leading star or not. It does not matter that two nth-expressions have the same meaning, they need to have to same form in order to be matched. The only exception are quotes in attribute selector, less knows they have the same meaning and matches them.

选择器的继承（extend）默认是精确匹配的。它不管选择器是否使用前导 * 号通配符，也不管两个nth-表达式的结果是否一致，它们要求格式必须完全一直。只有属性选择器的引号是例外的，Less 能够识别和匹配不同引号。

例如:

```less
.a.class,
.class.a,
.class > .a {
  color: blue;
}
.test:extend(.class) {} // this will NOT match the any selectors above
```

Leading star does matter. Selectors `*.class` and `.class` are equivalent, but extend will not match them:

前导 * 是会影响匹配结果的。`*.class` 和 `.class` 选择器是一致的，但是继承（extend）不会匹配他们：

```less
*.class {
  color: blue;
}
.noStar:extend(.class) {} // this will NOT match the *.class selector
```

Outputs

输出：

```css
*.class {
  color: blue;
}
```

Order of pseudo-classes does matter. Selectors `link:hover:visited` and `link:visited:hover` match the same set of elements, but extend treats them as different:

伪类的顺序也是会影响匹配的结果。`link:hover:visited` 和 `link:visited:hover` 作用于相同的元素上， 但是继承（extend）却把它们当成不一样：

```less
link:hover:visited {
  color: blue;
}
.selector:extend(link:visited:hover) {}
```

Outputs

输出：

```css
link:hover:visited {
  color: blue;
}
```

### 6. nth 表达式

Nth expression form does matter. Nth-expressions `1n+3` and `n+3` are equivalent, but extend will not match them:

Nth 表达式的格式也是会影响匹配的结果。Nth 表达式 `1n+3` 和 `n+3` 效果是一致的，但是继承（extend）认为它们不匹配

```less
:nth-child(1n+3) {
  color: blue;
}
.child:extend(:nth-child(n+3)) {}
```

Outputs

输出：

```css
:nth-child(1n+3) {
  color: blue;
}
```

Quote type in attribute selector does not matter. All of the following are equivalent.

属性选择器中的引号类型不会影响匹配的结果。下面列出来的情况都是一致的：

```less
[title=identifier] {
  color: blue;
}
[title='identifier'] {
  color: blue;
}
[title="identifier"] {
  color: blue;
}

.noQuote:extend([title=identifier]) {}
.singleQuote:extend([title='identifier']) {}
.doubleQuote:extend([title="identifier"]) {}
```

Outputs

输出：

```css
[title=identifier],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title='identifier'],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}

[title="identifier"],
.noQuote,
.singleQuote,
.doubleQuote {
  color: blue;
}
```

### 7. 使用 "all" 的继承

When you specify the all keyword last in an extend argument it tells Less to match that selector as part of another selector. The selector will be copied and the matched part of the selector only will then be replaced with the extend, making a new selector.

当你在继承的参数中使用 “all” 关键字，less 将对选择器进行进行部分匹配。被继承的选择器将会被复制并替换被匹配的那一部分，并形成一个新的选择器。

Example:

例如：

```less
.a.b.test,
.test.c {
  color: orange;
}
.test {
  &:hover {
    color: green;
  }
}

.replacement:extend(.test all) {}
```

Outputs

```css
.a.b.test,
.test.c,
.a.b.replacement,
.replacement.c {
  color: orange;
}
.test:hover,
.replacement:hover {
  color: green;
}
```

_You can think of this mode of operation as essentially doing a non-destructive search and replace._

_你可以认为这本质上是一种非破坏性的查找和替换的操作模式。_


### 8. 带插值的选择器的继承
> Extend is NOT able to match selectors with variables. If selector contains variable, extend will ignore it.

> 继承（extend）不能匹配那些带名称中变量的选择器。如果一个选择器的名称中带有变量，那么继承（extend）将会忽略它。

There is a pending feature request for this but it is not an easy change.  However, extend can be attached to interpolated selector.

这是一个请求被附加的特性，但是这不是一个轻易的变更。然而继承（extend）可以被附加到带插值的选择器上。

Selector with variable will not be matched:

选择器上带有变量将不会被匹配：

```less
@variable: .bucket;
@{variable} { // interpolated selector
  color: blue;
}
.some-class:extend(.bucket) {} // does nothing, no match is found
```

and extend with variable in target selector matches nothing:

继承的目标是一个变量也不会进行匹配：

```less
.bucket {
  color: blue;
}
.some-class:extend(@{variable}) {} // interpolated selector matches nothing
@variable: .bucket;
```

Both of the above examples compile into:

上面的例子编译后都是：

```less
.bucket {
  color: blue;
}
```

However, `:extend` attached to an interpolated selector works:

然而，`:extend` 可以被附加到一个插值选择器上：

```less
.bucket {
  color: blue;
}
@{variable}:extend(.bucket) {}
@variable: .selector;
```

编译后:

```less
.bucket, .selector {
  color: blue;
}
```

### 9. 媒体查询中的继承及作用域

Extend written inside a media declaration should match only selectors inside the same media declaration:

媒体查询中的继承（extend）只能匹配媒体查询中的选择器。

```less
@media print {
  .screenClass:extend(.selector) {} // extend inside media
  .selector { // this will be matched - it is in the same media
    color: black;
  }
}
.selector { // ruleset on top of style sheet - extend ignores it
  color: red;
}
@media screen {
  .selector {  // ruleset inside another media - extend ignores it
    color: blue;
  }
}
```

编译后:

```css
@media print {
  .selector,
  .screenClass { /*  ruleset inside the same media was extended */
    color: black;
  }
}
.selector { /* ruleset on top of style sheet was ignored */
  color: red;
}
@media screen {
  .selector { /* ruleset inside another media was ignored */
    color: blue;
  }
}
```

Extend written inside a media declaration does not match selectors inside nested declaration:

媒体查询中的继承（extend）是不能匹配嵌套的的媒体查询中的选择器。

```less
@media screen {
  .screenClass:extend(.selector) {} // extend inside media
  @media (min-width: 1023px) {
    .selector {  // ruleset inside nested media - extend ignores it
      color: blue;
    }
  }
}
```

编译后:

```css
@media screen and (min-width: 1023px) {
  .selector { /* ruleset inside another nested media was ignored */
    color: blue;
  }
}
```

Top level extend matches everything including selectors inside nested media:

顶级的继承（extend）可以匹配同级以及嵌套的媒体查询中的选择器。

```less
@media screen {
  .selector {  /* ruleset inside nested media - top level extend works */
    color: blue;
  }
  @media (min-width: 1023px) {
    .selector {  /* ruleset inside nested media - top level extend works */
      color: blue;
    }
  }
}

.topLevel:extend(.selector) {} /* top level extend matches everything */
```

编译后:

```css
@media screen {
  .selector,
  .topLevel { /* ruleset inside media was extended */
    color: blue;
  }
}
@media screen and (min-width: 1023px) {
  .selector,
  .topLevel { /* ruleset inside nested media was extended */
    color: blue;
  }
}
```

### 10. 重复检测

Currently there is no duplication detection.

当前不支持重复检测。

Example:

例如：

```less
.alert-info,
.widget {
  /* declarations */
}

.alert:extend(.alert-info, .widget) {}
```

Outputs

输出：

```css
.alert-info,
.widget,
.alert,
.alert {
  /* declarations */
}
```

### 11. 继承的用例

#### 11.1 典型用例

The classic use case is to avoid adding a base class. For example, if you have

典型应用是避免添加基类，例如，假设你有一下代码：

```css
.animal {
  background-color: black;
  color: white;
}
```

and you want to have a subtype of animal which overrides the background color then you have two options, firstly change your HTML

然后你想用一个子类型的动物选择器重写 background-color 覆盖父类型的样式，你有两种方式来实现。第一种是，更改你的HTML代码：

```html
<a class="animal bear">Bear</a>
```

```css
.animal {
  background-color: black;
  color: white;
}
.bear {
  background-color: brown;
}
```

or have simplified html and use extend in your less. e.g.

或者是，使用简单的 HTML 代码，然后在 Less 中使用继承（extend）来实现，例如：

```html
<a class="bear">Bear</a>
```

```less
.animal {
  background-color: black;
  color: white;
}
.bear {
  &:extend(.animal);
  background-color: brown;
}
```

#### 11.2 减少 CSS 的体积

Mixins copy all of the properties into a selector, which can lead to unnecessary duplication. Therefore you can use extends instead of mixins to move the selector up to the properties you wish to use, which leads to less CSS being generated.

混合（mixins）会把样式属性复制到选择器中，这会导致没必要的重复。因此，你可以使用继承（extend）代替混合（mixins），将目标选择器添加到你想要使用的样式的选择器上，这会减少less生成的 CSS 样式。

Example - with mixin:

例如，使用混合（mixin）：

```less
.my-inline-block() {
  display: inline-block;
  font-size: 0;
}
.thing1 {
  .my-inline-block;
}
.thing2 {
  .my-inline-block;
}
```

Outputs

输出：

```css
.thing1 {
  display: inline-block;
  font-size: 0;
}
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

Example (with extends):

例如，使用继承（extend）：

```less
.my-inline-block {
  display: inline-block;
  font-size: 0;
}
.thing1 {
  &:extend(.my-inline-block);
}
.thing2 {
  &:extend(.my-inline-block);
}
```

Outputs

输出：

```css
.my-inline-block,
.thing1,
.thing2 {
  display: inline-block;
  font-size: 0;
}
```

#### 11.3 组合使用样式 / 更高级的混合

Another use-case is as an alternative for a mixin - because mixins can only be used with simple selectors, if you have two different blocks of html, but need to apply the same styles to both you can use extends to relate two areas.

这是另外一种作为混合（mixin）的代替的用例，原因是混合（mixins）只能使用单一的选择器，如果你在 HTML 中有两个不同块，但是又想使用相同的样式代码，你可以使用继承（extend）来关联着两个区域。

Example:

例如：

```less
li.list > a {
  // list styles
}
button.list-style {
  &:extend(li.list > a); // use the same list styles
}
```
