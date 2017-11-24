> "mix-in" properties from existing styles

> 将属性与存在的样式进行“混合”

You can mix-in class selectors and id selectors, e.g.

你可以混合类选择器和id选择器，例如：

```less
.a, #b {
  color: red;
}
.mixin-class {
  .a();
}
.mixin-id {
  #b();
}
```

which results in:

结果为：

```css
.a, #b {
  color: red;
}
.mixin-class {
  color: red;
}
.mixin-id {
  color: red;
}
```

Notice that when you call the mixin, the parentheses are optional.

注意：当你使用混合（mixin）的时候，括号是可选的。

```less
// these two statements do the same thing:
.a(); 
.a;
```

## 1. 不在结果中输出混合

If you want to create a mixin but you do not want that mixin to be output, you can put parentheses after it.

如果你想创建不被输出的混合（mixin），那么你可以在混合（mixin）后面添加括号：

```less
.my-mixin {
  color: black;
}
.my-other-mixin() {
  background: white;
}
.class {
  .my-mixin;
  .my-other-mixin;
}
```

outputs

输出：

```css
.my-mixin {
  color: black;
}
.class {
  color: black;
  background: white;
}
```

## 2. 混合中的选择器

Mixins can contain more than just properties, they can contain selectors too.

混合（mixins）不仅能包含样式属性，还可以包含选择器。

For example:

例如：

```less
.my-hover-mixin() {
  &:hover {
    border: 1px solid red;
  }
}
button {
  .my-hover-mixin();
}
```

Outputs

输出：

```css
button:hover {
  border: 1px solid red;
}
```

## 3. 命名空间

If you want to mixin properties inside a more complicated selector, you can stack up multiple id's or classes.

如果你想使用一个复杂选择器中的混合（mixin），你可以通过堆叠多个id或类选择器来实现。

```less
#outer {
  .inner {
    color: red;
  }
}

.c {
  #outer > .inner;
}
```

and again both `>` and whitespace are optional

再次说明：`>` 和空格是可选的。

```less
// all do the same thing
#outer > .inner;
#outer > .inner();
#outer .inner;
#outer .inner();
#outer.inner;
#outer.inner();
```

One use of this is known as namespacing. You can put your mixins under a id selector and this makes sure it won't conflict with another library.

这种用法被称为命名空间。你可以将你的混合（mixins）放在一个id选择器下以保证不会跟其他的样式库发生冲突。

Example:

例如：

```less
#my-library {
  .my-mixin() {
    color: black;
  }
}
// which can be used like this
.class {
  #my-library > .my-mixin();
}
```

## 4. 命名空间守卫

If namespace have a guard, mixins defined by it are used only if guard condition returns true. Namespace guard is evaluated exactly the same way as guard on mixin, so next two mixins work the same way:

如果命名空间有守卫，在命名空间下定义的混合（mixins）只有当守卫的表达式为 true 的时候才能被使用。命名空间守卫和混合守卫是一样的，所以下面两段代码的工作方式是一样的：

```less
#namespace when (@mode=huge) {
  .mixin() { /* */ }
}

#namespace {
  .mixin() when (@mode=huge) { /* */ }
}
```

The `default` function is assumed to have the same value for all nested namespaces and mixin. Following mixin is never evaluated, one of its guards is guaranteed to be false:

`default` 函数的作用是假定所有的嵌套命名空间和混合（mixin）都有相同的值。下面的混合将永远不会被计算的，他的有一个守卫永远是 false ：

```less
#sp_1 when (default()) {
  #sp_2 when (default()) {
    .mixin() when not(default()) { /* */ }
  }
}
```

## 5. `!important` 关键字

Use the `!important` keyword after mixin call to mark all properties inherited by it as `!important`:

在混合（mixin）后面使用关键字 `!important` ， 混合后的属性都将被标记为 `!important`：

Example:

例如：

```less
.foo (@bg: #f5f5f5, @color: #900) {
  background: @bg;
  color: @color;
}
.unimportant {
  .foo();
}
.important {
  .foo() !important;
}
```

Results in:

结果为：

```css
.unimportant {
  background: #f5f5f5;
  color: #900;
}
.important {
  background: #f5f5f5 !important;
  color: #900 !important;
}
```
