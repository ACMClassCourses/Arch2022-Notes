## 11.2

### Cache (cont'd)

#### Virtual Cache

+ Cache 中使用虚拟地址

+ 地址转换发生在 Cache 和 Memory 之间

#### Physical Cache

+ Cache 中使用物理地址

+ 地址转换发生在 Core 和 Cache 之间

#### Difference

假设正常情况下地址转换延迟与内存访问延迟数量级相同。考虑在一个实例中，地址转换延迟为 100, 内存访问延迟为 100, Cache 访问延迟为 1。

+ Virtual Cache
  + hit: 1
  + miss: 1 + 100 + 100

+ Physical Cache
  + hit: 100 + 1
  + miss: 100 + 1 + 100

而一般来说 miss rate 数值较小，故从时间延迟上来看，Virtual Cache 更优。

但实际上 Virtual 存在以下问题：

+ Synonymous: 同一个虚地址在不同列表内对应不同物理地址；
+ Alias: 多个虚地址指向同一个物理地址，从而引发同步问题。

实际上这两个问题都不难解决。

对于 Synonymous，可以直接在 Cache 中的 tag 中加上进程的信息（PID）；

对于 Alias，考虑下图。由于利用 virtual adress 在 Cache 中寻址时会根据 index 定位，那么只需要保证同一个物理地址 index 相同就行（即使需要替换也不会出现多个备份，就不会有不同备份间的 sync 问题）

```plain
virtual address
               |<----d--->|
[   page no.   |   disp   ]

cache
|<----t---->|<--i-->|<-b->|
[    tag    | index | bs  ]
```

通过增加 $d$ （增加 page size）或者减小 $i$ （增加关联度）的方法可以使得 $d\ge i+b$，从而保证不会出现 Alias 问题。 