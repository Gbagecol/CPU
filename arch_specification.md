# CPU ARCHITECTURE SPECIFICATION

This CPU is designed to have a RISC format. It is a 16 bit architecture with no floating-point capabilities in
hardware.


## Instruction Set
------------------

All instructions for this instruction set are 16 bits. There are two different instruction types: I-type,
and R-type.

### I-Type Instructions

I-type instructions are instructions that use unsigned 8-bit immediates. The format of an I-type instruction is:

**ooooo rrr iiiiiiii**
- o: The instruction opcode.
- r: A register id.
- i: An unsigned 8-bit immediate value.

### R-Type Instructions

R-type instructions are instructions that use two registers, a source resister and a destination register. The format
of an R-type instruction is:

**ooooo ddd rrr ssss u**
- o: The instruction opcode.
- r: A register id, usually the source for a value.
- d: A register id, usually the destination for a value.
- s: Shift amount.
- u: Unused.

### Instruction List

| Instruction | Type | Description | Assembly | Opcode |
| ----------- | ---- | ----------- | -------- | ------ |
| Add Register | R | Add registers A and B, store the result in A. | add $a $b | 0x0 / 0b0 |
| Sub Register | R | Subtract register B from register A, store the result in A. | sub $a $b | 0x1 / 0b1 |
| Shift Register Left | R | Shift the value of register B left by n bits, store the result in A. | shl $a $b n | 0x2 / 0b10 |
| Shift Register Right | R | Shift the value of register B right by n bits, store the result in A. | shr $a $b n | 0x3 / 0b11 |
| And Register | R | Logical AND A and B together, store the result in A. | and $a $b | 0x4 / 0b100 |
| Or Register | R | Logical OR A and B together, store the result in A. | or $a $b | 0x4 / 0b100 |
| Load Word | R | Loads the value at the memory address in register B into register A. | lw $a $b | 0x6 / 0b110 |
| Store Word | R | Stores the value in register A into the address in register B. | sw $a $b | 0x7 / 0b111 |
| Move Register | R | Stores the value in register B in register A. | mov $a $b | 0x8 / 0b1000 |
| Jump If Equal | R | Jumps to the address in register A if the value in register B equals 0. | jeq $a $b | 0x9 / 0b1001 |
| Jump If Less Than | R | Jumps to the address in register A if the value in register B is less than 0. | jlt $a $b | 0xA / 0b1010 |
| Jump If Greater Than | R | Jumps to the address in register A if the value in register B is greater than 0. | jgt $a $b | 0xB / 0b1011 |
| Add Immediate | I | Add the immediate value n to register A. | addi $a n | 0x10 / 0b10000 |
| Sub Immediate | I | Subtract the immediate value n from register A. | subi $a n | 0x11 / 0b10001 |
| And Immediate | I | Logical AND A and the immediate value n together, store the result in A. | andi $a n | 0x12 / 0b10010 |
| Or Immediate | I | Logical OR A and the immediate value n together, store the result in A. | ori $ a n | 0x13 / 0b10011 |
| Jump | I | Jumps unconditionally to the address in register A plus an optional immediate offset n. | jmp $a [n] | 0x14 / 0b10100 |


## ALU
------

The ALU uses 2's complement arithmetic. Internally, the ALU can do addition or shift operations.The ALU will also
output status bits for a negative result, a result equal to 0, and a carry bit.