> Referencing parent selectors with `&`

> 使用 `&` 引用符选择器

The `&` operator represents the parent selectors of a [nested rule](#features-overview-feature-nested-rules) and is most commonly used when applying a modifying class or pseudo-class to an existing selector:

`&` 操作符在[嵌套的样式](#features-overview-feature-nested-rules)中代表父选择器,它经常应用在将修改的类或者伪类应用到一个已经存在的选择器上。

```less
a {
  color: blue;
  &:hover {
    color: green;
  }
}
```

results in:

结果为：

```css
a {
  color: blue;
}

a:hover {
  color: green;
}
```

Notice that without the `&`, the above example would result in `a :hover` rule (a descendant selector that matches hovered elements inside of `<a>` tags) and this is not what we typically would want with the nested `:hover`.

注意：在规则中如果没有使用 `&`，那么上面的例子的结果将会是 `a :hover`（一个 `<a>` 标签后代匹配鼠标悬停的选择器），这不是我们想要的典型的嵌套`:hover`。

The "parent selectors" operator has a variety of uses. Basically any time you need the selectors of the nested rules to be combined in other ways than the default. For example another typical use of the `&` is to produce repetitive class names:

“父选择器”操作符是其中的一种使用。基本上，任何时候你都需要将嵌套规则的选择器与默认的其他方式组合在一起。例如， `&` 的另外一种典型的用法是产生重复的类名：

```less
.button {
  &-ok {
    background-image: url("ok.png");
  }
  &-cancel {
    background-image: url("cancel.png");
  }

  &-custom {
    background-image: url("custom.png");
  }
}
```

output:

输出：

```css
.button-ok {
  background-image: url("ok.png");
}
.button-cancel {
  background-image: url("cancel.png");
}
.button-custom {
  background-image: url("custom.png");
}
```

### 1. 使用多个 `&`

`&` may appear more than once within a selector. This makes it possible to repeatedly refer to a parent selector without repeating its name.

`&` 可能在一个选择器内部出现多次。这使得他可以重复地引用父选择器而不重复它的名称。

```less
.link {
  & + & {
    color: red;
  }

  & & {
    color: green;
  }

  && {
    color: blue;
  }

  &, &ish {
    color: cyan;
  }
}
```

will output:

输出：

```css
.link + .link {
  color: red;
}
.link .link {
  color: green;
}
.link.link {
  color: blue;
}
.link, .linkish {
  color: cyan;
}
```

Note that `&` represents all parent selectors (not just the nearest ancestor) so the following example:

注意，`&` 代表的是多有的父选择器（而不只是最近的祖先），看一下下面的例子：

```less
.grand {
  .parent {
    & > & {
      color: red;
    }

    & & {
      color: green;
    }

    && {
      color: blue;
    }

    &, &ish {
      color: cyan;
    }
  }
}
```

results in:

结果是：

```css
.grand .parent > .grand .parent {
  color: red;
}
.grand .parent .grand .parent {
  color: green;
}
.grand .parent.grand .parent {
  color: blue;
}
.grand .parent,
.grand .parentish {
  color: cyan;
}
```

### 2. 改变选择器的排序

It can be useful to prepend a selector to the inherited (parent) selectors.  This can be done by putting the `&` after current selector.
For example, when using Modernizr, you might want to specify different rules based on supported features:

在继承（父）选择器前附加选择器是非常有用的。这可以通过将 `&` 放置于当前选择器之后。
例如当使用现代化浏览器，你想根据浏览器的特性指定不用的规则：

```less
.header {
  .menu {
    border-radius: 5px;
    .no-borderradius & {
      background-image: url('images/button-background.png');
    }
  }
}
```

The selector `.no-borderradius &` will prepend `.no-borderradius` to its parent `.header .menu` to form the`.no-borderradius .header .menu` on output:

选择器 `.no-borderradius &` 会将 `.no-borderradius` 放置于它的父选择器 `.header .menu` 之前，形成输出结果 `.no-borderradius .header .menu`：

```css
.header .menu {
  border-radius: 5px;
}
.no-borderradius .header .menu {
  background-image: url('images/button-background.png');
}
```

### 3. 组合展开

`&` can also be used to generate every possible permutation of selectors in a comma separated list:

`&` 可以用于在使用逗号分隔的列表中生成每一种可能的选择器组合：

```less
p, a, ul, li {
  border-top: 2px dotted #366;
  & + & {
    border-top: 0;
  }
}
```

This expands to all possible (16) combinations of the specified elements:

这将使用指定的元素扩展成所有（16种）的组合：

```css
p,
a,
ul,
li {
  border-top: 2px dotted #366;
}
p + p,
p + a,
p + ul,
p + li,
a + p,
a + a,
a + ul,
a + li,
ul + p,
ul + a,
ul + ul,
ul + li,
li + p,
li + a,
li + ul,
li + li {
  border-top: 0;
}
```
