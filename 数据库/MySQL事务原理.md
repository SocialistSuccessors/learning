#### MySQL 事务基础概念
事务（Transaction）是访问和更新数据库的程序执行单元；事务中可能包含一个或多个 sql 语句，这些语句要么都执行，要么都不执行。
![1554277191631.jpg](https://i.loli.net/2019/04/03/5ca46396f22cd.jpg)
如上图所示MySQL 服务器逻辑架构从上往下可以分为三层：
- 第一层：处理客户端连接、授权认证等。
- 第二层：服务器层，负责查询语句的解析、优化、缓存以及内置函数的实现、存储过程等。
- 第三层：存储引擎，负责 MySQL 中数据的存储和提取。MySQL 中服务器层不管理事务，事务是由存储引擎实现的。
MySQL 支持事务的存储引擎有 InnoDB、NDB Cluster 等，其中 InnoDB 的使用最为广泛；其他存储引擎不支持事务，如 MyIsam、Memory 等。

#### 提交和回滚
典型的 MySQL 事务是如下操作的：
![1554277910698.jpg](https://i.loli.net/2019/04/03/5ca466587c6aa.jpg)
其中 start transaction 标识事务开始，commit 提交事务，将执行结果写入到数据库。
如果 sql 语句执行出现问题，会调用 rollback，回滚所有已经执行成功的 sql 语句。当然，也可以在事务中直接使用 rollback 语句进行回滚。

#### 自动提交
MySQL 中默认采用的是自动提交（autocommit）模式，如下所示：
![1554277933677.jpg](https://i.loli.net/2019/04/03/5ca466588b383.jpg)
在自动提交模式下，如果没有 start transaction 显式地开始一个事务，那么每个 sql 语句都会被当做一个事务执行提交操作。
通过如下方式，可以关闭 autocommit；需要注意的是，autocommit 参数是针对连接的，在一个连接中修改了参数，不会对其他连接产生影响。
![1554277952288.jpg](https://i.loli.net/2019/04/03/5ca4665897ef1.jpg)
如果关闭了 autocommit，则所有的 sql 语句都在一个事务中，直到执行了 commit 或 rollback，该事务结束，同时开始了另外一个事务。

#### 特殊操作
在 MySQL 中，存在一些特殊的命令，如果在事务中执行了这些命令，会马上强制执行 commit 提交事务；如 DDL 语句(create table/drop table/alter/table)、lock tables 语句等等。
不过，常用的 select、insert、update 和 delete 命令，都不会强制提交事务。