[TOC]

### review of last week's software optimization

- unrolling
- pipelining
- loop-carried dependency has parallelism ? 
- conditions or predicated instructions
    - e.g. LWC (load word conditional)
    - supported by hardware

- exception behavior support
    - may cause page fault
    - prefetch we don't allow it to cause exception

- memory reference speculation

### what is atomicity ?

When multiple threads access the same memory location, atomicity requires "one at a time". When a instruction is executing, no other instruction can access the same memory location.

### LL/SC

load-linked and store-conditional

##### example of atomic swap

trying to swap register `R4` and memory location `R1`

```
try :
    mov R3, R4
    ll R2, 0(R1)
    sc R3, 0(R1)
    beqz R3, try
    mov R4, R2
```

when `sc` fails, the R3 will be 0, and we can retry the operation.

##### example of fetch-and-add

self-incrementing a memory location `R1` by `R3`

when `sc` fails, the `R2` will be 0, and we can retry the operation.

```
try :
    ll R2, 0(R1)
    add R2, R2, R3
    sc R2, 0(R1)
    beqz R2, try
```

### compare-and-swap

compare the value first, if same, than swap

however, CAS can't handle ABA problem

### ABA problem

ABA problem means that the value is changed from A to B, and then back to A. If we use CAS, we can't detect this.

ll/sc instruction can solve this problem, as sc directly detect the location has been written by other threads. If the location has been written, a register will be set to 0, even the data is the same.