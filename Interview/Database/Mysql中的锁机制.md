## 锁的认识
### 1.1 锁的解释
计算机协调多个进程或线程[[并发]]访问某一**资源**的机制。
### 1.2 锁的重要性
在数据库中，除传统计算资源（CPU、RAM、I\O等）的争抢，数据也是一种供多用户共享的资源。
如何保证数据并发访问的一致性，有效性，是所有数据库必须要解决的问题。
锁冲突也是影响数据库并发访问性能的一个重要因素，因此锁对数据库尤其重要。
### 1.3 锁的缺点
加锁是消耗资源的，锁的各种操作，包括获得锁、检测锁是否已解除、释放锁等 ，都会增加系统的开销。
### 1.4 简单的例子
淘宝双十一活动，当天的人流量是千万及亿级别的，但商家的库存是有限的。
系统为了保证商家的商品库存不发生超卖现象，会对商品的库存进行锁控制。当有用户正在下单某款商品最后一件时，
系统会立马对该件商品进行锁定，防止其他用户也重复下单，直到支付动作完成才会释放（支付成功则立即减库存售罄，支付失败则立即释放）。
## 锁的类型
### 2.1表锁
#### 种类
##### 读锁（read lock）
也叫共享锁（shared lock）
多个事务可以同时对同一份数据进行读操作（select），但是无法都无法更新。
![[表级读锁]]
##### 写锁（write lock）
也叫排他锁（exclusive lock）
当前操作没完成之前，会**阻塞**其它读和写操作（update、insert、delete）。
> 上写锁之后，只有上了锁的事务可以读写数据，其他事务只能等待。
#### 上锁方式
##### 隐式上锁（默认，自动加锁自动释放）
```sql
select //上读锁

insert 、 update 、 delete //上写锁
```
##### 显式上锁（手动）
上完锁之后如果不手动解锁，之后便无法执行更新操作
```sql
lock table tableName read;//读锁

lock table tableName write;//写锁

unlock tables;//解锁
```
##### 读锁示意：

| 会话1 | 会话2 |
| ---- | ---- |
| lock table teacher read;// 上读锁 |  |
| select * from teacher; // 正常读取 | select * from teacher;// 正常读取 |
| update teacher set name = 3 where id =2;// **报错**因被上读锁不能写操作 | update teacher set name = 3 where id =2;// 被**阻塞** |
| unlock tables;// 解锁 |  |
|  | update teacher set name = 3 where id =2;// 更新操作成功\| |
|  |  |
**报错**：Table 'users' was locked with a READ lock and can't be updated
**被阻塞**:如我在Java中运行时，程序执行到`statement.executeUpdate`后，便不再运行了。
	![[Mysql上锁.gif]]
##### 写锁示意：

| 会话1 | 会话2 |
| ---- | ---- |
| lock table teacher write;// 上写锁 |  |
| select * from teacher; // 可以正常读取 | select * from teacher;// 被阻塞 |
| update teacher set name = 3 where id =2;// 可以正常更新操作 | update teacher set name = 4 where id =2;// 被阻塞 |
| unlock tables;// 解锁 |  |
|  | select * from teacher;// 读取成功 |
|  | update teacher set name = 4 where id =2;// 更新成功\| |
#### 存储引擎默认锁
```php
MyISAM
```
#### 特点
1. 对整张表加锁
2. 开销小
3. 加锁快
4. 无死锁
5. 锁粒度大，发生锁冲突概率大，并发性低
#### 结论
1. 读锁会阻塞写操作，不会阻塞读操作
2. 写锁会阻塞读和写操作
#### 建议
MyISAM的读写锁调度是写优先，这也是MyISAM不适合做写为主表的引擎，因为写锁以后，*其它线程不能做任何操作*，大量的更新使查询很难得到锁，从而造成永远阻塞。
### 2.2 行锁
#### 种类
##### 读锁（read lock）
也叫共享锁（shared lock）
允许一个事务去读一行，阻止其他事务获得相同数据集的**写锁**
##### 写锁（write lock）
也叫排他锁（exclusive lock）
允许获得排他锁的事务更新数据，阻止**其他事务**取得相同数据集的**读锁**和**写锁**
##### 为什么上了写锁，别的事务还可以读操作？
因为InnoDB有MVCC机制（多版本并发控制），可以使用快照读，而不会被阻塞。
##### 上锁方式
###### 隐式上锁（默认，自动加锁自动释放）
```sql
select //不会上锁

insert、update、delete //上写锁
```
###### 显式上锁（手动）
单独执行这条语句无法上锁，要在事务中执行。
```sql
select * from tableName lock in share mode; -- 读锁

select * from tableName for update; -- 写锁

-- 解锁方式;
1. 提交事务（commit）
2. 回滚事务（rollback）
3. kill 阻塞进程
```
###### 行级读锁示意：
| session01 | session02 |
| ---- | ---- |
| begin; |  |
| select * from teacher where id = 2 lock in share mode;// 上读锁 |  |
|  | select * from teacher where id = 2;// 可以正常读取 |
| update teacher set name = 3 where id =2;// 可以更新操作 | update teacher set name = 5 where id =2;// 被阻塞 |
| commit; |  |
|  | update teacher set name = 5 where id =2;// 更新操作成功\| |
###### 行级写锁示意：
| session01 | session02 |
| ---- | ---- |
| begin; |  |
| select * from teacher where id = 2 for update;// 上写锁 |  |
|  | select * from teacher where id = 2;// 可以正常读取 |
| update teacher set name =3 where id = 2 // 可以更新操作 |  |
|  | update teacher set name = 5 where id =2 //被阻塞 |
| rollback;//回滚 |  |
|  | update teacher set name = 5 where id = 2;// 更新操作成功 |
##### 意向共享锁（IS）
一个事务给一个数据行加共享锁时，必须先获得表的IS锁
##### 意向排它锁（IX）
一个事务给一个数据行加排他锁时，必须先获得该表的IX锁
#### 存储引擎默认锁
```php
InnoDB
```
#### 特点
1. 对一行数据加锁
2. 开销大
3. 加锁慢
4. 会出现死锁
5. 锁粒度小，发生锁冲突概率最低，并发性高
#### 事务并发带来的问题
##### 更新丢失
解决：让事务变成串行操作，而不是并发的操作，即对每个事务开始---对读取记录加排他锁
##### 脏读
解决：隔离级别为Read uncommitted
##### 不可重读
解决：使用Next-Key Lock算法来避免
##### 幻读
解决：间隙锁（Gap Lock）
### 2.3 页锁
开销、加锁时间和锁粒度介于表锁和行锁之间，会出现死锁，并发处理能力一般（此锁不做多介绍）
## 行锁的实现算法？

## 如何排查锁？
### 表锁
```sql
show open tables; -- 查看表锁的情况
```
有四列字段：
- **Database**：数据库名。
- **Table**：数据库中的表名。
- **In_use**：表示该表当前是否被使用。如果 `In_use` 的值为 1，表示该表正在被使用；如果为 0，表示该表当前没有被使用。
- **Name_locked**：表示该表的名称是否被锁定。1表示已经被锁定，0为未锁定。
```sql
show status like 'table%';
```
- Table_locks_immediate：表示已经**立即获得**的表锁的次数。
- Table_locks_waited：表示因为锁被占用而不得不**等待**的次数。如果这个值较高，可能表示系统上存在表锁竞争，因为一些事务正在等待获取表锁。
### 行锁
```sql
show status like 'innodb_row_lock%';
```
1. innodb_row_lock_current_waits //当前正在等待锁定的数量
2. innodb_row_lock_time //从系统启动到现在锁定总时间长度
3. innodb_row_lock_time_avg //每次等待所花平均时间
4. innodb_row_lock_time_max //从系统启动到现在等待最长的一次所花时间
5. innodb_row_lock_waits //系统启动后到现在总共等待的次数
### 优化建议？

## 死锁
#### 解释
指两个或者多个事务在**同一资源**上相互占用，并请求锁定对方占用的资源，从而导致恶性循环的现象
#### 产生的条件
1. 互斥条件：一个资源每次只能被一个进程使用
2. 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
3. 不剥夺条件：进程已获得的资源，在没有使用完之前，不能强行剥夺
4. 循环等待条件：多个进程之间形成的一种互相循环等待的资源的关系
#### 解决
1. 查看死锁：show engine innodb status \G
2. 自动检测机制，超时自动回滚代价较小的事务（innodb_lock_wait_timeout 默认50s）
3. 人为解决，kill阻塞进程（show processlist）
4. wait for graph 等待图（主动检测）
#### 如何避免
1. 加锁顺序一致，尽可能一次性锁定所需的数据行
2. 尽量基于primary（主键）或unique key更新数据
3. 单次操作数据量不宜过多，涉及表尽量少
4. 减少表上索引，减少锁定资源
5. 尽量使用较低的隔离级别
6. 尽量使用相同条件访问数据，这样可以避免间隙锁对并发的插入影响
7. 精心设计索引，尽量使用索引访问数据
8. 借助相关工具：pt-deadlock-logger
## 乐观锁与悲观锁
### 悲观锁
假定会发生并发冲突，屏蔽一切可能违反数据完整性的操作
- 实现机制：表锁、行锁等
- 实现层面：数据库本身
- 适用场景：并发量大
### 乐观锁
假设不会发生并发冲突，只在提交操作时检查是否违反数据完整性
- 实现机制：提交更新时检查版本号或者时间戳是否符合
- 实现层面：业务代码
- 适用场景：并发量小
