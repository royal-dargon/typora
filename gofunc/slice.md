#### go语言切片深入理解

* 概念 

  切片是对数组的一个连续片段的引用，值得注意的是终止索引标识的项不包括在切片内。

* 使用make创建一个切片

  ```go
  var slice []type = make([]type, len)
  slice := make([]type, len)
  ```

  make接收两个参数，元素的类型以及切片元素的个数。当然后面还有一个可选参数，就是cap。

* new与make之间的区别