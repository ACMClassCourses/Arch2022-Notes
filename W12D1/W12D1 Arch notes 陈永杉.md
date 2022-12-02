## Arch W2D1 notes

###### 陈永杉

### Review : out of order

-Dynamic type: Tomasulo with reorder buffer

-Static: conde movement (achieved in compiler)

### Distributed Computing System

##### Shared memory and Snoopy Protocol

While multi-processer with private cache use one public mem, would in case of coherence. Which means, on data could have more than one copies in different caches and in memory. And they may can't keep same during the multi-processer execution.

Under the Share Memory Polymer:

after adding the cache, 

different processer: non-coherence

between cache and memory: inconsistency

Even write through can't solve the problem that difference between copies in different cache.

Solution: Snoopy (distributed) / Directory-based (centralized)

### Snoopy Protocol

every copy has three types:

invalidate: has no copy/ has a wrong copy

shared: read only

exclusive: can read and write, is the only copy of the newest data.

and with data fresh or write back, copies would change in these three types.

### consistency problem

suppose there are two programs:

```
a=0;
...
a=1;
if(a==0) then
  ex. pi;
```

```
b=0;
...
b=1;
if(b==0) then
ex. pj;
```

if both $a==0$ and $b==0$ ?

consistency requires different watcher can see it in the same order.

### improvement of ESI

add a new type "modify" , into MESI

