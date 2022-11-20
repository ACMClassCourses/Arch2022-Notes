#### RAID

Its full name is "redundant array of inexpensive disk".

Redundancy refers to multiple components with the same function, so that the system can continue to operate in case of partial system failure.

- increase capacity and bandwidth 
- high data availablity

#### RAID 1

- The disk is completely copied to its "mirror".
- The effect is to recover lost data in an unexpected way.

#### RAID 3

- Parity Disk
- When the data in the current disk is lost, we can recover the data by adding other data in the disk to calculate the lost data.However, when two disks fail, this method cannot recover data.
- And it cannot read and write to two disks at the same time. RAID 3 relies on the parity disk, so it can't read or write two disks at the same time.

RAID 3 relies on the parity disk, so it can't read or write two disks at the same time.

#### RAID 4

Each sector in the disk has a parity called "self parity".
It supports small reads, but still only large writes.  - small read , large write.

#### RAID 5

It supports small writes in the following ways.
It has interleaved parity, which means that the two parity checks are located on different disks. We change the parity check to $P'+D=P+D'$, so we do not need to read all disks.

interleaved parity : two disks' parity disks are interleaved (in different stripe), so we can access them at the same time.

#### Interconnection

An (n,k) cube is a hypercube with n dimensions and k nodes in each dimension.

The diameter is defined as the maximum distance between two nodes (the number of links between them).
It is easy to know that if the diameter of the same node is the smallest, then its size is the largest.

