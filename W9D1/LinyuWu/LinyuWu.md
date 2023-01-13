## DRAM Technology

As early DRAMs grew in capacity, the cost of a package with all necessary lines was an issue. The solution was to multiple address lines, thereby cutting the number of address pins in half.

One-half of the address is sent first during the **row access strobe** (RAS), and the other half of the address, sent during the **column access strobe**, which follows RAS. These names come from the internal chip organization, because the memory is organized as a rectangular matrix addressed by rows and columns.

Dynamic stands for two things:

- The sensing wires that used to detect the charge must be precharged.
- On reading, a row is placed into a row buffer, where CAS signals can select a portion of the row to read out from the DRAM. Because reading a row destroys the information, it must be written back when the row is no longer needed. This write back happens in overlapped fashion(?). It might mean that the cycle time before a new row coul be read was larger than the time to read a row and access a portion of that row.

## Optimization Approaches

## Multibank

To handle multiple data cache acesses per block, e can divide the cache into independent banks, each supporting an independent access. Banks were originally used to improve performance of main memory and are now used inside modern DRAM chips as well as with caches.

## Interleaving

### Sequential Interleaving

A simple mapping that works well is to spread the addresses of the block sequentially across the banks, which is called _sequential interleaving_. It is slow because it contains division.

### Chinese Interleaving

The name is given by the theorem used to prove its correctness. Its $x = a \% 2^s$, $y = a \% (2^l - 1)$, and as long as $x$ and $y$ is co-prime, the theorem can make sure that with different $a$, the $(x, y)$ would never repeat.
