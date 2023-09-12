# Note W7D1

## Cache

target: reduce $AMAT=T_{nit}+\eta\times T_{penalty}$

- miss reduction: 3Cs (cache size unchanged)
  - **Compulsory**
  - **Capacity**
  - **Conflict**

- miss reduction measures
  - change block size
  - victim cache
  - pseudo-associativity
  - Hardware prefetching (instructions)
    - extra blocks placed in **stream buffer **(has similar data structure with victim cache/write-buffer)
  - Software prefetching (data)
  - Compiler Optimization

### How to optimize Compiler?

- Merging Arrays

  <font color=green>the concept of `struct`</font>

  ```c++
  //before: 2 arrays
  int val[N];
  int key[N];
  /*query sequence:
  |1|
  |3|
  |5|
  |7|
  
  |2|
  |4|
  |6|
  |8|
  Crossing queries increases miss rate 
  */
  
  
  //After:1 array
  struct merge {
  	int val;
  	int key;
  }
  struct merge merged_array[N];
  /*query sequence:
  |1 2|
  |3 4|
  |5 6|
  |7 8|
  match with the common usage of key-val relations
  */
  ```

- Loop Interchange

  ```C++
  for(int i=0;i<5000;i++){
  	for(int j=0;j<100;j++){
  		//balabala
  	}
  }
  //->
  for(int j=0;j<100;i++){
  	for(int i=0;i<5000;j++){
  		//balabala
  	}
  }
  
  ```

- Loop Fusion

  ```C++
  for(int i=0;i<n;i++){
   //balabala1
  }
  for(int i=0;i<n;i++){
   //balabala2
  }
  //->
  for(int i=0;i<n;i++){
   //balabala1
   //balabala2
  }
  ```

- Blocking（used in Matrix Multiply）

  - don't waste unused bytes in the block read from mem

  - compute on 1 element -> compute on `size(block)`x`size(block)`submatrix.

  - once read a block, **use it until it won't be used after.**

    ```C++
    /* Before */
    for (i = 0; i < N; i = i+1)
    for (j = 0; j < N; j = j+1)
    {r = 0;
    for (k = 0; k < N; k = k+1){
    r = r + y[i][k]*z[k][j];};
    x[i][j] = r;
    };
    
    /* After */
    for (jj = 0; jj < N; jj = jj+B)
    for (kk = 0; kk < N; kk = kk+B)
    for (i = 0; i < N; i = i+1)
    for (j = jj; j < min(jj+B-1,N); j = j+1){
        r = 0;
    	for (k = kk; k < min(kk+B-1,N); k = k+1) {
    		r = r + y[i][k]*z[k][j];
    	}
    	x[i][j] = x[i][j] + r;
    }
    
    ```

