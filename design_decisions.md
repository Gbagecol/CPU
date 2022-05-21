# PROJECT DESIGN DECISIONS

This is a record of the decisions I make throughout this project pertaining to the design of the different parts of the
CPU and language stack.

## CPU
------

- Bit Shift: The inclusion of logical shift left/right instructions is necessary for efficient integer multiplication. 
  I decided to only allow the CPU to shift left or right one bit at a time for two reasons. One, to avoid having to
  implement a barrel shifter in the hardware, and two, to avoid having to use a MIPS-like shmt in the corresponding
  instructions. This frees up space in the opcode to include an additional register.