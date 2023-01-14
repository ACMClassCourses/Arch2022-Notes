## Out-of-order Execution
### History
1960s: Vector(or Array) vs Superscalar vs Pipeline+OoO  
Scoreboarding(Thorton 1964) vs Tomasulo(IBM 1965)
### How to WAR/WAW
~~Scoreboarding~~  
RAW: distance: forwarding/code movement  

WAW/WAR(pseudo): renaming(tomasulo)  
**Reservation Station**  
- Op: operation in the unit
- Vj, Vk: Value of source operands 
- Qj,Qk: id of reservation stations producing source registers (0 means value is ready)

### Challenges
- branch
- exception
- process context switching(multiprocess OS)

### Precise Interrupt
Tomasulo: In-order issue, out-of-order execution, and out-of-order completion  
"fix" the out-of-order completion  

Reorder Buffer(ROB): all instructions commit in order  
- Use ROB number instead of RS when execution completes
- supplies operands between execution complete & commit
- inst commit, when inst commits, put result into register

easy to undo speculated inst/mispredicted branches/exceptions