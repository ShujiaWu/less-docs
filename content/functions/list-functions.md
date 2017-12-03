### length

> Returns the number of elements in a value list.

> 返回列表中元素的个数。

参数： `list` - 由逗号或空格分隔的值列表.

返回： 列表中元素的数量

例子： `length(1px solid #0080ff);`

输出： `3`

例子：

```less
@list: "banana", "tomato", "potato", "peach";
n: length(@list);
```

输出：

```
n: 4;
```

### extract

> Returns the value at a specified position in a list.

> 返回列表中指定位置的值。

参数：
`list` - 由逗号或空格分隔的值列表。
`index` - 一个整数，用于指定元素列表中需要返回的元素的位置。
返回： 列表中指定位置的元素。

例子： `extract(8px dotted red, 2);`
输出： `dotted`

例子：

```less
@list: apple, pear, coconut, orange;
value: extract(@list, 3);
```

输出：

```
value: coconut;
```
