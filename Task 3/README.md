**RISC-V Instruction Analysis**<br>
This repository focuses on analyzing and decoding 15 distinct RISC-V instructions extracted from application code.
Each instruction is categorized based on its type (R, I, S, B, U, J) and represented by its 32-bit binary encoding.

**Overview**<br>
The primary objectives of this project are to:
Explore the various RISC-V instruction types: R, I, S, B, U, and J.
Extract and classify 15 unique RISC-V instructions from the riscv-objdump output of the application code.
Decode these instructions into their corresponding 32-bit binary representations.<br>

**1. auipc gp, 0x13**
opcode: 0010111 (7 bits)

immediate (imm): 0x13 = 0000 0000 0001 0011 (20 bits)

destination register (rd): gp (3, 5 bits) = 00011

32-bit Code: 0000 0000 0001 0011 | 00011 | 0010111<br>

**2. addi gp, gp, 0**

opcode: 0010011 (7 bits)

immediate (imm): 0 = 0000 0000 0000 (12 bits)

source register (rs1): gp (3, 5 bits) = 00011

destination register (rd): gp (3, 5 bits) = 00011

func3: 000 (3 bits)

32-bit Code: 0000 0000 0000 | 00011 | 000 | 00011 | 0010011<br>

**3. sd ra, 8(sp)**

opcode: 0100011 (7 bits)

immediate (imm): 8 = 0000 0000 1000 (12 bits split as imm[11:5] and imm[4:0])

imm[11:5]: 0000 000

imm[4:0]: 01000

source register (rs2): ra (1, 5 bits) = 00001

base register (rs1): sp (2, 5 bits) = 00010

func3: 011 (3 bits)

32-bit Code: 0000 000 | 00001 | 00010 | 011 | 01000 | 0100011<br>

**4.addi sp, sp, -16**

opcode: 0010011 (7 bits)

immediate (imm): -16 = 1111 1111 1111 0000 (12 bits)

source register (rs1): sp (2, 5 bits) = 00010

destination register (rd): sp (2, 5 bits) = 00010

func3: 000 (3 bits)

32-bit Code: 1111 1111 1111 0000 | 00010 | 000 | 00010 | 0010011<br>

**5.add s0, a5, s0**

opcode: 0110011 (7 bits)

func7: 0000000 (7 bits)

source register 2 (rs2): s0 (8, 5 bits) = 01000

source register 1 (rs1): a5 (15, 5 bits) = 01111

destination register (rd): s0 (8, 5 bits) = 01000

func3: 000 (3 bits)

32-bit Code: 0000000 | 01000 | 01111 | 000 | 01000 | 0110011<br>

**6.lui a5, 0x2**

opcode: 0110111 (7 bits)

immediate (imm): 0x2 = 0000 0000 0000 0010 (20 bits)

destination register (rd): a5 (15, 5 bits) = 01111

32-bit Code: 0000 0000 0000 0010 | 01111 | 0110111<br>

**7.jal ra,**

opcode: 1101111 (7 bits)

immediate (imm): <address> (20 bits, needs to be calculated based on PC-relative offset)

destination register (rd): ra (1, 5 bits) = 00001

32-bit Code: <imm[20]> | <imm[10:1]> | <imm[11]> | <imm[19:12]> | 00001 | 1101111<br>

**8.li a5, 1**

opcode: 0010011 (7 bits)

immediate (imm): 1 = 0000 0000 0000 0001 (12 bits)

source register (rs1): x0 (0, 5 bits) = 00000

destination register (rd): a5 (15, 5 bits) = 01111

func3: 000 (3 bits)

32-bit Code: 0000 0000 0000 0001 | 00000 | 000 | 01111 | 0010011<br>

**9.jalr zero, 0(ra)**

opcode: 1100111 (7 bits)

immediate (imm): 0 = 0000 0000 0000 (12 bits)

source register (rs1): ra (1, 5 bits) = 00001

destination register (rd): zero (0, 5 bits) = 00000

func3: 000 (3 bits)

32-bit Code: 0000 0000 0000 | 00001 | 000 | 00000 | 1100111<br>

**10. beqz a5,**

opcode: 1100011 (7 bits)

immediate (imm): <offset> (12 bits split as imm[12|10:5|4:1|11])

imm[12]: <offset>[12]

imm[10:5]: <offset>[10:5]

imm[4:1]: <offset>[4:1]

imm[11]: <offset>[11]

source register (rs1): a5 (15, 5 bits) = 01111

source register (rs2): x0 (0, 5 bits) = 00000

func3: 000 (3 bits)

32-bit Code: <imm[12]> | <imm[10:5]> | 01111 | 00000 | 000 | <imm[4:1]> | <imm[11]> | 1100011<br>
