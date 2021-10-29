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

##### 面向对象

###### method

* `go` 里面的面向对象可以通过 `method` 来实现

```go

package main

import (
    "fmt"
    "math"
)

type Rectangle struct {
    width, height float64
}

type Circle struct {
    radius float64
}

func (r Rectangle) area() float64 {
    return r.width*r.height
}

func (c Circle) area() float64 {
    return c.radius * c.radius * math.Pi
}

func main() {
    r1 := Rectangle{12, 2}
    r2 := Rectangle{9, 4}
    c1 := Circle{10}
    c2 := Circle{25}

    fmt.Println("Area of r1 is: ", r1.area())
    fmt.Println("Area of r2 is: ", r2.area())
    fmt.Println("Area of c1 is: ", c1.area())
    fmt.Println("Area of c2 is: ", c2.area())
}
```

##### web 基础

###### web 工作方式

* 输入的 `url` 会通过 `DNS` 服务进行解析获取	域名相对应的`Ip`

###### `http` 的请求包

* 请求包分为3部分，第一部分叫请求行，第二部分叫请求头，第三部分是主体。`header` 和 `body` 之间有个空行

###### GO 搭建一个web服务器

###### Go 如何使得web进行工作

* 服务端有处理请求，进行相应，连接和处理器的几个概念

###### `http` 包的详解

* `servemux`   (多路复用器) 的自定义

  ```go
  
  type ServeMux struct {
      mu sync.RWMutex   // 锁，由于请求涉及到并发处理，因此这里需要一个锁机制
      m  map[string]muxEntry  // 路由规则，一个 string 对应一个 mux 实体，这里的 string 就是注册的路由表达式
      hosts bool // 是否在任意的规则中带有 host 信息
  }
  ```



##### 表单

* handler 里面有一种方法可以自动解析form

  ```go
  r.ParseForm() 
  ```

#### 数据库

##### `database/sql` 接口

###### `sql.Register` 

这个是用来注册数据库的驱动的，是实现在 `init` 函数里的。

```go
Register(name string, driver driver,Driver)
```

同时，`database/sql` 在内部通过一个`map` 来存储用户定义的相应驱动。因此是可以注册多个驱动的

###### `driver.Driver`

`Driver` 是一个数据库驱动的接口，定义了一个`method： Open (name string)` 返回的是一个数据库的连接

###### `driver.Conn` 

`Conn` 是一个数据库连接的接口定义，定义了一系列的方法，这个`Conn` 只能应用在一个`go` 协程中。

```go
// Prepare主要是返回与当前连接相关的执行Sql语句的准备状态，可以进行查询，删除等操作
// Close 是关闭，释放连接资源
// Begin 是返回一个代表事物处理的Tx？？？
type Conn interface {
    Prepare(query string) (Stmt, error)
    Close() error
    Begin() (Tx, error)
}
```

###### diver.Stmt

`Stmt` 是一种准备好的状态

```go
type Stmt interface {
    Close() error
    NumInput() int
    Exec(args []Value) (Result, error)
    Query(args []Value) (Rows, error)
}
```

###### driver.Tx

事物处理，递交或者回滚