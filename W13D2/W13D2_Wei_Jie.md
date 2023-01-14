#### Hardware Support for Memory Reference Speculation

We have just one LR register, so we can do ll/sc in ll/sc which called nested ll/sc.

When $M_{x}\not= M_{y}$, 

1. store $M_{y}$
2. load $M_{x}$

We can first load $M_{x}$, then store $M_{y}$. It is an optimization.

When $M_{x}= M_{y}$, we must obey the order----Hazard: error occurs when Mx = My. 

#### Spinlock

A locking mechanism is called a spinlock (non-blocking locker).

In spinlock, the task cannot sleep while waiting for the lock, whereas in mutex, the task can sleep while waiting for the lock. 

Load link & Store conditional: 

eg1:

1. mov R3, R4
2. ll  R2, 0(R1)
3. sc  R3, 0(R1)
4. beqz R3
5. mov R4, R2

eg2:

1. ll 	R2, 0(R1)
2. addi R2, R2 #1 
3. sc	 R2, 0(R1)
4. beqz R2



Compare and swap is different from ll/sc because it just compares the value but not pays attention to whether it has been modified.