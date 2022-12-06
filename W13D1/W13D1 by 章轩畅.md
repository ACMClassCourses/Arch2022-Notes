# W13D1 Notes

章轩畅

## Software Scheduling

### Code Movement

#### Unrolling (loop) (simple)

* original version :

```
 1 Loop: L.D F0,0(R1) ;F0=vector element
 2 stall
 3 ADD.D F4,F0,F2 ;add scalar in F2
 4 stall
 5 stall
 6 S.D 0(R1),F4 ;store result
 7 DSUBUI R1,R1,8 ;decrement pointer 8B (DW)
 8 BNEZ R1,Loop ;branch R1!=zero
 9 stall ;delayed branch slot
```

   1 - 6 : payload

   7 - 8 : loop overhead

* revised version :

```
 1 Loop: L.D F0,0(R1)
 2 stall
 3 ADD.D F4,F0,F2
 4 DSUBUI R1,R1,8
 5 BNEZ R1,Loop ;delayed branch
 6 S.D 8(R1),F4 ;altered when move past DSUBUI
```

* unrolling ( 展开循环 ) :

```
1 Loop:L.D F0,0(R1)
2 ADD.D F4,F0,F2
3 S.D 0(R1),F4 ;drop DSUBUI & BNEZ
4 L.D F6,-8(R1)
5 ADD.D F8,F6,F2
6 S.D -8(R1),F8 ;drop DSUBUI & BNEZ
7 L.D F10,-16(R1)
8 ADD.D F12,F10,F2
9 S.D -16(R1),F12 ;drop DSUBUI & BNEZ
10 L.D F14,-24(R1)
11 ADD.D F16,F14,F2
12 S.D -24(R1),F16
13 DSUBUI R1,R1,#32 ;alter to 4*8
14 BNEZ R1,LOOP
15 NOP
```

* unrolling 优点：

  * 代码少

  * 量化分析：假设循环执行 1000 次, payload 用时 $t_1$, overhead 用时 $t_2$

    不展开 : $1000(t_1+t_2)$

    将 s 个循环展开成一个：$1000t_1+\frac{1000t_2}{s}$

* unrolling 缺点

  * 需要大量寄存器进行数据传输
  * 代码膨胀

* unrolling 条件

  * 每段代码没有相关性

  * 反例

    ~~~c++
    for (i=0; i<100; i=i+1) {
      A[i+1] = A[i] + C[i]; 
      B[i+1] = B[i] + A[i+1];
    }
    ~~~

  * 特殊情况下有相关性的循环也可以 unroll

    ~~~c++
    for (i=0; i< 8; i=i+1) {
      A = A + C[i];
    }
    ~~~

    <img src="C:\Users\27595\AppData\Roaming\Typora\typora-user-images\image-20221206192155581.png" style="zoom:50%">

#### Software pipeline

* 基本思路：把循环用 unrolling 展开，然后分析 pipeline

  <img src="C:\Users\27595\AppData\Roaming\Typora\typora-user-images\image-20221206191659912.png" style="zoom:35%">

* super scalar（多路径）

  一个部件在一个时刻可以处理多个 **数据**

  > tomasulo 处理时的多个 function unit，就是 super scalar

#### VLIW (Very Long Instruction Word)

* History
  * TI-DSP, 为了实现矩阵乘法
  * 通用处理器，把可以同时 issue 的指令合并成一个长指令

* unrolling

* S/W pipeline

  * To compiler to move loads across stores, when it cannot be absolutely certain that such a movement is correct, a special instruction to check for address conflicts can be included in the architecture.

    > load 和 store 地址不一样，但是同时用到了一个寄存器（立即数不同），那么不能随意移动

  * 解决方法（将一条 sp 指令放在 ld 指令位置，然后把 ld 指令往上移动）

    – The special instruction is left at the original location of the load and the load is moved up across stores
    – When a speculated load is executed, the hardware saves the address of the accessed memory location 
    – If a subsequent store changes the location before the check instruction, then the speculation has failed
    – If only load instruction was speculated, then it suffices to redo the load at the point of the check instruction

### Change

#### Kill BRANCH instruction (control hazard)

* conditional

  * LWC (条件执行指令)

    先进行 LW ，把结果保存在 tmp 中

    再判断目标的地址，如果不为0，就 commit tmp

    ~~~
    LW R1,40(R2)         ADD R3,R4,R5
                         ADD R6,R3,R7
    BEQZ R10,L
    LW R8,0(R10)
    LW R9,0(R8)
    ~~~

    改为

    ~~~
    LW R1,40(R2)         ADD R3,R4,R5
    LWC R8,20(R10),R10   ADD R6,R3,R7
    BEQZ R10,L
    LW R9,0(R8)
    ~~~

    用处：填充多发指令（Dual Issue) 情况下出现的空缺

    极端情况：If the sequence following the branch were short, the entire block of code might be 
    converted to predicated execution, and the branch eliminated.

* superblock

* trace cache

  * cache 的 block 存储分支语句中同一条路的指令

  * 作用：替代 I-Cache

    