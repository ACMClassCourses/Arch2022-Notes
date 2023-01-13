## RW : scoreboarding  vs.  Tomasulo

Inventor of scoreboarding : Seymour Cray

renaming : 标注是哪条指令的结果

乱序 ： make FUs busy

Pentinum 处理器 ：放入了所有指令

### 1. Branch (RW : delay slots 填充指令)

Branch Prediction algorithom

思想：

- 历史预测未来

#### 1.1 2-bit Scheme 2位饱和计数器 

思想：迟滞性响应

#### 1.2 corelating Branch Predictors

多个计数器，先通过 hash 确定行

Q：$b_i,b_j$ 对应到同一行？

A：全局计数器，看历史前2条，判断用哪列

#### 1.3 Tournament 锦标赛

基本思想： 多预测器

- global predictor
- local predictor



### 2. BHT (data structure to help 1)

branch history table

BTB: branch target buffer



### 3. special case return addr

例：UALR 实际上难以预测跳到的地址

对 BTB 提出挑战



### 4. virtual registers

hold both arvhitecturally visible (ASM code visible) + temp. value

e.g. X86 CISC Arch, RISC micro-arch