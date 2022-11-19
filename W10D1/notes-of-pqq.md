RAID: redundant array of inexpensive disk

- **Reliability:** How many disk faults can the system tolerate? 



### RAID-0

normal disk, can't tolerate any disk failure.

- **Reliability:** 0

### RAID-1(Mirroring)

def: More than one copy of each block is stored in a separate disk. 

Thus, every block has two (or more) copies, lying on different disks.

- **Reliability:** $ N / 2$ 

### RAID-3

def: **(Block-Level Stripping with Dedicated Parity)** 

![](https://media.geeksforgeeks.org/wp-content/uploads/raid4-1.png)

parity-based approach. 

can't read R0, R5 simultaneously. (P0 = D0+D1+D2+D3)

increase capacity compared to RAID-1.

### RAID-4

small read(without parity check/only checksum)

large write:

### RAID-5

![](https://media.geeksforgeeks.org/wp-content/uploads/raid10.png)

independent writes possible because of interleaved parity.

e.g. write to D0, D6 uses Disks 0, 1, 3, 4



### A Little Queuing Theory 

$Length=\lambda \cdot W$

- $\lambda$ : long-term average effective arrival rate
- $W$ : a customer spends in the system