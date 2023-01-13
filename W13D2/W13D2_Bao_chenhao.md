### Hardware support for exposing more parallelism at compiler-time

We can use predicate version load word(LWC).
Load occurs unless the third operand is 0.

### Hardware support for memory reference speculation

When we met
- Store Mx
- Load My
  
We can put load earlier before Store.

But we have one problem, if Mx=My we can just do a check load at the first load space.

### Spinlock 
A locking mechanism called nonblocking locker.
It can't sleep while waiting the task.

### Load Link && Store conditional

It can detect that whether `load/store` instruction is **atomic**.
(transaction memory)
```
; swap operation
; suppose R4 = y, mem[0(R1)] = x
mov R3, R4		; R3 = y
ll  R2, 0(R1) ; R2 = x
sc  R3, 0(R1) ; mem[0(R1)] = y;
beqz R3, try
mov R4, R2 		; R4 = x 
```

```
ll 	R2, 0(R1)
addi R2, R2 #1 ; increment
sc	 R2, 0(R1)
beqz R2, try
```

We explain the latter example.

First, if we use the origin load and store, we just increase the value in the memory whose address is R1. But this time if other people modify the value during the load and store, then we will get wrong value.

So we introduce a new register(linker register) to record the address R1, then when we do the store, then we check the register, if the address isn't equal to zero, then we store the value and change the register to zero. Else it fail, we try another time.

We have just one LR register, so we can do ll/sc in ll/sc which called nested ll/sc.

Compare and swap is different from ll/sc because it just compare the value but not pay attention to whether it has been modified.(ABA problem).