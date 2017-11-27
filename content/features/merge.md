> Combine properties

> 组合属性

The `merge` feature allows for aggregating values from multiple properties into a comma or space separated list under a single property. `merge` is useful for properties such as background and transform.

`merge` 特性允许你在单个属性下将多个属性的值聚合成逗号或者分号隔开的列表。`merge` 对于  background 和 transform 属性特别有用。

### 1. 逗号

> Append property value with comma

> 使用逗号添加属性

Released [v1.5.0]({{ less.master.url }}CHANGELOG.md)

Example:

例如：

```less
.mixin() {
  box-shadow+: inset 0 0 10px #555;
}
.myclass {
  .mixin();
  box-shadow+: 0 0 20px black;
}
```

Outputs

输出：

```css
.myclass {
  box-shadow: inset 0 0 10px #555, 0 0 20px black;
}
```

### 2. 空格

> Append property value with space

> 使用空格添加属性

Released [v1.7.0]({{ less.master.url }}CHANGELOG.md)

Example:

例如：

```less
.mixin() {
  transform+_: scale(2);
}
.myclass {
  .mixin();
  transform+_: rotate(15deg);
}
```

Outputs

输出：

```css
.myclass {
  transform: scale(2) rotate(15deg);
}
```

To avoid any unintentional joins, `merge` requires an explicit `+` or `+_` flag on each join pending declaration.

为了避免任何意外的加入，`merge` 需要在没有个要添加的声明中有一个明确的 `+` 或 `+_` 标记。