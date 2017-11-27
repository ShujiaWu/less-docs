> Creating loops

> 创建循环

In Less a mixin can call itself. Such recursive mixins, when combined with [Guard Expressions](#mixin-guards-feature) and [Pattern Matching](#mixins-parametric-feature-pattern-matching), can be used to create various iterative/loop structures.

在 Less 中，混合可以调用自身。这样结合了 [守卫表达式](#mixin-guards-feature) 和 [模式匹配](#mixins-parametric-feature-pattern-matching)的递归混合，能够用于创建各种迭代/循环结构。

Example:

例如：

```less
.loop(@counter) when (@counter > 0) {
  .loop((@counter - 1));    // next iteration
  width: (10px * @counter); // code for each iteration
}

div {
  .loop(5); // launch the loop
}
```

Output:

输出：

```css
div {
  width: 10px;
  width: 20px;
  width: 30px;
  width: 40px;
  width: 50px;
}
```

A generic example of using a recursive loop to generate CSS grid classes:

一种比较常见的应用是使用递归循环产生CSS网格布局：

```less
.generate-columns(4);

.generate-columns(@n, @i: 1) when (@i =< @n) {
  .column-@{i} {
    width: (@i * 100% / @n);
  }
  .generate-columns(@n, (@i + 1));
}
```

Output:

输出：

```css
.column-1 {
  width: 25%;
}
.column-2 {
  width: 50%;
}
.column-3 {
  width: 75%;
}
.column-4 {
  width: 100%;
}
```
