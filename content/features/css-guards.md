> "if"'s around selectors

> 围绕在选择器的“条件”

Released [v1.5.0]({{ less.master.url }}CHANGELOG.md)

Guards can also be applied to css selectors, which is syntactic sugar for declaring the mixin and then calling it immediately.

守卫同样可以应用到 CSS 选择器上，这是声明混合然后立即调用的语法糖。

For instance, before 1.5.0 you would have had to do this:

例如：在1.5.0之前，你必须这样写：

```less
.my-optional-style() when (@my-option = true) {
  button {
    color: white;
  }
}
.my-optional-style();
```

Now, you can apply the guard directly to a style.

现在你可以直接在样式上应用守卫：

```less
button when (@my-option = true) {
  color: white;
}
```

You can also achieve an `if` type statement by combining this with the `&` feature, allowing you to group multiple guards.

你同样可以通过使用 `&` 的组合特性来实现 `if` 类型表达式，允许将多个守卫组合起来：

```less
& when (@my-option = true) {
  button {
    color: white;
  }
  a {
    color: blue;
  }
}
```
