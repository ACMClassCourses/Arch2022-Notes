# Hierarchy

Registers -> L1 Cache -> L2 Cache -> L3 Cache -> Memory -> Disk -> Network

# Cache

- Principle
  - Locality
    - Temporary
    - Spatial
- Mapping
  - DM
  - FAC
  - SAC
- Organization

## Direct-Mapped Cache

A memory address could be divided into three parts: tag, index and bs (byte select), which consists $t$ bits, $s$ bits and $b$ bits, respectively.

Generally, cache consists of $S = 2^s$ cache set. Every cache set consists of $E$ cache line, which consists a block with $B = 2^b$ bytes. For a direct-mapped cache, the $E = 1$.

When a memory access happens, it first gets its group index to locate the right cache set. After that, it selects the first $t$ bits as tag, scanning the whole cache set (in this case, there is only one cache line) to check whether there is a cache line with the same tag with the address. If there is one, then the cache hit occurs, after which the cache is read and return. Otherwise, the cache miss occurs. The cache has to access the memory to get bytes in the memory, and replace the original bytes in cache, and then return it back.

## Full Associative Cache

Contrast to direct-mapped cache, $E = \frac{C}{B}$, meaning that it could be accessed without indexing, but directly goes to the right and the only one cache set. Then it uses its tag to index the cache line, and after that using the byte select to access the right offset.

## Set Associative Cache

The difference between directed-mapped cache and set associative cache is $E$. in set associative cache, $E$ is greater then $1$. For the choice of the cache set, it's similar with directed-mapped cache. After choosing the right cache set, it checks whether the desired tag is inside the cache lines. If it does, then it reads from the cache and returns back. However, if the tag isn't inside the cache lines, it has to replace one specified cache line in the cache set with the desired cache line. The algorithm to choose the particular cache line to be replaced is called **replacement algorithm**. There are two major easy algorithms called least-frequently-used algorithm and least-recent-used algorithm.

## Write

Write-through: After fetching the cache (or it already exists), we write the modified cache back to the lower level cache directly.
Write-back: Make modification only on the current layer of cache, mark the dirty bit to be one. Once the dirty cache line is selected as victim, write it back to the lower level cache and eject it.
