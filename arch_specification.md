# CPU ARCHITECTURE SPECIFICATION

This CPU is designed to have a RISC format. It is a 16 bit architecture with no floating-point capabilities in
hardware.


## Instruction Set
------------------

All instructions for this instruction set are 16 bits. There are two different instruction types: I-type,
and R-type.

### I-Type Instructions

I-type (Immediate-type) instructions are instructions that use unsigned 8-bit immediates. The format of an I-type
instruction is:

**ooooo rrr iiiiiiii**
- o: The instruction opcode.
- r: A register id.
- i: An unsigned 8-bit immediate value.

### R-Type Instructions

R-type (Register-type) instructions are instructions that use only two registers. These are either jumps, shifts, or
unary operations. The format of an R-type instruction is:

**ooooo aaa bbb s uuu 1**
- o: The instruction opcode.
- a: A register id.
- b: Another register id.
- s: A single bit, 0 for shift left, 1 for shift right. (Unused otherwise.)
- u: Unused.

### O-Type Instructions

O-type (Operand-type) instructions are instructions that use three registers, two source registers that some binary
operation is applied to, and a destination register. The format of an O-type instruction is:

**ooooo aaa bbb ccc u 0**
- o: The instruction opcode.
- a: A register id, usually the destination for the resulting value.
- b: A register id, usually the left hand side of an expression.
- c: A register id, usually the right hand side of an expression.
- u: Unused.

### Instruction List

| Instruction | Type | Description | Assembly | Opcode |
| ----------- | ---- | ----------- | -------- | ------ |
| Load Immediate | I | Load the 8 bit immediate value *n* into register *A*. | ldi $A n | 0 |
| Store Immediate | I | Store the 8 bit immediate value *n* into the address in register *A*. | sti $A n | 1 |
| Add Immediate | I | Add the immediate value *n* to register *A*. | adi $A n | 2 |
| Subtract Immediate | I | Subtract the immediate value *n* from register *A*. | sbi $A n | 3 |
| And Immediate | I | Logical AND the immediate value *n* with register *A*. | ani $A n | 4 |
| Or Immediate | I | Logical OR the immediate value *n* with register *A*. | ori $A n | 5 |
| Not Immediate | I | Logical NOT the immediate value *n* and store the result in register *A*. | nti $A n | 6 |
| Jump | I | Jump unconditionally to the address in register *A* plus an optional immediate offset *n*. | jmp $A [n] | 7 |
| Load Word | R | Loads the value at the address in register *B* into register *A*. | ldr $A $B | 16 |
| Store Word | R | Store the value in register *B* into the address in register *A*. | str $A $B | 17 |
| Shift Left | R | Shift the value in register *B* left one bit and store the result in register *A*. | shl $A $B | 18 |
| Shift Right | R | Shift the value in register *B* right one bit and store the result in register *A*. | shr $A $B | 19 |
| Not Register | R | Logical NOT the value in register *B* and store the result in register *A*. | not $A $B | 20 |
| Move Register | R | Copy the value in register *B* into register *A*. | mov $A $B | 21 |
| Add Register | O | Add registers *B* and *C*, store the result in register *A*. | add $A $B $C | 22 |
| Subtract Register | O | Subtract register *C* from register *B*, store the result in register *A*. | sub $A $B $C | 23 |
| And Register | O | Logical AND registers *B* and *C*, store the result in register *A*. | and $A $B $C | 24 |
| Or Register | O | Logical OR registers *B* and *C*, store the result in register *A*. | lor $A $B $C | 25 |
| Jump if Equal | O | Jump to the address in register *A* if the values in registers *B* and *C* are equal. | jeq $A $B $C | 26 |
| Jump if Less Than | O | Jump to the address in register *A* if the value in register *B* is less than the value in register *C*. | jlt $A $B $C | 27 |
| Jump If Greater Than | O | Jump to the address in register *A* if the value in register *B* is greater than the value in register *C*. | jgt $A $B $C | 28 |
| Jump If Not Equal | O | Jump to the address in register *A* if the values in registers *B* and *C* are not equal. | jne $A $B $C | 29 |

### Pseudo Instructions

These are instructions that do not directly correspond to single 16-bit machine instructions, but can still be used in
assembly as macros to replace common routines that take multiple instructions.

| Instruction | Description | Assembly |
| ----------- | ----------- | -------- |
| Shift Left N | Shift the value in register *B* left by *n* bits and store the result in register *A* (*n* <= 15). | srn $A $B n |
| Shift Right N | Shift the value in register *B* right by *n* bits and store the result in register *A* (*n* <= 15). | sln $A $B n |


## ALU
------

The ALU uses 2's complement arithmetic. Internally, the ALU can do addition or shift operations.The ALU will also
output status bits for a negative result, a result equal to 0, and a carry bit.