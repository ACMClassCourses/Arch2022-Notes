## 12.21

alei 老师的复习课

### Pipeline Loop

计算 branch prediction 的命中率

### RAID 0-1 vs. RAID 1-0

区别：先组成 RAID 1 和先组成 RAID 0 的区别

### Consistency Model
> contract between Software and Memory

#### with sync

+ strict
  + 上帝时钟

+ sequential
  + 需保持指令的先后执行顺序

+ casual
  + 保证内存层面上因果关系即可

+ Intel TSX
  + 依赖 Cache snoopy 一致性协议

**Example**

```text
P1  W(x)1                 W(x)3

P2          R(x)1  W(x)2

P3          R(x)1                 R(x)3  R(x)2   not sequential  \
                                                                  |-> but casual consistency
P4          R(x)1                 R(x)2  R(x)3   almost strict   /
```

#### without sync(i.e. lock...)

+ 在程序运行中设置同步点，只有当所有同步点都被达到后才能继续运行
+ 要求较为严格，时间花费太大