ARTS
====

## Algorithm

## Review

* https://medium.com/@ApsOps/an-illustrated-guide-to-kubernetes-networking-part-1-d1ede3322727 
* https://medium.com/@ApsOps/an-illustrated-guide-to-kubernetes-networking-part-2-13fdc6c4e24c

* [做个有深度的DBA：MySQL锁机制实践](https://mp.weixin.qq.com/s/zi86vvktNbA0_R6s1P67iQ)

两种锁，元数据锁(MDL)，引擎锁（比如Innodb).

隔离级别 | 脏读 | 不可重复读 | 幻读 
----| ----| ---| ---
读未提交 | O | O | O
读提交 | X | O | O
可重复度 | X | X | O
串行化 | X | X | X

* 脏读：一个事物中读到其他事务未提交的数据
* 不可重复读：一个事务内根据同一个条件对行记录进行多次查询，但是搜出来的结果却不一致
* 幻读：同一个事务内多次查询返回的结果集不一样（比如增加了或者减少了行记录）

## Tip



## Share

[Python 文件批处理](./file_read.md) 进程Pool, 采用FIFO的策略调度。

Pool 和 Process，使用上比较
* pool 适合任务非常多，因为可以重复利用
* process 适合任务比较少，并且只需要一次完成的这种









