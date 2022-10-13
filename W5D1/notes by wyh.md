## 10.10

revise: Memory Hierarchy

### Memory Technology

> "所有运行的代码和数据在运行是一定在 mem 里, 是唯一能直接访问到的, Disk 是不能直接访问的……" ——Alei

### Data Storage
状态逻辑 (vs.组合逻辑)

#### 锁存器

![1.png](https://s2.loli.net/2022/10/11/yF8Sg7n1rTldiOA.png)
(图来源于梁亚伦)

发展:
- Electrical (ms)
- Electronic (ms, ns)
- static (RS)
- Dynamic

电容作为锁存器:

电容充放电需要时间 -> 发展速度较慢

![2.jpg](https://s2.loli.net/2022/10/11/2cBmsDZYqNparjG.png)

发展(即充放电时间变小): 应使 **电容变小** 或 **电压变小**

不同种类: SRAM/DRAM/ROM/EPROM(or flash)/NAND

### Interface

#### DRAM + CPU 示意图


```
                          ┌─────────────────┐
┌───────────┐             │                 │
│           │    m-bit    │     Memory      │
│         <─┼─────addr────┼──>              │
│    Core   │             │                 │
│         <─┼─────data────┼──>              │
│           │             │  2^m location   │
└───────────┘             │                 │
                          └─────┬───────────┘
                                │
                                └──── I/O: I=read, O=write
 ```

e.g.
回到 80 年代, 我们在市场上定制到的 memory 宽 1 bit, 大小为 1K, 现要组成 宽 1 byte, 大小为 64K 的 memory.

考虑 8 个 chip 组成一个 memory module, 共 64 module, 每个 module 连 10 根线, core 连出 16 根线, 中间接一个 6-64 译码器来决定数据存放在哪个 module, 设一个 switch 即可.


### DRAM Read Timing

![3.jpg](https://s2.loli.net/2022/10/11/e78kRtA2wWJ9CQb.png)

`L` 低电平有效

`RAS` ROW Adress Selection

`CAS` COLUMN Adress Selection

`WE` Writing Enable

`OE` Output Enable

