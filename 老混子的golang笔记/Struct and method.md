## Struct and method

### 定义

结构体定义方式：

```
type identifier struct {
    field1 type1
    field2 type2
    ...
}
```

`type T struct {a, b int}` 也是合法的语法，它更适用于简单的结构体。

```
type myStruct struct { i int }
var v myStruct    // v是结构体类型变量
var p *myStruct   // p是指向一个结构体类型变量的指针
v.i
p.i
```

**递归结构体**

结构体类型可以通过引用自身来定义。这在定义链表或二叉树的元素（通常叫节点）时特别有用，此时节点包含指向临近节点的链接（地址）。如下所示，链表中的 `su`，树中的 `ri` 和 `le` 分别是指向别的节点的指针。

链表：

[![img](https://github.com/Unknwon/the-way-to-go_ZH_CN/raw/master/eBook/images/10.1_fig10.3.jpg?raw=true)](https://github.com/Unknwon/the-way-to-go_ZH_CN/blob/master/eBook/images/10.1_fig10.3.jpg?raw=true)

这块的 `data` 字段用于存放有效数据（比如 float64），`su` 指针指向后继节点。

Go 代码：

```
type Node struct {
    data    float64
    su      *Node
}
```

链表中的第一个元素叫 `head`，它指向第二个元素；最后一个元素叫 `tail`，它没有后继元素，所以它的 `su` 为 nil 值。当然真实的链接会有很多数据节点，并且链表可以动态增长或收缩。

同样地可以定义一个双向链表，它有一个前趋节点 `pr` 和一个后继节点 `su`：

```
type Node struct {
    pr      *Node
    data    float64
    su      *Node
}
```

二叉树：

[![img](https://github.com/Unknwon/the-way-to-go_ZH_CN/raw/master/eBook/images/10.1_fig10.4.jpg?raw=true)](https://github.com/Unknwon/the-way-to-go_ZH_CN/blob/master/eBook/images/10.1_fig10.4.jpg?raw=true)

二叉树中每个节点最多能链接至两个节点：左节点（le）和右节点（ri），这两个节点本身又可以有左右节点，依次类推。树的顶层节点叫根节点（**root**），底层没有子节点的节点叫叶子节点（**leaves**），叶子节点的 `le` 和 `ri` 指针为 nil 值。在 Go 中可以如下定义二叉树：

```
type Tree strcut {
    le      *Tree
    data    float64
    ri      *Tree
}
```