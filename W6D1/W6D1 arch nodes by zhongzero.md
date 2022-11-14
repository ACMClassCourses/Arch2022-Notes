# CPI,AMAT

$\text{CPI(Cycle Per Instruction)=ideal CPI + average stalls per instruction}$ 

$AMAT_{mem}(\text{Average memory access time})=T_{addressing}+T_{access}+T_{transfer}$ 

$AMAT_{cache}(\text{Average memory access time})=T_{hit}+MissRate*MissPenalty$ 



# i-cache,d-cache,unified cache

只保存指令的高速缓存称为i-cache

只保存数据的高速缓存称为d-cache

既保存指令又保存数据的高速缓存称为unified cache

现代处理器包括独立的i-cache和d-cache

独立的i-cache和d-cache的优点在于：i-cache通常只是只读的，可以针对它们使用不同的访问模式来进行优化(如指令主要要求空间稳定，数据主要要求时间稳定)，且它们可以有不同的块大小、相联度和容量。且分开储存保证了数据访问不会与指针访问形成冲突不命中



# 缓存不命中的种类

* 强制性不命中(compulsory miss) (又叫做冷不命中(cold miss))

  若是一个缓存一开始是空的，则刚开始对数据的访问都是不命中的

* 容量不命中(capacity miss)

  当访问一块连续的数据(称为工作集)时，若是缓存的容量比工作集要小，则无法一次性把数据全部存入缓存，即容量不命中

* 冲突不命中

  多个对象映射到同一个缓存块中，缓存会不命中

* (连贯性Coherence)

  有多个CPU 共用 Memory，每个CPU都有一个对应的 cache。而其中的数据不一致

# 2：1 Cache Rule

miss rate 1-way associative cache size X
= miss rate 2-way associative cache size X/2





# 1.组数的选定

增加组数可以减少冲突不命中，但是会增加在组内并行搜索的时间(增加 $T_{hit}$ )和构造电路的成本

构造一个又大又快的相联高速缓存很困难且很昂贵，所以一般全相联高速缓存只适合做小的高速缓存，过大的高速缓存的组数不能一味的追求大

# 2.块大小的选定

当块变大时，不命中率先减小后增大(在缓存总容量不变的前提下)

一开始不命中率减小：块变大，减少了容量不命中(空间局部性利用变多)

后来不命中率增大：块变大意味着行数(块数)减少，增加了冲突不命中的可能(时间局部性利用变少)