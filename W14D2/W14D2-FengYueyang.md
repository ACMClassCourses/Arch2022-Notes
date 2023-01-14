## 期末相关考点

### 基础知识

一些考点：

- Cache Miss多少次
  - write back / write through
  - write allocation / write around
- Cache Hit Ratio
- 分支命中次数
- Tomasulo填表格
- RISC-V流水线表格（带有forwarding）

### 事务内存

#### 问题



#### 事务

事务是并发控制的单位，是用户定义的一个操作序列。

- 原子性(Atomicity)： 事务是数据库的逻辑工作单位，事务中包括的诸操作要么全做，要么全不做。
- 一致性(Consistency)： 事务执行的结果必须是使数据库从一个一致性状态变到另一个一致性状态。一致性与原子性是密切相关的。
- 隔离性(Isolation)： 一个事务的执行不能被其他事务干扰。
- 持续性/永久性(Durability)： 一个事务一旦提交，它对数据库中数据的改变就应该是永久性的。

把一堆操作“打包”到一起

### 弱内存模型



### RAID10和RAID01



### 内存保护键



内存屏障



- 怎么在RISCV上实现 Txbegin，Txend

- 怎么用xbegin和xend测L1 cache 大小



- 加入store buffer后加速的原因？
  - 不用等待核间通信的时间
- 会带来什么问题？核心原因是什么
- store FIFO和非FIFO区别？



- 硬件级别的RAID支持？
- 比较RAID10和RAID01在实现上的区别
