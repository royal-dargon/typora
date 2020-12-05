# API接口

##### 应用程序，网站一般都是采用前后端分离的方案。我们后端写业务处理逻辑（一般是对数据的处理和存储），然后对外暴露一个接口，前端通过这个接口，向我们请求数据（GET）,或者发送数据（POST）给我们后台处理。前后端交互就是通过我们写的接口实现的。

分析工作台成员界面

理解了API是啥之后，下面我们就开始一步步尝试自己写一个简单的接口。

## 接口功能

接收不带参数的```GET```请求，返回```Hello```

  ```World!```



## 服务架构图



![](https://drek4537l1klr.cloudfront.net/chang/Figures/03fig02_alt.jpg)





我们写的接口其实就是一个个处理器(Handler)，一个处理器绑定一个URL

我们用 ```net/http``` 标准库写



## 代码实现

```go
package main

import (
	"fmt"
	"net/http"
)

func Hello(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "Hello")
}
func World(w http.ResponseWriter, r *http.Request) {
	fmt.Fprintln(w, "World")
}
func main() {
	server := http.Server{
		// 端口号要开在 1024-65535 这个范围内,如果页面进不了，可能是端口号被占用
		// 我电脑8080就被占用了
		Addr: "127.0.0.1:1024", 
        
	}
    
	http.HandleFunc("/hello", Hello)
	http.HandleFunc("/world", World)
	server.ListenAndServe()
}
```

`` go run `` 把服务跑起来之后，我们去浏览器输入网址``http://127.0.0.1:1024/hello`` 和``http://127.0.0.1:1024/world`` 就能分别看到

Hello 和 World了。



### 下面我们一步步解释：

服务架构图中的 ```Multiplexer``` 叫多路复用器，用来转接到不同的处理器函数处理客户端发来的请求。代码中

``` go
server.ListenAndServe()
```

```server``` 的 ```ListenAndServe()``` 开启一个web服务，其实可以自己指定复用器的，但是我们一般不指定，它会默认使用 ```DefaultServeMux``` 默认多路复用器. 然后我们有：

```go
	http.HandleFunc("/hello",Hello)
    http.HandleFUnc("/world",World)
```

前面讲了 Hello,World 是两个处理器函数， 然后用 ```http.HandleFunc()``` 把那两个函数转换为两个处理器， 就是服务架构图中的``Handler``  ，并且为每一个处理器绑定一个路径，我们一般叫  ```pattern``` ，这个就会在我们请求的URL体现出来了 （注意分清我说的处理器函数和处理器的区别）.  然后多路复用器就会根据请求的 URL 分析 ``pattern`` 来转接到不同的处理器 ```handler``` 做出不同的响应。



你们可能会疑惑，下面这个server干啥用的:

```go
	server:=http.Server	{
        // Addr 是服务的地址。 因为进程间通信，TCP协议规定了用“IP:port”(IP地址：端口号)来定位一个主机的特定进程。
        // IP地址定位主机，端口号定位进程（就是我们开的Web服务），这两个组合就叫套接字（Socket）。端口号有个范围
        // 1024-65535 就是协议预留给我们用户自己定义的端口号， 这里我就用了 1024
        // 127.0.0.1 是我们主机默认的的IP地址（所有主机都一样），也叫:localhost，注意这个地址是不能被其他主机访问到的，只能
        // 自己访问，所以我们现在写的Web服务在其他电脑的浏览器是访问不到的
		Addr:"127.0.0.1:1024",
	}
```

很明显它是一个结构体，我们可以看下标准库对它的描述：

```go
// A Server defines parameters for running an HTTP server. The zero value for Server is a valid configuration.
type Server struct {
    Addr           string      // 监听地址
    Handler        Handler     // 处理器：  handler to invoke, http.DefaultServeMux if nil 
    ReadTimeout    time.Duration   // 其他的想了解自己去标准库看吧，都有解释 但是我们一般不会设置它
    WriteTimeout   time.Duration
    MaxHeaderBytes int
    TLSConfig      *tls.Config
    TLSNextProto   map[string]func(*Server, *tls.Conn, Handler)
    ConnState      func(net.Conn, ConnState)
    ErrorLog       *log.Logger
}
```

可以看到，server 是用来定义一些开启HTTP服务的相关参数，如果我们不设置它，它就会用默认值

注意Server结构体里面的这个属性

```go
Handler        Handler     // 处理器：  handler to invoke, http.DefaultServeMux if nil
```

我们不是用```http.HandleFunc()```函数构造了 ``Hello`` 和 ``World`` 两个处理器吗，其实我们也可以直接对我们开的服务指定一个特定的处理器，只做特定的服务。 前面的代码我们没设置这个属性， 就默认用 ``http.DefaultServeMux`` 前面我们不是讲了这是多路复用器吗，怎么现在又是处理器了？

实际上， ``http.DefaultServeMux`` 不仅是一个多路复用器，它也是一个处理器。但是它和一般的处理器不同，这个处理器唯一要做的就是根据请求的 URL 将请求重定向到不同的处理器。 再回头看服务架构图就清楚了吧.



## Web框架问题&Postman演示

前面我们是用 ```net/http``` 标准库写的服务，但是你们有没有发现一个问题？

对于客户端发来的请求，我们没有分析它的请求方法是 ``Get`` ``Post`` 还是 ``Delete`` 啥的，也就是说，我们不能区分请求类型。我对同一个

URL（http://127.0.0.1:1024/hello） 做不同的请求（Get,Post），得到的响应永远是 ``Hello``

我们下面用Postman演示下：

Postman可以模拟浏览器发送HTTP请求，我们写接口的时候不可能再去写个网页来测试我们写的接口，所有一般用Postman测试。

演示用不同方法请求（http://127.0.0.1:1024/hello），都是得到同一个结果



也就是说，我们对网站上的同一资源不能区别的做不同类型的处理，这就很麻烦了.

其实我们要用标准库实现这个功能也可以，只是比较麻烦，然后还有其他的一些问题（比如不能在URL模式匹配中使用变量），要对URL做复杂的语法分析。那每次这样就很麻烦。所以就有人用标准库写了一个Web框架，实现了这些功能（当然肯定不止这些），我们直接调用他们框架的函数就可以了，简化了操作。  go语言比较常用的web框架就是 gin， 还有 echo（echo对新手友好）

我们可以看下用 gin 写的路由选择（这是张竣淇学长寒假写的miniproject的部分代码）：

```go
var Router *gin.Engine

func InitRouter() {
	Router= gin.Default()
	Router.GET("/api/v1/people/:user_id",hander.PeopleInfo)   
	Router.PUT("/api/v1/people/:user_id",hander.UpdatePeopleInfo)
	Router.PATCH("/api/v1/people/:user_id",hander.Follow)
	Router.GET("/api/v1/people/:user_id/albums/:album_id",hander.TheAlbum)
	Router.POST("/api/v1/people/:user_id/albums/:album_id",hander.AddReviews)
	Router.PUT("/api/v1/people/:user_id/albums/:album_id",hander.RemoveReviews)
}
```

可以看到，gin框架写的路由选择函数，实现了对同一URL不同请求方法重定向到不同的处理器。 而且还支持 URL 中出现变量`` user_id`` 

``album_id`` , 很方便。

自己用 ``net/http``  标准库写的话，加强对请求处理流程的认识，请求处理流程的认识，然后后面写项目的话还是用框架写吧。然后后面写项目的话还是用框架写吧。

然后还有不懂的看``` <<go web 编程>>``` , 就封面是一个老头吊着一根棍子的，别搞错了， 我之前中文百度的时候搜出了另一本书  