# Note W14D1

by xjq

## Functions

Von Neuman

## Performance

### Parallelism

Pipeline

#### Basic Principle

- Balance (stage-stage)
- Speed up = N-stages

#### Hazard

stalls

##### Structural

Duplicating

eg. memory conflict $\to$ I-Cache/D-Cache

##### Data

- RAW $\to$ Distance Prod/Cons 
- WAR, WAW $\to$ renaming

##### Control

a control list (JMP B CALL/RET)

- do nothing
- kill branch
- delay-slot

### Locality

Cache

$AMAT_{Cahce}=T_{hit}+\eta_{miss}\times T_{penalty}$

- $T_{hit}$ : small, DM is fast and FA is slow
- $\eta_{miss}$ : high associative, small miss-rate
- $T_{peralty}$ : Mem (L2-Cache) $\to$ wider bus, multi-bank 

### Reducing Latency

- freq
- CLA

### Principles

- Small: fast
- Simple: RISC
- Tradeoff/compromise
- Amdahl's law: =$S_P=\frac{1}{(1-\eta)+\eta/s}$