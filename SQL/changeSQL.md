## 数据库的修改

***分为以下三类***

* INSERT [^注释1]
* UPDATE[^注释2]
* DELETE [^注释3]

[^注释1]: 插入新数据
[^注释2]: 更新已有纪录
[^注释3]: 删除已有记录

#### INSERT

```
INSERT INTO <表名> (字段1, 字段2, ...) VALUES (值1, 值2, ...);
```

自增主键可以由数据库自己推算出来，不需要人为的去添加。

我们可以一次向一个表内插入一个或多个信息。

#### UPDATE

`UPDATE`语句的基本语法是：

```
UPDATE <表名> SET 字段1=值1, 字段2=值2, ... WHERE ...;
```

同样的，也可以对一个表内的多个数据进行操作，同时进行修改。

要特别小心，update可以没有where，此时会对整张表进行更新，这点要特别重视。

~~还真想这样试一试~~

#### DELETE

`DELETE`语句的基本语法是：

```
DELETE FROM <表名> WHERE ...;
```

可以一次删除多条数据。

如果没有可以匹配的条件，将不会有任何信息被删除。

但是，特别注意，如果没有where，将会导致整张表被删除。~~我想学长肯定犯过这样的错~~
