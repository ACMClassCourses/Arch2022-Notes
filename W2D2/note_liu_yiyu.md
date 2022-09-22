# Note for W2D2

*Authored by Liu Yi-Yu*

## More Details about MIPS 5-steps Datapath

### Signed Extension

A typical implementation of signed extension is to link all upper bits
with the wire on the top bit of input. With that designed, the circuit
works pretty good whenever the input is positive or negative.

### Data Stationary Control

To make the CPU work as a pipeline, we should seperate each part of the
pipeline.  If we do not seperate them, the next instruction may affect
the previous one and cause the result to be incorrect.

## Hazards

Limit to pipeline: Hazards prevent next instruction from executing during
its designated clock cycle.

### Structural Hazard

If several parts access a certain part at the same time, anything unexpected
may happen.  A typical solution to it is to use bubble and stop the
instruction that is fetched later. (If we choose to stop the previous one,
that instruction may not eventually be executed.)

### Data Hazards

Generally, data hazard happens when the instruction depends on the result of
previous instruction.

#### Read after Write (RAW)

The date is read after the data been written.  If the data haven't been
stored back in registers, the data read afterwards will be wrong.

An example is

```
add r1, r2, r3
sub r4, r1, r3
```

#### Write after Read (WAR)

The instruction of writing is after the instruction of reading.  However,
the data is acutally written after being read.  In MIPS, this case will
simply not happen because reads are always in stage 2, which is previous to writes in stage 5.

If the instruction is executed out of order, this will cause a problem.

#### Write after Write (WAW)

Instruction writez operand brefore the previous instruction writes it.

This case is the same as the WAR case.  In MIPS 5 stage pipeline, it simply
won't happen, because all instruction takes 5 stage and writes are always
in satage 5.

If the instruction is executed out of order, this will cause a problem.

#### Solution

- Renaming
- Forwarding: put the data to be written into the data to be read
