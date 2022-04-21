# CPU ARCHITECTURE SPECIFICATION

This CPU is designed to have a RISC format. It is a 16 bit architecture with no floating-point capabilities in
hardware.

## Instruction Set

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

**ooooo rrr ddd ssss u**
- o: The instruction opcode.
- r: The source register id.
- d: The destination register id.
- s: Shift amount.
- u: Unused.