The key idea is to ensure that a processor has **exclusive** access to a data item before writing that item. This style of protocol is called a _write invalidate protocol_.

An alternative protocol is to update all the cached copies of a data item when that item is written. It's called _write update protocol_. It considerably consumes more bandwidth than _write invalidate protocol_.

## Implementation Techniques

To perform an invalidate, simply:

1. The processor acquires bus access and broadcasts the address to be invalidated on the bus
2. Other processors snoop on the continuously, watching the address, checking if it's inside their cache. If so, the corresponding data in the cache are invalidated.

When a write to a block that is shared occurs, the writing processor must acquire bus access to broadcast its invalidation. There is a case that two processors attempt to write shared blocks at the same time, and their attempts to broadcast an invalidate operation will be **serialized** when they arbitrate for the bus. This also solves the problems where two processors write the same block **simultaneously**.

When a cache miss occurs, the block should be located in some way when using write-back cache, leading to the [[Snooping Coherence Protocols]]. For write-through cache, there is no such concern. (Write buffers would lead to some distinction, where write-through cache could be as complicated as write-back cache.)

For write-back cache, it snoops on the bus both for invalidation and for cache miss. If it has a dirty copy of the requested cache block, it **provides that cache block in response to the read request** and **cause the memory access to be aborted**.

An extra state bit associated with each cache block is needed to track whether or not a cache block is **shared**, which is used to determine **whether or not to send** the invalidation onto the bus, because only the first time the block is modified will the processor sends out invalidation.

There might be **interference** between bus access and cache access. One way is to **duplicate** the tags and have snoop access on the duplicate tags. Another way is to establish **directory** in L3 cache to indicate whether ot not a given block is shared and possibly which block might have copies.

## Principles

The key ideas behind the protocols are:

- Any valid cache blocks are either in the **shared state in one or more private caches** or in the **exclusive state in exactly one cache**.
- Any trasition to the exclusive state requires an **invalidate or write miss** to be placed on the bus, causing all local blocks invalid.
- Any memory block that is in the shared state is always up to date in the outer shared cache.

There might be some issues that complicate the implementation:

- The protocol has assumed that operations are atomic. However, in reality, to gurantee that requires a lot of work.

## Extensions to the Basic Coherence Protocol

The basic coherence protocol, also could be called as MSI, has many extensions:

### MESI

_MESI_ is the protocols with additional state _Exclusive_ relative to MSI.

If a block is in **exclusive** state, it can be written **without generating any invalidates**, which optimizes the case where a block is read by a single cache before being written by that same cache.

In particular, if another processor issues a read miss, the state is changed **from exclusive to shared**.

### MOESI

_MOESI_ adds the state owned to the _MESI_ protocol to indicate that the associated block is owned by that cache and out-of-date in memory.

In this protocol, the block can be changed from modified to owned without writing it to memory. Other caches, which are newly sharing the block, keep the block in the shared state.

## Implementations Difficulties

As mentioned before, the snooping coherence protocol has non-atomic write and upgrade misses.

In a multicore with **a single bus**, these steps can be made effectively atomic by arbitrating for the bus to the shard cache or memory first and not releasing the bus until all actions are complete. In early design, **a single line** was used to signal when all necessary invalidates had been received and were being processed.

In a multicore using multiple buses, **races**, namely two processors attempt to write the same block at the same time, could be eliminated if each block of memory is associated with **a single bus**, ensuring that two attempts to access the same block must be serialized by that common bus.
