#### docker

##### docker的架构

* docker的三大要素

  * 镜像（image）

    镜像就是模板，容器就是镜像的实例

    镜像就是一个只读的模板，镜像可以用来创建docker容器，一个镜像可以创建很多容器。

  * 容器

    容器是镜像创建的运行实例。他可以被启动，开始，停止，删除。每个容器都是相互隔离，保证安全的平台。可以把容器当做一个简易版的Linux环境。

  * 仓库

    仓库是集中存放镜像的地方。
  
* Linux的两大技术

  * namespace

    这个起到作用是隔离，让应用进程只能看到该namespace内的世界。

  * Cgroups

    这个的作用是限制，因为在本质上来讲，namespace技术起到的作用是对各个应用进程实现了隔离，但是本质上它们还是共用了宿主机的内核，所以存在一个进程抢占所有CPU资源的可能，于是需要这个control group 技术的诞生，来限制。真正意义上实现沙盒。

* 容器里看到的文件系统

  容器对文件存在这一个“挂载点”的认知。

##### 启动docker

* docker run

  run干了在本机中寻找上面的镜像。

* docker运行的机制和原理

##### dockerfile

dockerfile的设计思想就是使用一些标准的原语，描述我们所要构建的docker镜像。并且这些原语，都是按照顺序处理的。



