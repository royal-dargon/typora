## Go语言并发之道

### 第一章

* 竞争条件 ：但两个或多个操作必须按正确的顺序执行，而程序并未保证这个顺序，就会发生竞争条件。举个例子吧，竞争发生在a,b同时对p进行操作，最后的结果是有竞争的失败者决定。总言而之，就是会给程序带来了不确定性。
* 原子性 ：当某些东西被认为是原子的，或者具有原子性的时候，这意味着在它运行的环境中，它是不可分割的或不可中断的。当然，原子性是会环境的转变，发生转变。
* 死锁 ***deadlock*** 在我的理解里死锁就是程序中的所有并发进程进入了一个彼此互相等待的状态。它的发生需要同时满足四个条件。**排斥条件**，**请求和保持条件**，**不剥夺条件**（进程获得的资源只能由自己释放），**循环条件**。
* 活锁 就是没有发生堵塞，但是一个请求却一直处于失败失败的循环中，但是要注意活锁是可能会自己解开的。
* 饥饿 就是一个进程占用了过多的资源导致其他进程完成的效率底下，甚至无法完成。  

### 第二章  ~~这一章没有认真看~~

* 并发与并行的区别

  > 并发：同一时间段内执行多个任务（你在用你的微信和你的两个女朋友聊天）
  >
  > 并行：同一时刻执行多个任务（你和你的好兄弟都在用微信和你的女朋友聊天）

* ***CSP*** （Communicating Sequential Processes ）中文名是通信顺序进程。
* Go语言的并发哲学  ： 追求简洁，尽量使用channel，并且认为goroutine得使用是没有成本的。

### 第三章

* 每一个Go程序至少有一个goroutine。简单来说，这是一个并发的函数，添加关键字go来触发

* Go语言中的goroutine是独一无二的，它们是一个更高级别的抽象，称为协程。(轻量级线程)，不能被中断，但是有很多point，允许暂停和重新进入。

* Go语言的主机托管机制是一个名为m:n调度器实现，这意味着它将M个绿色线程（由语言运行平台进行调度）映射到N个OS线程

* Go语言遵循的是一个fork-join的并发模型，fork是一个节点，在这个节点处会将程序分叉，同时运行，join就是在某一时刻，分支和主干汇合。

* 了解“sync包”中的waitgroup add（表示几个goroutine开始），wait（阻塞main上的goroutine），done（表明已经退出）。

* 互斥锁与读写锁 ***Mutex*** 是互斥的意思，就是一种请求对临界区独占的方式，在使用完后释放互斥锁。(当一个 goroutine 获得了 Mutex 后，其他 goroutine 就只能乖乖等到这个 goroutine 释放该 Mutex。)

* sync.REMutex 在概念上是和互斥是一样的，但是它会让你对内存有了更多的控制。在读锁占用的情况下，会阻止写，但不阻止读，也就是多个 goroutine 可同时获取读锁（调用 RLock() 方法；而写锁（调用 Lock() 方法）会阻止任何其他 goroutine（无论读和写）进来，整个锁相当于由该 goroutine 独占。从 RWMutex 的实现看，RWMutex 类型其实组合了 Mutex。通常建议使用的是RWMutex。

* 池 work-pool 我的理解就是任务数多于开的goroutine的数量，用来防止泄露

* channel先声明然后初始化 

    ```go
var dataStream chan interface{}
dataStream = make(chan interface{})
    ```

​      ***其中第二行的make，最好声明一下通道的容量 ~~我试了一下，写的不好会出现死锁~~***

​      当然也是可以声明一个只允许接收或者发送的通道（通常使用在函数的参数中或者是函数的返回值中）

```go
  var dataStream <-chan interface{}
 dataStream = make(<-chan interface{})  
```
​      这是只允许读取的channelgo

```go
var dataStream chan<- interface{}
dataStream := make(chan<- interface{})
```
​      这是只允许发送到其nondeterministic中的通道类型

```go
var receiveChan <-chan interface{}
var sendChan chan<- interface{}
dataStream := make(chan interface{})
// Valid statements:
receiveChan = dataStream
sendChan = dataStream
```

<- 这个操作在返回的时候可以返回两个值

```go
stringStream := make(chan string)
go func() {
stringStream <- "Hello channels!"
}()
salutation, ok := <-stringStream
fmt.Printf("(%v): %v", ok, salutation)
```

### 第四章 

~~只看了for-select，防止泄露和错误处理~~

* for-select  循环的方式有无限循环和range循环

```go
for _, s := range []string{"a", "b", "c"} {
	select {
		case <-done:
			return
		case stringStream <- s:
	}
}
```

* 防止goroutine泄露    ~~说不明白~~
* 错误处理  ~~说不明白~~





