# Lecture Notes W02 D2

###### Yichao Zhong



### Review: How 5-staged Pipeline works

- Von Neumann's structure

- uses **Muxplexers**

  

# Topic: Hazard in Pipeline & Solutions

#### instructions catagories:

- arithmetic/logic: +, -, AND...
- data transfer: MOV, LD, ST...
- control: JUMP, CALL, RET...

sign extend (offline class)

between stage: inter-mediate reg, or transfer reg

## Hazards

- Structural hazards: HW cannot support this combination of instructions (single person to fold and put clothes away)  (exclusive sharing)
- Data hazards: Instruction depends on result of prior instruction still in the pipeline (missing sock)  
- Control hazards: Caused by delay between the fetching of instructions and decisions about changes in control flow (branches and jumps).  

General solution: STALL(BUBBLE)

### Data Hazard

- data dependence: RAW

```
//data hazard
add r1,r2,r3
sub r4,r1,r3
and r6,r1,r7
or  r8,r1,r9
// no data hazard
xor r10,r1,r11
```

- data anti-dependence: WAR

```
sub r4,r1,r3 //it reads r1 later
add r1,r2,r3 //it writes r1 earlier
mul r6,r1,r7
```

renaming can solve it.

- output dependence

```
sub r1,r4,r3
add r1,r2,r3
mul r6,r1,r7
//will see in Tomasulo.
```

#### Solution: Forwarding

……

### Structural Hazard

（if memory build the structural hazard, the solution shall be I-cache+D-cache;）(Harvard Structure by Aiken)