## W7D1 notes

**written by Chen Zejia.**

### Cache

* $AMAT = T_{hit} + \eta_{miss}\times T_{penalty}$
* Main reasons of miss: Compulsory, Capacity and Conflict.

### How to Reduce Misses

some feasible methods:

* Choose proper block size.
* Enhance the associativity.
* Victim Cache: add buffer to place data discarded from cache.
* Pseudo-Associativity: for example, toggle the highest bit of index.
* Hardware Prefetching: for example, add stream buffer between cache and memory. The structure of stream buffer is similar to victim cache and write buffer. When we extract data from the memory, we place extra block in stream buffer.
* Software Prefetching: access to the data in advance in order to load it to the cache.
  * Binding prefetch: load data to register. But it uses one register.
  * Non-Binding prefetch: just touch `Mx`. But it might be useless and the instruction set is more complex.

#### Compiler Optimizations

Reorder the procedures in order to reduce the conflict.

##### Merging Arrays

```c++
int val[SIZE];
int key[SIZE];//Before

struct merge{
    int val;
    int key;
}merged_array[SIZE];//After
```

Improve spatial locality by merging multiple arrays.

Note that the conflict of 2 arrays can be solved by victim cache. When the number of arrays in the conflict is greater than the size of victim cache, Merging Arrays can work.

##### Loop Interchange

```c++
for(k=0;k<100;k=k+1)
    for(j=0;j<100;j=j+1)
        for(i=0;i<5000;i=i+1)
            x[i][j]=2*x[i][j];//Before
            
for(k=0;k<100;k=k+1)
    for(i=0;i<5000;i=i+1)
        for(j=0;j<100;j=j+1)
            x[i][j]=2*x[i][j];//After
```

Swap the order of loops in order to sequential access the data. It improves spatial locality.

##### Loop Fusion

```c++
for(i=0;i<N;i=i+1)
    for(int j=0;j<N;j=j+1)
        a[i][j] = 1/b[i][j] * c[i][j];
for(i=0;i<N;i=i+1)
    for(j=0;j<N;j=j+1)
        d[i][j] = a[i][j] + c[i][j];//Before

for(i=0;i<N;i=i+1)
    for(j=0;j<N;j=j+1){
	    a[i][j] = 1/b[i][j] * c[i][j];
        d[i][j]=a[i][j]+c[i][j];
    }//After
```

2 misses per access to a&c vs. one miss per access.
Merge loops to sequential access the data. It improves spatial locality.

##### Blocking

```c++
for(i=0;i<N;i=i+1)
    for(j=0;j<N;j=j+1){
        r=0;
        for(k=0;k<N;k=k+1)
            r = r + y[i][k]*z[k][j];
        x[i][j]=r;
    }//Before

for(jj=0;jj<N;jj=jj+B)
for(kk=0;kk<N;kk=kk+B)
    for(i=0;i<N;i=i+1)
        for(j=jj;j<min(jj+B-1,N);j=j+1){
            r=0;
            for(k=kk;k<min(kk+B-1,N);k=k+1)
                r = r + y[i][k]*z[k][j];
            x[i][j] = x[i][j] + r;
        }//After
```

Access data by a certain block size in order to use cache more fully.
It works better with fully associative cache since fully associative cache can use the most of the space. And choosing proper size of block is also important.
