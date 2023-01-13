# Arch W8D1 Notes

## Cache Summary

non-blocking cache

hit under N miss (outstanding $\neq$ out-of-order)

- use MSHR(miss status handling register)

## Virtual Memory

Virtual address mechanism:

processor send virutal address $a$

translate to physical address $a'$

- success: visit main memory
- fail: fault / exception $\to$ search in virtual memory $\to$ send to main memory $\to$ retry translation



Translation unit

- section (large fixed size)
- segment (arbitrary size, complicated for programmer and compiler)
  - fragment
    - internal (allocated but not used)
    - external (fragments that cannot be allocated)
- page (trade off)
  - small fixed size
  - reduce internal fragments



Page

virtual address = virtual page + offset

physical address = physical page + offset

vp $\to$ pp: page table(in physical memory, not accessible itself)



Virtual addressing cache

query cache (use va) before translation