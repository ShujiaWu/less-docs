> Conditional mixins

> 带条件的混合（mixins）

Guards are useful when you want to match on _expressions_, as opposed to simple values or arity. If you are familiar with functional programming, you have probably encountered them already.

当你想使用_表达式_匹配时,相对于简单的值或特性，守卫是非常有用的。如果你熟悉函数化编程，你可能早已经遇到过。

In trying to stay as close as possible to the declarative nature of CSS, Less has opted to implement conditional execution via **guarded mixins** instead of `if`/`else` statements, in the vein of `@media` query feature specifications.

为了尽可能地近似 CSS 的原生声明， Less 以 `@media` 媒体查询规范，选择通过 **被守卫的混合** 实现条件执行，代替 `if`/`else` 语句。

Let's start with an example:

```less
.mixin (@a) when (lightness(@a) >= 50%) {
  background-color: black;
}
.mixin (@a) when (lightness(@a) < 50%) {
  background-color: white;
}
.mixin (@a) {
  color: @a;
}
```

The key is the `when` keyword, which introduces a guard sequence (here with only one guard). Now if we run the following code:

`when` 是作为守卫语句开始的关键字（上面是只有一个守卫的情况）。如果我们运行下面的代码：

```less
.class1 { .mixin(#ddd) }
.class2 { .mixin(#555) }
```

Here's what we'll get:

我们将得到：

```css
.class1 {
  background-color: black;
  color: #ddd;
}
.class2 {
  background-color: white;
  color: #555;
}
```

### 1. 守卫中的比较运算符

The full list of comparison operators usable in guards are: `>`, `>=`, `=`, `=<`, `<`. Additionally, the keyword `true` is the only truthy value, making these two mixins equivalent:

守卫中可以使用的比较运算符清单：`>`, `>=`, `=`, `=<`, `<`。另外关键字 `true` 是唯一的真值，下面这两种混合等效：

```less
.truth (@a) when (@a) { ... }
.truth (@a) when (@a = true) { ... }
```

Any value other than the keyword `true` is falsy:

任何不等于 `true` 的值都是假的：

```less
.class {
  .truth(40); // Will not match any of the above definitions.
}
```

Note that you can also compare arguments with each other, or with non-arguments:

注意，你还可以将参数相互比较，或者使用非参数进行比较。

```less
@media: mobile;

.mixin (@a) when (@media = mobile) { ... }
.mixin (@a) when (@media = desktop) { ... }

.max (@a; @b) when (@a > @b) { width: @a }
.max (@a; @b) when (@a < @b) { width: @b }
```

### 2. 守卫中的逻辑运算符

You can use logical operators with guards. The syntax is based on CSS media queries.

你可以在守卫中使用逻辑运算符，这些符号是基于 CSS 的媒体查询的。

Use the `and` keyword to combine guards:

使用 `and` 关键字组合守卫：

```less
.mixin (@a) when (isnumber(@a)) and (@a > 0) { ... }
```

You can emulate the *or* operator by separating guards with a comma `,`. If any of the guards evaluate to true, it's considered a match:

你可以通过使用逗号`,`分隔守卫来模拟 *or* 运算符。只要任意一个守卫的值为 true ，则认为是匹配的：

```less
.mixin (@a) when (@a > 10), (@a < -10) { ... }
```

Use the `not` keyword to negate conditions:

使用 `not` 关键字来取反：

```less
.mixin (@b) when not (@b > 0) { ... }
```

### 3. 类型检查函数

Lastly, if you want to match mixins based on value type, you can use the `is` functions:

最后，如果你想在值的上匹配混合，你可以使用 `is` 函数：

```less
.mixin (@a; @b: 0) when (isnumber(@b)) { ... }
.mixin (@a; @b: black) when (iscolor(@b)) { ... }
```

Here are the basic type checking functions:

下面是基于类型检查的函数：

* `iscolor`
* `isnumber`
* `isstring`
* `iskeyword`
* `isurl`

If you want to check if a value is in a specific unit in addition to being a number, you may use one of:

如果你想检查一个带数字的值是否使用了指定的单位，你可以使用下面的函数：

* `ispixel`
* `ispercentage`
* `isem`
* `isunit`

### 4. 条件混合

_(**FIXME**)_ Additionally, the `default` function may be used to make a mixin match depending on other mixing matches, and you may use it to create "conditional mixins" similar to `else` or `default` statements (of `if` and `case` structures respectively):

_(**FIXME**)_ 另外，`default` 函数常用在匹配其他情况的混合，你可以像使用 `else` 或者 `default` 表达式（`if` and `case` 结构）一样创建“条件混合”：

```less
.mixin (@a) when (@a > 0) { ...  }
.mixin (@a) when (default()) { ... } // matches only if first mixin does not, i.e. when @a <= 0
```
