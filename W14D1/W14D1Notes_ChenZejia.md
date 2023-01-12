## W14D1 notes

**written by Chen Zejia.**

### Functions

### Performance

* metric: CPI(Cycles per instruction) / MFLOPS
* how to make it faster: Reducing latency / Parallelism(Super Scalar/Pipeline) / Locality

### Principles

* Small (=fast)
* Simple (=regularity)
* Tradeoff / Compromise
* Amdahl's law: $Sp = \frac 1{1-\eta + \eta/s}$ (make the most common part faster)

### Parallelism: Pipeline(ILP)

* Balance(stage-stage)
* Speedup(potential) = N-stages

#### Hazard

* Structural: FU conflict. eg: Mem-conflict(load and instruction fetch) $\leftarrow$ I-cache / D-cache

* Data: **RAW**(true-dep) $\leftarrow$ Distance
  "small" distance: forwarding(H/W)
  "large" distance: out-of-order(H/W) or code movement(S/W)

  **WAR WAW**(Reg conflict)(pseudo-dep) $\leftarrow$ renaming register

* Control $\leftarrow$ Stall+Prediction / Kill branch / Delay slot filling

### Locality: cache

$AMAT = T_{hit}\mathrm{(cache)} + \eta_{miss-rate}\times T_{peralty}$
$T_{hit}$: DM is fast and FA is slow.       $T_{peralty}$ (depends on Mem) $\leftarrow$ Wider Bus / multi-bank

#### Def of Cache: DM/FA/SA

* DM line: valid+tag+data.
  Instruction: tag+index+bs and index decides which line the data in.
  width = $1 + t + 2^b$  lines = $2^i$, while $t$: length of tag, $i$: length of index, $b$: length of bs.
* FA
* SA = DM + FA
  N-way SA: $\mathrm{DM}_1$ $\mathrm{DM}_2$ ... $\mathrm{DM}_n$
