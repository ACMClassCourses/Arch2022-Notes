# W11D1

## Tomasulo Design
![PPT Tomasulo Design](https://raw.githubusercontent.com/bytetriper/img/main/367c715fdf87a7a7d8366e4e4d3f7d3.jpg)
## Basic Design

略

## Exceptions

What's exception?

From Software to stop CPU:Exception

From IO to stop CPU:Interrupt

According to Alei,normally only Page Fault Exception is tolerated by the OS.

#### Context Switch:

```mermaid
graph TB

Interrupt_happens-->Onrun_Program_Ends
Onrun_Program_Ends-->Bunch_of_NOP
Bunch_of_NOP-->Clear_All_Component
Clear_All_Component-->New_Program_Run
New_Program_Run-->Interrupt_ends

```

#### How to Rerun the program after interrupt?
**Precise Interrupt**:

When Interrupt Happens on some Fixed instruction,the architecture guarantees that every instruction **before** it is done, while every instrction **after** it uncommited.

This job is easily done,thanks to Reorder Buffer(ROB or 重排序缓冲区).

剩下的就是阿磊老师漫谈历史时间🕶️




