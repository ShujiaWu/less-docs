> How to pass arguments to mixins

> 这么将参数传递给混合

Mixins can also take arguments, which are variables passed to the block of selectors when it is mixed in.

混合也可以携带参数，当进行混合的时候，可以通过变量将参数传递给选择器的代码块。

For example:

例如：

```less
.border-radius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

And here's how we can mix it into various rulesets:

下面是如何使用参数混合成各种规则：

```less
#header {
  .border-radius(4px);
}
.button {
  .border-radius(6px);
}
```

Parametric mixins can also have default values for their parameters:

带参数的混合（mixins）它们的参数可以有默认值：

```less
.border-radius(@radius: 5px) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```

We can invoke it like this now:

我们可以像下面一样调用：

```less
#header {
  .border-radius;
}
```

And it will include a 5px border-radius.

上面的规则中将包含 5px 的 border-radius。

You can also use parametric mixins which don't take parameters. This is useful if you want to hide the ruleset from the CSS output, but want to include its properties in other rulesets:

你也可以使用不带任何参数的参数模式的混合（mixins）。这对于你想把其他规则集中的属性混合到样式中，又不想在输出的 CSS 包含改样式集特别有用。

```less
.wrap() {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}

pre { .wrap }
```

Which would output:

它将输出为：

```css
pre {
  text-wrap: wrap;
  white-space: -moz-pre-wrap;
  white-space: pre-wrap;
  word-wrap: break-word;
}
```

### 1. 带多个参数的混合
Parameters are either *semicolon* or *comma* separated. It is recommended to use *semicolon*. The symbol comma has double meaning: it can be interpreted either as a mixin parameters separator or css list separator.

参数使用 *分号* 或者 *逗号* 分隔。推荐使用 *分号* 进行分隔。逗号有两种含义：一种是作为参数的分隔符，另外一种是作为 CSS 属性参数列表的分隔符。

Using comma as mixin separator makes it impossible to create comma separated lists as an argument. On the other hand, if the compiler sees at least one semicolon inside mixin call or declaration, it assumes that arguments are separated by semicolons and all commas belong to css lists:

使用逗号作为混合的分隔符将导致不能使用逗号作为 css 属性参数列表的分隔符。另一方面如果当编译器发现声明或者调用混合中存在一个分号，则假定是以分号进行分隔，所有的逗号都会被当做 css 属性的参数列表分隔符。

* two arguments and each contains comma separated list: `.name(1, 2, 3; something, else)`,
* three arguments and each contains one number: `.name(1, 2, 3)`,
* use dummy semicolon to create mixin call with one argument containing comma separated css list: `.name(1, 2, 3;)`,
* comma separated default value: `.name(@param1: red, blue;)`.

* 两个参数，没个参数都是包含逗号隔开的列表: `.name(1, 2, 3; something, else)`,
* 三个参数，每个参数只包含一个数字: `.name(1, 2, 3)`,
* 使用一个不起作用的分号来创建只带一个 css 属性参数列表的参数的混合: `.name(1, 2, 3;)`,
* 使用逗号分隔默认值: `.name(@param1: red, blue;)`.

It is legal to define multiple mixins with the same name and number of parameters. Less will use properties of all that can apply. If you used the mixin with one parameter e.g. `.mixin(green);`, then properties of all mixins with exactly one mandatory parameter will be used:

定义具有相同名字和参数数量的混合（mixins）是合法的。Less 将会混合所有它能使用的属性。如果你使用一个参数调用混合（mixin），例如 `.mixin(green);` ，所有匹配的混合都会被使用。

```less
.mixin(@color) {
  color-1: @color;
}
.mixin(@color; @padding: 2) {
  color-2: @color;
  padding-2: @padding;
}
.mixin(@color; @padding; @margin: 2) {
  color-3: @color;
  padding-3: @padding;
  margin: @margin @margin @margin @margin;
}
.some .selector div {
  .mixin(#008000);
}
```

compiles into:

```css
.some .selector div {
  color-1: #008000;
  color-2: #008000;
  padding-2: 2;
}
```

### 2. 命名的参数

A mixin reference can supply parameters values by their names instead of just positions. Any parameter can be referenced by its name and they do not have to be in any special order:

混合引用可以通过他们的名字提供参数值，而不仅仅通过对应位置提供。任何参数都可以通过名字被引用，所以没有必要指定他们的顺序。

```less
.mixin(@color: black; @margin: 10px; @padding: 20px) {
  color: @color;
  margin: @margin;
  padding: @padding;
}
.class1 {
  .mixin(@margin: 20px; @color: #33acfe);
}
.class2 {
  .mixin(#efca44; @padding: 40px);
}
```

compiles into:

编译成：

```css
.class1 {
  color: #33acfe;
  margin: 20px;
  padding: 20px;
}
.class2 {
  color: #efca44;
  margin: 10px;
  padding: 40px;
}
```

### 3. `@arguments` 变量

`@arguments` has a special meaning inside mixins, it contains all the arguments passed, when the mixin was called. This is useful if you don't want to deal with individual parameters:

`@arguments` 在混合中有着特殊的意义，它包含所有传递进来的参数。但混合（mixin）被调用的时候，如果你不希望单独处理每一个参数，这将是非常有用的。

```less
.box-shadow(@x: 0; @y: 0; @blur: 1px; @color: #000) {
  -webkit-box-shadow: @arguments;
     -moz-box-shadow: @arguments;
          box-shadow: @arguments;
}
.big-block {
  .box-shadow(2px; 5px);
}
```

Which results in:

结果为：

```css
.big-block {
  -webkit-box-shadow: 2px 5px 1px #000;
     -moz-box-shadow: 2px 5px 1px #000;
          box-shadow: 2px 5px 1px #000;
}
```

### 4. 高级参数 和 `@rest` 变量

You can use `...` if you want your mixin to take a variable number of arguments. Using this after a variable name will assign those arguments to the variable.

如果想传递可变参数可以使用 `...`。将它放在一个变量名称的后面来指定这个变量接收的参数是可变的。

```less
.mixin(...) {        // matches 0-N arguments
.mixin() {           // matches exactly 0 arguments
.mixin(@a: 1) {      // matches 0-1 arguments
.mixin(@a: 1; ...) { // matches 0-N arguments
.mixin(@a; ...) {    // matches 1-N arguments
```

Furthermore:

另外：

```less
.mixin(@a; @rest...) {
   // @rest is bound to arguments after @a
   // @arguments is bound to all arguments
}
```

## 5. 模式匹配

Sometimes, you may want to change the behavior of a mixin, based on the parameters you pass to it. Let's start with something basic:

有时候你想通过传递不同的参数来改变混合的行为。让我们从最基本的开始：

```less
.mixin(@s; @color) { ... }

.class {
  .mixin(@switch; #888);
}
```

Now let's say we want `.mixin` to behave differently, based on the value of `@switch`, we could define `.mixin` as such:

现在我们想通过 `@switch` 的值来使得 `.mixin` 有不同的行为，我们可以像下面一样定义 `.mixin`：

```less
.mixin(dark; @color) {
  color: darken(@color, 10%);
}
.mixin(light; @color) {
  color: lighten(@color, 10%);
}
.mixin(@_; @color) {
  display: block;
}
```

Now, if we run:

当我们调用的时候：

```less
@switch: light;

.class {
  .mixin(@switch; #888);
}
```

We will get the following CSS:

我们将得到下面的 CSS ：

```css
.class {
  color: #a2a2a2;
  display: block;
}
```

Where the color passed to `.mixin` was lightened. If the value of `@switch` was `dark`,
the result would be a darker color.

上面的结果是颜色值传递给 `.mixin` 的是等到一个更浅的颜色。如果 `@switch` 的值是 `dark` 的话，那么得到的是一个更深的颜色。

Here's what happened:

* The first mixin definition didn't match because it expected `dark` as the first argument.
* The second mixin definition matched, because it expected `light`.
* The third mixin definition matched because it expected any value.

代码分析如下：

* 第一个混合没有被匹配是因为它接收的第一个参数必须是 `dark`。
* 第二个混合被匹配是因为它接收的第一个参数是 `light`。
* 第三个混合能被匹配是因为它接收任意值。

Only mixin definitions which matched were used. Variables match and bind to any value.
Anything other than a variable matches only with a value equal to itself.

只有匹配的混合（mixin）会被使用。变量必须绑定任意值。
除变量外，其他只有与它本身相等才能被匹配。

We can also match on arity, here's an example:

我们可以在数量上进行匹配，例如下面的例子：

```less
.mixin(@a) {
  color: @a;
}
.mixin(@a; @b) {
  color: fade(@a; @b);
}
```

Now if we call `.mixin` with a single argument, we will get the output of the first definition,
but if we call it with *two* arguments, we will get the second definition, namely `@a` faded to `@b`.

当我们使用一个参数调用 `.mixin`，我们将输出第一个定义的结果，但是当我们使用 *两个* 参数进行调用，我们将使用第二个定义，即从`@a` 渐变到 `@b`。