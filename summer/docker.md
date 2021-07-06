### 暑期实训

#### 数组

* 定义 具有相同元素的集合

* 求二维数组的行列数

  ```c
  int a[][3] = {1,1,2,3,1};
  int lenthf = sizeof(a)/sizeof(a[0]);
  int lenths = sizeof(a[0])/sizeof(a[0][0])
  ```

#### docker

* 解决了运行环境与配置问题软件容器，方便做持续集成并有助于整体发布的容器虚拟化技术
* docker三要素***镜像，容器，仓库***
* docker能-干什么

  * 虚拟机技术
  * 容器虚拟化技术
  * 开发/运维  ~~运维的危机~~
  * 企业级
* docker与虚拟机之间的区别

  * 虚拟机的缺点
    * 占用资源过多
    * 冗余步骤多
    * 启动慢
  * Linux容器不是对完整的操作系统进行模拟，而是对进程进行隔离。容器与虚拟机不同，不需要捆绑一整套操作系统，只需要软件工作所需的资源库与设置。系统因此变得高效轻量。
  * 比较了docker和传统虚拟化方式的不同之处
    * 传统的虚拟机技术是虚拟出一套硬件后，在其上运行一个完整的操作系统，在该系统上再运行所需应用进程。
    * 而容器内的应用进程直接运行于宿主的内核，容器内没有自己的内核，而且也没有进行硬件虚拟。
    * 每个容器之间相互隔离，每个容器有自己的文件系统，容器之间的进程不会互相影响，能区分计算资源。
* 为什么用docker
  * 一个宿主机可以部署上百个容器。
* 去哪下载docker
  * 官方   建议使用中文版
  * 仓库   docker hub 就是运行环境的打包封装，上面存的都是镜像
* docker的安装

#### Sql Sever

* 查询
  * 普通查询
  * 接条件查询
  * 全连接查询
  * 连接查询

* 创建表的时候的五大约束

  * 主键约束 

    ```sql
    eId int primary key indentity(1001,2) not null
    ```

  * 唯一约束

    ```sql
    eName varchar(20) unique not null
    ```

    可以让列中的元素唯一

  * 检查约束

    ```sql
    eAge int check(eAge>15 and eAge<30) not null
    ```

  * 默认约束

    ```sql
    eGender char(2) default('男') not null
    ```

    在插入表的时候如果是默认值就是填入默认值

  * 外键约束

    ```sql
    bAuthor int foreign key references empInfo(eId) not null
    ```

    该约束的意思是该列的元素在外界特定的地方是可以找到的。

* 插入数据

  ```sql
  insert into empInfo() values ()
  ```

  信息要一一对应

* 查询数据

  ```sql
  select *from empInfo
  ```

  表示查询该表内的所有信息，当然后面也是可以加 **where** 进行条件查询。

* 修改语句

  ```sql
  update empInfo set eHobby = '内容',eAge = 内容 where 条件
  ```

* 删除语句

  ```sql
  delete from table where content
  ```

  

