> Return variables or mixins from mixins

> 混合返回变量或者混合

Variables and mixins defined in a mixin are visible and can be used in caller's scope. There is only one exception, a variable is not copied if the caller contains a variable with the same name (that includes variables defined by another mixin call).  Only variables present in callers local scope are protected. Variables inherited from parent scopes are overridden.

变量和混合（mixins）可以定义在混合（mixin）中，并且在调用者作用域中是可见的、可被访问的。但是有一点是例外的，当调用的作用域中有同名的变量，则混合（mixin）中的变量是不会被复制的（同样包括定义在其他被调用的混合的变量）。

Example:

例如：

```less
.mixin() {
  @width:  100%;
  @height: 200px;
}

.caller {
  .mixin();
  width:  @width;
  height: @height;
}

```

Results in:

结果为：

```css
.caller {
  width:  100%;
  height: 200px;
}
```

Thus variables defined in a mixin can act as its return values. This allows us to create a mixin that can be used almost like a function.

因此，变量定义在混合（mixin）中能够作为混合（mixin）的返回值。这允许我们创建类似函数的混合（mixin）。

Example:

```less
.average(@x, @y) {
  @average: ((@x + @y) / 2);
}

div {
  .average(16px, 50px); // "call" the mixin
  padding: @average;    // use its "return" value
}
```

Results in:

结果为：

```css
div {
  padding: 33px;
}
```

Variables defined directly in callers scope cannot be overridden. However, variables defined in callers parent scope is not protected and will be
overridden:

变量直接定义在调用者的作用域将不会被重写。但是定义在父作用域中的变量将不会受到保护，会被重写：

````less
.mixin() {
  @size: in-mixin;
  @definedOnlyInMixin: in-mixin;
}

.class {
  margin: @size @definedOnlyInMixin;
  .mixin();
}

@size: globaly-defined-value; // callers parent scope - no protection
````

Results in:

结果为：

````css
.class {
  margin: in-mixin in-mixin;
}
````

Finally, mixin defined in mixin acts as return value too:

最后，混合（mixin）定义在混合中也是作为返回值：

````less
.unlock(@value) { // outer mixin
  .doSomething() { // nested mixin
    declaration: @value;
  }
}

#namespace {
  .unlock(5); // unlock doSomething mixin
  .doSomething(); //nested mixin was copied here and is usable
}
````

Results in:

结果为：

````css
#namespace {
  declaration: 5;
}
````
