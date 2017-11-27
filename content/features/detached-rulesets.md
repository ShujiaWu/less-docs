> Allow wrapping of a css block, defined in a mixin

> 在混合（mixin）中定义封装的 CSS 块

Released [v1.7.0]({{ less.master.url }}CHANGELOG.md)

A detached ruleset is a group of css properties, nested rulesets, media declarations or anything else stored in a variable. You can include it into a ruleset or another structure and all its properties are going to be copied there. You can also use it as a mixin argument and pass it around as any other variable.

分离的样式集是指任意可以存储于变量中的一组 CSS 样式、嵌套样式集、媒体声明等。你可以把他们包含进一组样式集或者其他结构中，其中所有的样式将会被复制。你甚至可以把它当做混合（mixin）的参数，把它传递个其他变量。

Simple example:

一些例子：

````less
// declare detached ruleset
@detached-ruleset: { background: red; };

// use detached ruleset
.top {
    @detached-ruleset();
}
````

compiles into:

编译后：

````css
.top {
  background: red;
}
````

Parentheses after a detached ruleset call are mandatory. The call `@detached-ruleset;` would NOT work.

括号在分离样式集的调用中是强制的，如果只调用 `@detached-ruleset;` 将不会生效。

It is useful when you want to define a mixin that abstracts out either wrapping a piece of code in a media query or a non-supported browser class name. The rulesets can be passed to mixin so that the mixin can wrap the content, e.g.

当你想定义抽象出包装媒体查询或者不支持的浏览器类名代码的混合（mixin）时，这非常有用。规则集可以被传递给混合（mixin），混合（mixin）可以对内容进行包装。

```less
.desktop-and-old-ie(@rules) {
  @media screen and (min-width: 1200px) { @rules(); }
  html.lt-ie9 &                         { @rules(); }
}

header {
  background-color: blue;

  .desktop-and-old-ie({
    background-color: red;
  });
}
```

Here the `desktop-and-old-ie` mixin defines the media query and root class so that you can use a mixin to wrap a piece of code. This will output

上面的混合 `desktop-and-old-ie` 定义了媒体查询和根类，你可以使用混合来包装任何一段代码。这将输出：

```css
header {
  background-color: blue;
}
@media screen and (min-width: 1200px) {
  header {
    background-color: red;
  }
}
html.lt-ie9 header {
  background-color: red;
}
```

A ruleset can be now assigned to a variable or passed in to a mixin and can contain the full set of Less features, e.g.

一个包含所有 Less 特性的规则集可以被分配给一个变量或者作为参数传递给一个混合（mixin）。

```less
@my-ruleset: {
    .my-selector {
      background-color: black;
    }
  };
```

You can even take advantage of [media query bubbling](#features-overview-feature-media-query-bubbling-and-nested-media-queries), for instance

你甚至可以利用[媒体查询冒泡](#features-overview-feature-media-query-bubbling-and-nested-media-queries),例如：

```less
@my-ruleset: {
    .my-selector {
      @media tv {
        background-color: black;
      }
    }
  };
@media (orientation:portrait) {
    @my-ruleset();
}
```

which will output

输出：

```css
@media (orientation: portrait) and tv {
  .my-selector {
    background-color: black;
  }
}
```

A detached ruleset call unlocks (returns) all its mixins into caller the same way as mixin calls do. However, it does NOT return variables.

分离的样式调用跟混合（mixin）调用一样返回所有混合内容。但是不同的是，它不返回变量。

Returned mixin:

返回的混合（mixin）：

````less
// detached ruleset with a mixin
@detached-ruleset: {
    .mixin() {
        color:blue;
    }
};
// call detached ruleset
.caller {
    @detached-ruleset();
    .mixin();
}
````

Results in:

结果：

````css
.caller {
  color: blue;
}
````

Private variables:

私有变量：

````less
@detached-ruleset: {
    @color:blue; // this variable is private
};
.caller {
    color: @color; // syntax error
}
````

## 1. 作用域
A detached ruleset can use all variables and mixins accessible where it is *defined* and where it is *called*. Otherwise said, both definition and caller scopes are available to it. If both scopes contains the same variable or mixin, declaration scope value takes precedence. 

分离的规则器可以使用*定义*它的作用域和调用它的作用域中的变量。换句话说就是它可以访问定义它和调用它的作用域。如果两个作用域都包含相同的变量或者混合（mixin），优先使用声明它的作用中的。

*Declaration scope* is the one where detached ruleset body is defined. Copying a detached ruleset from one variable into another cannot modify its scope. The ruleset does not gain access to new scopes just by being referenced there.

*声明的作用域*是指定义分离的规则集的作用域。将一个分离的规则集从一个变量复制到另外一个变量不会修改它的作用域。规则集不会因被引用而获得新的访问作用域。

Lastly, a detached ruleset can gain access to scope by being unlocked (imported) into it.

最后。一个分离的规则集可以被导入的时候获得访问新的作用域。

#### 1.1 定义和调用的作用域是可以被访问的
A detached ruleset sees the caller's variables and mixins:

分离的规则集可以访问位于调用者中的变量和混合。

````less
@detached-ruleset: {
  caller-variable: @caller-variable; // variable is undefined here
  .caller-mixin(); // mixin is undefined here
};

selector {
  // use detached ruleset
  @detached-ruleset();

  // define variable and mixin needed inside the detached ruleset
  @caller-variable: value;
  .caller-mixin() {
    variable: declaration;
  }
}
````

compiles into:

编译后：

````css
selector {
  caller-variable: value;
  variable: declaration;
}
````

Variable and mixins accessible form definition win over those available in the caller:

变量和混合（mixin）的访问级别，定义中的要比调用者中的优先级更高。

````less
@variable: global;
@detached-ruleset: {
  // will use global variable, because it is accessible
  // from detached-ruleset definition
  variable: @variable; 
};

selector {
  @detached-ruleset();
  @variable: value; // variable defined in caller - will be ignored
}
````

compiles into:

编译后：

````css
selector {
  variable: global;
}
````

#### 1.2 引用*不会*修改分离样式集的作用域Referencing
A ruleset does not gain access to new scopes just by being referenced there:

规则集被引用时不会获得新的作用域：

````less
@detached-1: { scope-detached: @one @two; };
.one {
  @one: visible;
  .two {
    @detached-2: @detached-1; // copying/renaming ruleset 
    @two: visible; // ruleset can not see this variable
  }
}

.use-place {
  .one > .two(); 
  @detached-2();
}
````

throws an error:

抛出异常：

````
ERROR 1:32 The variable "@one" was not declared.
````

#### 1.3 返回*会*修改分离的作用域
A detached ruleset gains access by being unlocked (imported) inside a scope:

分离的规则集可以访问被返回（导入）的作用域：

````less
#space {
  .importer-1() {
    @detached: { scope-detached: @variable; }; // define detached ruleset
  }
}

.importer-2() {
  @variable: value; // unlocked detached ruleset CAN see this variable
  #space > .importer-1(); // unlock/import detached ruleset
}

.use-place {
  .importer-2(); // unlock/import detached ruleset second time
   @detached();
}
````

compiles into:

编译后：

````css
.use-place {
  scope-detached: value;
}
````
