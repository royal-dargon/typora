### go web 编程

#### go 基础

##### go 语言基础

###### 字符串

* 在`go`中字符串是不可变化的

```go
var s string = "hello"
s[0] = 'c'
```

这种写法是会报错的

如果想要修改可以变为如下的写法

```go
s := "hello"
c := []byte(s)
c[0] = 'c'
s2 := string(c)
```

* `go`是支持字符串连接的，就是`+`操作

###### go语言设计的一些规则

* 大写字母开头是可以导出的，但是小写字母开头的单词是无法导出的，属于是私有变量

###### 数组

```go
var name []type
```

就是这样来定义一个数组

###### slice

数组无法满足很多应用场景的需要，于是就有了`slice`，也就是动态数组。`slice`并不是真正意义上的动态数组，是一个引用类型。

```go
var a []int
a = ar[2:5]
// 值得注意的是a不包含ar[5]
```

`slice` 有一些小技巧

* `slice` 的默认开始位置是0，`ar[:n] ` 等价与 `ar[0:n]`
* `slice` 的第二个序列默认是数组的长度，`ar[n:]` 等价于 `ar[n:len(ar)]`
* 如果从一个数组里面直接获取 `slice`，可以这样` ar[:]`，因为默认第一个序列是 0，第二个是数组的长度，即等价于 `ar[0:len(ar)]`

对于 `slice` 有几个内置函数

*   `len` 获取 `slice` 的长度
*  `cap` 获取 `slice` 的最大容量
* `append1` 向 `slice` 里面追加一个或者多个元素，然后返回一个和 `slice` 一样类型的 `slice`
* `copy` 函数 `copy` 从源 `slice` 的 `src` 中复制元素到目标 `dst`，并且返回复制的元素的个数

###### map

`map` 就是字典 格式是 `map[keyType]valueType`

```go
// 初始化一个字典
rating := map[string]float32{"c":5,"c++":2}
```

值得注意的是`map`也是和引用类型的

##### 流程控制

###### if

* `go` 里面的 `if` 不需要括号

###### for

```go
for sum < 100 {}
```

以上就是我们熟悉的`while`

###### case

* `go` 的 `case` 和 `c`的还是有些的区别的，就是匹配成功后会跳出整个`switch` ，当然也是可以用`fallthrough` 来强制执行下面的内容的。

