### Hardware Support for Memory Reference Speculation

When $M_x \neq M_y$:

1. Store My
2. Load Mx

- Optimization: Let `Load Mx` to be executed earlier by switching the execution order.


- Hazard: error occurs when Mx = My. 



### Spinlock 

A locking mechanism is called a **spinlock**(non-blocking locker)

- spinlock V.S. Mutex: 

  In spinlock, the task cannot sleep while waiting for the lock, whereas in mutex, the task can sleep while waiting for the lock. 

### Load link & Store conditional:

- definition: it's a mechanism.
- usage: to detect whether `load/store` instruction is **atomic**.

e.g.1

```
; swap operation
; suppose R4 = y, mem[0(R1)] = x

mov R3, R4		; R3 = y
ll  R2, 0(R1) ; R2 = x
sc  R3, 0(R1) ; mem[0(R1)] = y;
beqz R3, try
mov R4, R2 		; R4 = x 
```

e.g.2

```
ll 	R2, 0(R1)
addi R2, R2 #1 ; increment
sc	 R2, 0(R1)
beqz R2, try
```

procedure can be described as follows:

1. Load [Mx] $\rightarrow$ R2
2. R2++
3. store R2's value into Memory

If Step 1-3 are **non-atomic**, say, [Mx] had been modified by others during Step 2.

Solution:

- if (LR ≠ 0) { LR = 0, R2 = 1} success // not interrupted by others
- if (LR = 0) R2 = 0 // interrupted
  - `beqz R2, try` will redo the procedure until success



- Q: nested ll/sc ? (i.e., doing `sc Mx`, `sc My` simultaneously)

  A: no (because we only have 1 single LR...)

LR: linker register

ll/sc V.S. CAS (compare and swap)

