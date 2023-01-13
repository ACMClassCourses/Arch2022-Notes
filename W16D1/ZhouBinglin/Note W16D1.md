# 期末复习

## 1. 事务内存

不考虑一个核上跑多个Tx的情况。

会考使用addm， xbegin， xend等指令测量L1 cache大小的方案。

## 2. Store buffer

一个核一个store buffer，作用是避免了核间通信，加快速度。

有FIFO和非FIFO之分，FIFO能够保证其他核看到的写顺序是一样的。

## 3. MESI 与 ESI的差异，机器状态和祖安环

## 4. RAIDS

RAIDS-01:先做条带，再作镜像。

RAIDS-10:先做镜像，再作条带。

综合来说 RAID-10优于RAIDS-01。

## 5.MPK

染色，用 “域” 表示读写权限，使用 PKRU 寄存器来表示不同 “域” 的读写权限。