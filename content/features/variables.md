---
title: 变量
---

> Control commonly used values in a single location.

> 将常用的值定义在一个地方。

### 1. 预览

It's not uncommon to see the same value repeated dozens _if not hundreds of times_ across your stylesheets:

我们经常在样式表中见到同样的样式值出现多次（甚至出现上百次）。

```css
a,
.link {
  color: #428bca;
}
.widget {
  color: #fff;
  background: #428bca;
}
```

Variables make your code easier to maintain by giving you a way to control those values from a single location:

变量在统一的地方进行管理，使得代码更加容易管理。

```less
// Variables
@link-color:        #428bca; // sea blue
@link-color-hover:  darken(@link-color, 10%);

// Usage
a,
.link {
  color: @link-color;
}
a:hover {
  color: @link-color-hover;
}
.widget {
  color: #fff;
  background: @link-color;
}
```

### 2. 变量插值

The examples above focused on using variables to control _values in CSS rules_, but they can also be used in other places as well, such as selector names, property names, URLs and `@import` statements.

上面的例子着重于使用变量控制 CSS 样式规则中的值，变量也可以很好地应用于其他地方，例如：选择器的名称、属性名称、URL、`@import`表达式。

### 3. 用于选择器名

Version: 1.4.0

```less
// Variables
@my-selector: banner;

// Usage
.@{my-selector} {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

编译后:

```css
.banner {
  font-weight: bold;
  line-height: 40px;
  margin: 0 auto;
}
```

### 4. 用于 URL 地址

```less
// Variables
@images: "../img";

// Usage
body {
  color: #444;
  background: url("@{images}/white-sand.png");
}
```

### 5. 用于Import 表达式

Version: 1.4.0

语法: `@import "@{themes}/tidal-wave.less";`

Note that before v2.0.0, only variables which have been declared in the root or current scope were considered and that only the current file and calling files were considered when looking for a variable.

注意：在 v2.0.0 之前只考虑在根或当前作用域声明的变量，所以当在查找变量的时候只考虑当前文件和调用文件查找。

例如:

```less
// Variables
@themes: "../../src/themes";

// Usage
@import "@{themes}/tidal-wave.less";
```

### 6. 用于属性

Version: 1.6.0

```less
@property: color;

.widget {
  @{property}: #0ee;
  background-@{property}: #999;
}
```

编译后:

```css
.widget {
  color: #0ee;
  background-color: #999;
}
```

### 7. 作为变量的名字

It is also possible to define variables with a variable name:

变量也可能用于定义一个变量的名字：

```less
@fnord:  "I am fnord.";
@var:    "fnord";
content: @@var;
```

编译后:

```
content: "I am fnord.";
```

<span class="anchor-target" id="variables-feature-lazy-loading"></span>
<!-- ^ please keep old anchor to not break zillion outer links -->
### 8. 延后计算（Lazy Evaluation）

> Variables are lazy evaluated and do not have to be declared before being used.

> 变量是延后计算（Lazy Evaluation）的，所以不用强制在使用它之前声明。

Valid Less snippet:

下面的代码片段是合法的：

```less
.lazy-eval {
  width: @var;
}

@var: @a;
@a: 9%;
```

this is valid Less too:

下面的代码也是合法的：

```less
.lazy-eval {
  width: @var;
  @a: 9%;
}

@var: @a;
@a: 100%;
```

他们都编译成:

```css
.lazy-eval {
  width: 9%;
}
```

When defining a variable twice, the last definition of the variable is used, searching from the current scope upwards. This is similar to CSS itself where the last property inside a definition is used to determine the value.

当一个变量被定义两次时，由于变量的查找是从当前的作用域往上查找的，最后定义的变量将会被使用。这类似于 CSS 本身的语法，定义的最后一个属性值将被使用。

例子:

```less
@var: 0;
.class {
  @var: 1;
  .brass {
    @var: 2;
    three: @var;
    @var: 3;
  }
  one: @var;
}
```

编译后:

```css
.class {
  one: 1;
}
.class .brass {
  three: 3;
}
```

### 8. 变量的默认值

We sometimes get requests for default variables - an ability to set a variable only if it is not already set. This feature is not required because you can easily override a variable by putting the definition afterwards.

有时候我们想要获得一个变量的默认值（当一个变量没有被设置的时候，才会去设置变量）。这种特性不是必须的，因为我们很容易重新定义来覆盖这个变量。

例如:

```less
// library
@base-color: green;
@dark-color: darken(@base-color, 10%);

// use of library
@import "library.less";
@base-color: red;
```

This works fine because of [Lazy Loading](#variables-feature-lazy-loading) - base-color is overridden and dark-color is a dark red.

因为 [Lazy Loading](#variables-feature-lazy-loading)，使得以上代码满足我们的需求。 base-color 被覆盖，dark-color 的值为 深红色
