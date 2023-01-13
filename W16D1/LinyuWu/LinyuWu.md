## Transaction Memory

考虑 snooping 协议于 txn mem 的关系。

与 database 的 txn 几乎一致。

一些特例：cache conflict

测 L1 Cache？测试是否 abort 来实现。

## Store Buffer

弱内存模型核心：store buffer。

考虑 store buffer 是否是 FIFO，考虑多核间通信。

## MESI

参考 W12D2 的笔记。

## RAIDS

RAID01: 先做 RAID0，再做 RAID1
RAID10: 先做 RAID1，再做 RAID0

相关硬件实现：page size？

## Memory Protection Keys

优化修改权限的过程。大批量修改权限。用一个 register 来表示不同 domain 的不同权限。

在 entry 里增加两位表示 domain 的编号。
