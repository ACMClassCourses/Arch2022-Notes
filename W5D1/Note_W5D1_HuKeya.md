# Week 5 Day 1 Note By Hu Keya

### Memory Hierarchy

1. Register Cache / Memory / Disk
2. Memory Technology
3. Interface 
4. Timing

### Register Cache / Memory / Disk

<img src="http://computerscience.gcse.guru/wp-content/uploads/2016/04/Von-Neumann-Architecture-Diagram.jpg" alt="Von Neumann Architecture - Computer Science GCSE GURU" style="zoom:67%;" />

By Von Neumann Structure we know that 

- codes and data are all stored in memory Unit 
- only CPU can visit memory unit.

### Memory Technology

How to make a memory device?

- #### Electric Way:

  - During 30-50s
  - ms level
  - Using relay to implement self-locking

- #### Electronic Way:

  - $\mu s$ $ns$ level

  - During 70s: Using Logic Gates to implement latch and trigger such as R-S. 

    <img src="https://sub.allaboutcircuits.com/images/04173.png" alt="The S-R Latch | Multivibrators | Electronics Textbook" style="zoom:90%;" />

  - During 80s~ : Using Capacitor, a dynamic way, such as DRAM

### Interface

Suppose that we have a chip with 1-bit width and $2^{10}$ length, we want to construct a memory of 8-bit width and $2^{16}$ length

- make eight of chip in a row, that we get a module of 8-bit width and  $2^{10}$ length
- that make 64 of the module in a line, finally we get the memory.

We have address $A [ 15: 0 ]$ for interface. 

- First we use $A [15:10]$ to determine which module ( from module 0 to module 63)
- Then we use $A[9:0]$ to determine which chip to go ( from chip 0 to chip 7)

### DRAM Read Timing

For larger Memory there will be too many address wires, resulting in too many 

chip pins to place on the chip. To solve the problem, we transmit the address twice by column address and row address.

**The process  is as follows.**

<img src="https://ts1.cn.mm.bing.net/th/id/R-C.de1e0979fc4f039f22a5579f887dd04f?rik=p8S6kEQXrG%2f1rA&riu=http%3a%2f%2fimage.slideserve.com%2f210382%2fdram-read-timing-l.jpg&ehk=Hxe3LqNsi2lsgzbMjyolNSetXOwa%2bI67RR0%2f5dz4zzg%3d&risl=&pid=ImgRaw&r=0" alt="DRAM" style="zoom:50%;" />

- CAS_L: Column Address Select

- A: Address

- WE_L: Write Enable

- OE_L: Output Enable

- D: Data

**Some Interpretation of process:**

- Junk: Uncertain signal

- High Z: high-impedance state with no signal

- _L: Low level works

**Reasons for asynchrony:**  

- Different signals sent should be given sufficient time to arrive.
- Sufficient delay is required to detect capacitance levels





