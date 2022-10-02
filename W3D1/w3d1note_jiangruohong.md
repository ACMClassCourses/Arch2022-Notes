## Solutions to Hazards
Hazards prevent next instruction from executing during its designated clock cycle
### Structural hazards
Hardware cannot support this combination of instructions (single person to fold and put clothes away)

Solution: Copy/Duplicating FUs
### Data hazards
Instruction depends on result of prior instruction still in the pipeline.

WAR/WAW: pseudo data hazards, can be solved by renaming.

RAW (true hazard) solutions:
- Apply forwarding to avoid data hazard
- Change hardware for forwarding
- With forwarding, read after load still cause hazard, add bubble.
- Software Scheduling: compiler changes the order of instructions, can avoid "read after load" situation, increase speed.
### Control hazards
Caused by delay between the fetching of instructions and decisions about changes in control flow (branches and jumps).

- Stall until branch direction is clear: for every branch instruction, stall 3 cycles. Significantly slower if 30% instructions are branch.
- Predict Branch Not Taken
- Predict Branch Taken
- Delayed Branch
Define branch to take place after instructions in its "delay slot". The delay slot is filled by possible instructions in the basic block (doesn't contain any branch instruction) before it. Because basic blocks' size are often small, about 60% of the delay slots can be filled.  
For example, loop unwinding increases the number of instructions in a loop, optimizing by making the size of basic block larger.