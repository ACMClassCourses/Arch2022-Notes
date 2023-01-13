## Cache

![image-20230113131904863](D:\Users\JXGuo\OneDrive\studying_materials\computer_related\computer_arch\note_doc\assets\image-20230113131904863.png)



- MR: miss rate
- MP: miss penalty
- HT: hit time



RW: non-blocking Cache ? ( in P83 )

reduce $T_{hit}$: prefetch, outstanding...

需要寄存器：Miss Status Holding Registers





##  Virtual Memory

disk 内划分一块作为 mem

### virtual address

![b9809bc2ea3a519a68215e82d562a12](D:\Users\JXGuo\OneDrive\studying_materials\computer_related\computer_arch\note_doc\assets\b9809bc2ea3a519a68215e82d562a12.jpg)

#### Translation

- section
- segment
- page



碎片分类：external fragment, internal fragment



### Page

- VA : (vp # , offset)

- PA : (physical page # , offset)

- translate : page table in mem



### 与 Cache 的关系

1. virtual addressing cache ： 歧义 (ambiguity) & 别名 (alias)  
2. physical addressing cache : 每次访问 Cache 都要翻译，开销大

hint : 当 page 字段够左边，此时不会出问题