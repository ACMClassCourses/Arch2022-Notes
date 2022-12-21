## Arch W15D2 notes

###### 陈永杉

#### abstract

<img src="cys W15D2 1.jpg">

#### 1 pipeline

Memory Trace :  memories touched while loop executed.

Cache: calculate the situation of cache after code execution or the miss rate of cache.

pipeline: 

(base): instruction status at cartain time

(forwarding): how to reduce nop/stall 

if code with loop without jump predict, then we need to add nops. And how will it react with jump predictor. 

#### 2 RAID

RAID0: link the disks into a bigger one.

RAID1: make two teams of disks be mirror of each other.

#### 3 consistency

"transetion" : how to make sure each operation of the whole issue must be finished at the continuity way (rollback)

consistency model: contract between software and Memory.

(weak consistency ): add sync. only suit partical size is huge situation. Only make sure consistency at the consistency check point.

add absolute physical time temp to every data before give out.

Sequential consistency: every processers can see the same order from public memory.

Causal model: only make sure causality. 

Cohenrence: others should see change to data in time.

Weak memory model

PiperamRam model: all ram operation must be FIFO. make oricesser kill at same time possible. (a bit more loose)

<img src="cys W15D2 2.jpg">

intel TSX

first add doesn't affected by xbegin. 

addm: if confliex heppens, then abort at once, won't submit to memory.

if x0 or x1 is replaced before xend, then the whole issue would jump to abort without condition. 