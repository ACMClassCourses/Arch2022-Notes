# W15D2 Notes

林田川  2022.12.21

## RAID10 vs RAID01

- RAID0: 条带，并发写
- RAID1: 镜像

- RAID10：先做镜像，然后再做条带。RAID0(RAID1, ... , RAID1)  
- RAID01：先做条带，然后再做镜像。RAID1(RAID0, RAID0)

以 6 个盘为例，RAID10 先将盘分成 3 组镜像，然后再对这 3 个 RAID1 做条带。RAID01 则是先利用 3 块盘做 RAID0，然后将另外 3 块盘也组成 RAID0 作为镜像。

RAID10 比 RAID01 在安全性方面要强。以 4 块盘为例来介绍安全性方面的差别：

- RAID10
  `RAID0( RAID1(DISK0, DISK1), RAID1(DISK2, DISK3) )`
  假设当 DISK0 损坏时，在剩下的 3 块盘中，只有当 DISK1 一个盘发生故障时，才会导致整个 RAID 失效，我们可简单计算故障率为 1/3。
- RAID01
  `RAID1( RAID0(DISK0, DISK1), RAID0(DISK2, DISK3) )`
  假设 DISK0 损坏，这时左边的条带将无法读取。在剩下的 3 块盘中，只要 DISK2，DISK3 两个盘中任何一个损坏，都会导致整个 RAID 失效，我们可简单计算故障率为 2/3。

## 内存一致性模型 Consistency model

### 强一致性

不需要手动同步。

#### Strict consistency

每个内存写入都应当立即被所有处理器看到。

#### Sequential consistency

对同一个数据执行的相对顺序，在各个处理器看来都保持一致。

#### Causal consistency

有因果关系的操作的相对顺序在所有处理器看来保持一致。

只有写操作之间有因果关系。写操作 B 依赖于先前的写操作 A，如果执行写操作 B 的处理器在执行 B 之前读取了写操作 A 的结果。下面是符合 causal consistency 的一个例子。

| Sequence | P1    | P2    | P3    | P4    |
| -------- | ----- | ----- | ----- | ----- |
| 1        | W(x)1 | R(x)1 | R(x)1 | R(x)1 |
| 2        |       | W(x)2 |       |       |
| 3        | W(x)3 |       | R(x)3 | R(x)2 |
| 4        |       |       | R(x)2 | R(x)3 |

W(x)2 依赖于 W(x)1，因为 P2 在 W(x)2 之前执行 R(x)1，读取了 W(x)1 的结果。所以在所有处理器看来，W(x)2 都应当在 W(x)1 之后发生。注意到 R(x)2 和 R(x)3 在 P3 和 P4 看来相对顺序不同，因此这个例子不符合 sequentially consistency。

#### Pipelined RAM consistency (PRAM consistency)

同一个处理器上的写的相对顺序得到保持。

### 弱一致性

需要手动同步。
