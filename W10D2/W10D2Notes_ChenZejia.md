## W10D2 notes

**written by Chen Zejia.**

### Async/Sync

* Sync: All components of the system work together in the same frame of reference. The frame of reference can be time or space. It's easier and clearer to design.
* Async: It usually don't have a common frame of reference.

### Interruption(I/O)

* Interruption: External devices interrupts CPU. The information is collected by an IC and IC transmits the information to the CPU. CPU can access the specific information through the bus.
* Daisy Chain: The devices are linearly arranged and core is the first. When multiple requests are sent, the request closest to the core was responded first.

### Internet

* Use supercube to increase the dimension and decrease the distance.
* ATM/ISDN(Euro)
  * ATM: Async Transfer Mode. Build virtual circuits for transmitting data when needed. All the lines are shared.
* TCP/IP(USA)
  * Data is divided into multiple slices for transmission.

Both ATM/ISDN and TCP/IP are asynchronous.

* SNMP: Simple Network Management Protocol, it's used to get the information of each node.
* OSPF: Open Shortest Path First, it can maintain a topology map of the network and find the best path between two nodes.
* DNS: Map url to IP, DNS is the largest database.

### FHSS

* FHSS: Frequency-hopping spread spectrum. Constantly changing the carrier frequency while transmitting data and split data into carrier of different frequencies.

### CDMA

* CDMA: Code-division multiple access. The transmission information is combined through the orthogonal carrier. Use the corresponding decoder to get the information when querying. This method is similar to the Fourier transform.

