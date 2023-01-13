# Hazards

## Structure Hazard
CPU does not provide support for instructions of this type.

Fix:More ALU/FU or adjust the structure of the CPU

## Data Hazard
Current instruction's execution depends on the result of other instructions,which have not been commited yet. 

Hazard Type
* WAR: Psuedo Hazard. Could be solved by renaming.

* RAR: Not a problem at all

* WAW: Psuedo Hazard. Could be solved by renaming.

* RAW: Use the technique "forwarding" to solve the hazard

Note: RAW can also be eased by software(compiler) scheduling.

## Control Hazard
Control Hazard happens when CPU cannot decide whether to jump on a conditional brunch instruction, as the condition haven't been calculated yet.

Fix:
* just stuck
* predict whether the brunch will be taken or not and jump immediately.If the predition was wrong,roll back and clear all the instruction in queue.
