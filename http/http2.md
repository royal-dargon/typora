### `http`

* `URL` 需要提供的信息有协议名，服务器地址，端口号，路径

  ```http
  http://localhost:8080/helloworld
  ```
  
  在这里，`http`就是起到了协议名的意思，其他的还有`https`之类的
  
  `localhost`就是服务器地址的意思，`localhost`表示的是本机的地址，有时，在主机名前也可以包含连接到服务器所需的用户名和密码（格式：`username:password@hostname`）。
  
  而`8080`表示的就是端口号
  
  后面则是跟着路径，一般用来表示主机上的一个目录或文件地址，通常由零或多个`/`隔开的字符串
  
  [详细介绍](https://blog.csdn.net/hhthwx/article/details/78567961)

使用`http`时必然是一段担任客户端角色，另一端担任服务端角色。

`http`协议规定，请求从客户端发出，最终服务端响应请求并返回。值得注意的是请求报文里面有请求的方法。例如，`get` ， `post` 等等。在服务端返回的时候会包含一个状态码，就是我们平时所熟知的`200`，`404`等等。

#### `HTTP`协议的方法

* GET 用于获取资源

  用来请求访问的资源。

* POST 用来传输实体主体

* PUT 用来传输文件

* DELETE 用来删除文件

* OPTIONS 用来询问支持的方法

* HEAD 获得报文的首部

* PATCH  在请求中定义了一个描述修改的实体的集合，如果被请求修改的资源不存在，服务器可能会创建一个新的资源

#### `HTTP Header` 的介绍

**HTTP头字段**（英语：HTTP header fields）是指在[超文本传输协议](https://zh.wikipedia.org/wiki/超文本传输协议)（HTTP）的请求和响应消息中的消息头部分。它们定义了一个超文本传输协议事务中的操作参数。HTTP头部字段可以自己根据需要定义，因此可能在 Web 服务器和浏览器上发现非标准的头字段。

HTTP 头字段根据实际用途被分为以下 4 种类型：

- 通用头字段(英语：General Header Fields)
- 请求头字段(英语：Request Header Fields)
- 响应头字段(英语：Response Header Fields)
- 实体头字段(英语：Entity Header Fields)\

## Requests部分

|       Header        |                             解释                             |                          示例                           |
| :-----------------: | :----------------------------------------------------------: | :-----------------------------------------------------: |
|       Accept        |                 指定客户端能够接收的内容类型                 |              Accept: text/plain, text/html              |
|   Accept-Charset    |                 浏览器可以接受的字符编码集。                 |               Accept-Charset: iso-8859-5                |
|   Accept-Encoding   |     指定浏览器可以支持的web服务器返回内容压缩编码类型。      |             Accept-Encoding: compress, gzip             |
|   Accept-Language   |                      浏览器可接受的语言                      |                 Accept-Language: en,zh                  |
|    Accept-Ranges    |           可以请求网页实体的一个或者多个子范围字段           |                  Accept-Ranges: bytes                   |
|    Authorization    |                      HTTP授权的授权证书                      |    Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ==    |
|    Cache-Control    |                 指定请求和响应遵循的缓存机制                 |                 Cache-Control: no-cache                 |
|     Connection      |      表示是否需要持久连接。（HTTP 1.1默认进行持久连接）      |                    Connection: close                    |
|       Cookie        | HTTP请求发送时，会把保存在该请求域名下的所有cookie值一起发送给web服务器。 |              Cookie: $Version=1; Skin=new;              |
|   Content-Length    |                        请求的内容长度                        |                   Content-Length: 348                   |
|    Content-Type     |                  请求的与实体对应的MIME信息                  |     Content-Type: application/x-www-form-urlencoded     |
|        Date         |                     请求发送的日期和时间                     |           Date: Tue, 15 Nov 2010 08:12:31 GMT           |
|       Expect        |                    请求的特定的服务器行为                    |                  Expect: 100-continue                   |
|        From         |                    发出请求的用户的Email                     |                  From: user@email.com                   |
|        Host         |                指定请求的服务器的域名和端口号                |                   Host: www.zcmhi.com                   |
|      If-Match       |                只有请求内容与实体相匹配才有效                |      If-Match: “737060cd8c284d8af7ad3082f209582d”       |
|  If-Modified-Since  | 如果请求的部分在指定时间之后被修改则请求成功，未被修改则返回304代码 |    If-Modified-Since: Sat, 29 Oct 2010 19:43:31 GMT     |
|    If-None-Match    | 如果内容未改变返回304代码，参数为服务器先前发送的Etag，与服务器回应的Etag比较判断是否改变 |    If-None-Match: “737060cd8c284d8af7ad3082f209582d”    |
|      If-Range       | 如果实体未改变，服务器发送客户端丢失的部分，否则发送整个实体。参数也为Etag |      If-Range: “737060cd8c284d8af7ad3082f209582d”       |
| If-Unmodified-Since |           只在实体在指定时间之后未被修改才请求成功           |   If-Unmodified-Since: Sat, 29 Oct 2010 19:43:31 GMT    |
|    Max-Forwards     |               限制信息通过代理和网关传送的时间               |                    Max-Forwards: 10                     |
|       Pragma        |                    用来包含实现特定的指令                    |                    Pragma: no-cache                     |
| Proxy-Authorization |                     连接到代理的授权证书                     | Proxy-Authorization: Basic QWxhZGRpbjpvcGVuIHNlc2FtZQ== |
|        Range        |                 只请求实体的一部分，指定范围                 |                  Range: bytes=500-999                   |
|       Referer       |         先前网页的地址，当前请求网页紧随其后,即来路          |     Referer: http://www.zcmhi.com/archives/71.html      |
|         TE          |   客户端愿意接受的传输编码，并通知服务器接受接受尾加头信息   |               TE: trailers,deflate;q=0.5                |
|       Upgrade       |    向服务器指定某种传输协议以便服务器进行转换（如果支持）    |     Upgrade: HTTP/2.0, SHTTP/1.3, IRC/6.9, RTA/x11      |
|     User-Agent      |            User-Agent的内容包含发出请求的用户信息            |          User-Agent: Mozilla/5.0 (Linux; X11)           |
|         Via         |            通知中间网关或代理服务器地址，通信协议            |       Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)       |
|       Warning       |                    关于消息实体的警告信息                    |             Warn: 199 Miscellaneous warning             |

## Responses 部分 

|       Header       |                             解释                             |                         示例                          |
| :----------------: | :----------------------------------------------------------: | :---------------------------------------------------: |
|   Accept-Ranges    |      表明服务器是否支持指定范围请求及哪种类型的分段请求      |                 Accept-Ranges: bytes                  |
|        Age         |     从原始服务器到代理缓存形成的估算时间（以秒计，非负）     |                        Age: 12                        |
|       Allow        |        对某网络资源的有效的请求行为，不允许则返回405         |                   Allow: GET, HEAD                    |
|   Cache-Control    |           告诉所有的缓存机制是否可以缓存及哪种类型           |                Cache-Control: no-cache                |
|  Content-Encoding  |            web服务器支持的返回内容压缩编码类型。             |                Content-Encoding: gzip                 |
|  Content-Language  |                         响应体的语言                         |                Content-Language: en,zh                |
|   Content-Length   |                         响应体的长度                         |                  Content-Length: 348                  |
|  Content-Location  |                请求资源可替代的备用的另一地址                |             Content-Location: /index.htm              |
|    Content-MD5     |                     返回资源的MD5校验值                      |         Content-MD5: Q2hlY2sgSW50ZWdyaXR5IQ==         |
|   Content-Range    |                在整个返回体中本部分的字节位置                |        Content-Range: bytes 21010-47021/47022         |
|    Content-Type    |                      返回内容的MIME类型                      |        Content-Type: text/html; charset=utf-8         |
|        Date        |                   原始服务器消息发出的时间                   |          Date: Tue, 15 Nov 2010 08:12:31 GMT          |
|        ETag        |                  请求变量的实体标签的当前值                  |       ETag: “737060cd8c284d8af7ad3082f209582d”        |
|      Expires       |                     响应过期的日期和时间                     |        Expires: Thu, 01 Dec 2010 16:00:00 GMT         |
|   Last-Modified    |                    请求资源的最后修改时间                    |     Last-Modified: Tue, 15 Nov 2010 12:45:26 GMT      |
|      Location      |  用来重定向接收方到非请求URL的位置来完成请求或标识新的资源   |    Location: http://www.zcmhi.com/archives/94.html    |
|       Pragma       |      包括实现特定的指令，它可应用到响应链上的任何接收方      |                   Pragma: no-cache                    |
| Proxy-Authenticate |         它指出认证方案和可应用到代理的该URL上的参数          |               Proxy-Authenticate: Basic               |
|      refresh       | 应用于重定向或一个新的资源被创造，在5秒之后重定向（由网景提出，被大部分浏览器支持） | Refresh: 5; url=http://www.zcmhi.com/archives/94.html |
|    Retry-After     |     如果实体暂时不可取，通知客户端在指定时间之后再次尝试     |                   Retry-After: 120                    |
|       Server       |                      web服务器软件名称                       |     Server: Apache/1.3.27 (Unix) (Red-Hat/Linux)      |
|     Set-Cookie     |                       设置Http Cookie                        |  Set-Cookie: UserID=JohnDoe; Max-Age=3600; Version=1  |
|      Trailer       |               指出头域在分块传输编码的尾部存在               |                 Trailer: Max-Forwards                 |
| Transfer-Encoding  |                         文件传输编码                         |               Transfer-Encoding:chunked               |
|        Vary        |        告诉下游代理是使用缓存响应还是从原始服务器请求        |                        Vary: *                        |
|        Via         |              告知代理客户端响应是通过哪里发送的              |      Via: 1.0 fred, 1.1 nowhere.com (Apache/1.1)      |
|      Warning       |                    警告实体可能存在的问题                    |          Warning: 199 Miscellaneous warning           |
|  WWW-Authenticate  |             表明客户端请求实体应该使用的授权方案             |                WWW-Authenticate: Basic                |

##### `cookies`

由于`http`是一种无状态的协议，所以服务器是无法对之前的客户端进行记录的，因此使用了`Cookie`技术，可以得到之前的状态信息。写在了请求和响应的报文内。比如你在登陆了淘宝后，系统再次访问其他页面，倘若需要验证用户权限，不可能让你再次登入，因此使用了这个技术。同理，token的作用也是类似。

#### 返回结果的`HTTP`状态码

* `2XX` 表示成功
  * 200 正常处理
  * 204 处理成功，但是没有资源返回
  * 206 表示客户端进行了范围的请求，服务端也成功执行了这个部分的请求
* `3XX` 表示需要重定向，表明浏览器需要执行某些特殊的处理以正确处理请求
  * 301 表示资源的位置永久更换了
  * 302 表示的是临时更换了位置
* `4XX` 表示客户端错误
  * 400 表示请求报文内存在语法错误
  * 401 表示认证失败，页面需要认证信息
  * 403 表示访问被服务端拒绝了
  * 404 表示服务器上没有请求的资源
* `5XX` 表示服务器的错误
  * 500 表示服务端本身的问题
  * 503 表示服务端暂时处于超载或者停机维护

