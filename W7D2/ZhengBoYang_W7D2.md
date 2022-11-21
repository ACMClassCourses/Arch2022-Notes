# W7D2
## How to Reduce Miss Penalty?
$AMAT_{Mem}=T_{addressing}+T_{assess}+T_{tranfer}$

### read priority over write on miss
Find $M_X$ Miss $\to$ Load from Memory into Cache and Read x right away$\to$ (If) conflicted $\to$ Write $M_y$ into Memory(in fact WB)

**Supplement knowledge**
Definition:
**Word**:Maximum Data a Order can control,normally the size of a cacheline.

$Word=\frac{Cache.size()}{Reg.size()}$

The bus Size rarely outweigh the "word".

So the CPU can fetch instruction at most of a word size per cycle from the bus.

### x First
When reading $M_x$ encounters a miss,we have to fetch a whole block from Memory,which consumes much more time than only fetching x itself.

Solutions:
* Fetching x first,then others. Pros: The Fastest. Cons:Disturbs the continuous Memory Reading Process
* Wait for the word(assume bus size=word) that contains x and take it right away.

### Non-blocking Caches
Multi-bank memories:
    Memories that have multi accessories,which allows more than one fetching orders to work at the (almost) same time.

怎么剩下的没讲了...

### Second-Level Cache:
Definition:
Local Miss Rate:Misses in L1 Cache
Global Miss:Misses that have to reach Memory
**Question**:
Should $L_1\subset L_2$?

AMD says:exclusive:$L_1\cap L_2=\varnothing$

Intel says:inclusive:$L_1 \subset L_2$
