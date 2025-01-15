# Samsung RISC-V Project
"Repository for RISC-V related projects and experiments under Samsung's ecosystem."

# Task 1-
C Language and RISC-V Based Compilation Lab

This repository contains the tasks and steps related to compiling C code using both GCC (GNU Compiler Collection) and RISC-V GCC compiler. It involves writing C code to calculate the sum of numbers from 1 to N and compiling the code using both traditional GCC and the RISC-V GCC compiler.

# C Language-based Compilation

In this part, we work with C code on a local system using the GCC compiler to compile and execute a simple program that prints the sum of numbers from 1 to N.

Steps:
1.	Open the terminal and navigate to the directory to create your file.
2.	Create and write your C code:
	
              	vi sum1ton.c
  	
This will open the vi editor. Write the C code in the editor to calculate the sum of numbers. Save and close the editor using:

               >	Ctrl + S to save.
               
               >	Ctrl + W to close.
3.	Compile the C code using GCC: In the terminal, run the following command:

               gcc sum1ton.c
  	
4.	Run the compiled code: After compilation, execute the generated binary using:
   
               ./a.out

# RISC-V Based Compilation

In this part, we perform the same task, but this time using the RISC-V GCC compiler to compile and generate assembly code for the program.

Steps:
1.	View the C code using cat: Open the terminal and run:
	
               cat sum1ton.c
  	
This will display the entire C code on the terminal.

2.	Compile the C code using the RISC-V GCC compiler: Run the following command to compile the code:
               
	       riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum_1ton.o sum_1ton.c
  	
The flags used here:

>	-O1: Applies basic optimizations to reduce execution time and code size.

>	-mabi=lp64: Specifies the 64-bit ABI (Application Binary Interface) for the RISC-V architecture.

>	-march=rv64i: Specifies the RISC-V 64-bit integer instruction set.

>	-o sum_1ton.o: Specifies the output file name.

3.	Disassemble the object file to view the assembly code: Open a new terminal and run:

               riscv64-unknown-elf-objdump -d sum_1ton.o

This will display the assembly code generated from the C source code. To locate the main section of the code, type /main in the terminal.

Keywords and Compiler Options Used

>	-mabi=lp64: Specifies the 64-bit Application Binary Interface (ABI), which is used for 64-bit integer, long, and pointer sizes.

>	-march=rv64i: Defines the target architecture as a 64-bit RISC-V base integer instruction set (RV64I).

>	riscv64-unknown-elf-gcc: The RISC-V GCC compiler used for compiling RISC-V code.

>	riscv64-unknown-elf-objdump: A tool for disassembling RISC-V binaries, allowing you to inspect the assembly code.

>	-Ofast: A compiler optimization flag to maximize the speed of the generated code.

>	-O1: A level of optimization that balances between speed and compilation time. It reduces code size and execution time without increasing compilation time significantly.

Notes on Compiler Optimizations:

•	Optimization Levels:

>	-O0: No optimization (default).

>	-O1: Basic optimization to improve code speed and size.

>	-O2: More aggressive optimization that may take longer to compile but provides faster or smaller code.

>	-O3: Maximizes optimization with additional code transformations, potentially increasing compilation time.

>	-Os: Optimizes code size and reduces memory usage, often used for embedded systems.

•	-Ofast Optimization: The -Ofast flag optimizes the generated code for the maximum speed, which may sometimes lead to non-standard behaviour. It is suitable for applications where execution speed is more critical than strict compliance with standards.




# Task 2-
Performing SPIKE Simulation and Debugging the C code with Interactive Debugging Mode using Spike

# What is SPIKE in RISCV?

A RISC-V ISA is a simulator, enabling the testing and analysis of RISC-V programs without the need for actual hardware.
Spike is a free, open-source C++ simulator for the RISC-V ISA that models a RISC-V core and cache system. It can be used to run programs and a Linux kernel, and can be a starting point for running software on a RISC-V target.


# What is pk (Proxy Kernel)?

The RISC-V Proxy Kernel, pk , is a lightweight application execution environment that can host statically-linked RISC-V ELF binaries.
A Proxy Kernel in the RISC-V ecosystem simplifies the interaction between complex hardware and the software running on it, making it easier to manage, test, and develop software and hardware projects.

Testing the SPIKE Simulator

The target is to run the sum1ton.c code using both gcc compiler and riscv compiler, and both of the compiler must display the same output on the terminal. So to compile the code using gcc compiler, use the following command:

               gcc sum1ton.c  

               ./a.out


And to compile the code using riscv compiler, use the following command:

               spike pk sum1ton.o

Debugging the Assembly Language Program of sum1ton.c
Open the Objdump of code by using the following command

               riscv64-unknown-elf-objdump -d sum1ton.o | less  
Open the debugger in another terminal by using the following command
 
              spike -d pk sum1ton.o
The debugger will be opened in the terminal.


# Task 3-
Identifying RISC-V instructions

# WHAT IS RISC-V?

RISC-V is an open-source instruction set architecture (ISA) that allows developers to develop processors for specific applications.

RISC-V is based on reduced instruction set computer principles and is the fifth generation of processors built on this concept.

RISC-V can also be understood as an alternative processor technology which is free and open, meaning that it does not require you to purchase the license of RISC-V to use it.

# INSTRUCTIONS FORMAT IN RISC-V

The instructions format of a processor is the way in which machine language instructions are structured and organized for a processor to execute. It is made up of series of 0s and 1s, each containing information about the location and operation of data.

There are 6 instruction formats in RISC-V:

# R-format
# I-format
# S-format
# B-format
# U-format
# J-format

RISCV Instruction Types

Let’s discuss each of the instruction formats in detail with examples.


# 1. R-type Instruction
In RV32, each instruction is of size 32 bits. In R-type instruction, R stands for register which means that operations are carried on the Registers and not on memory location. This instruction type is used to execute various arithmetic and logical operations. The entire 32 bits instruction is divided into 6 fields as shown below.

# R-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

The next subfield is known as rd field which is referred as Destination Register. The rd field is of length 5 bits and is used to store the final result of operation.

The next subfield is func3 also referred as function 3. Here the ‘3’ represents the size of this field. This field tells the detail about the operation, i.e., the type of arithmetic and logical that is performed.

The next two subfields are the source registers, rs1 and rs2 each of length 5 bits. These are mainly used to store and manipulate the data during the execution of instructions.

The last subfield is func7 also referred as function 7. Here ‘7’ represents the size of the field. The function of func7 field is same as that of func3 field.


# 2. I-type Instruction
In RV32, each instruction is of size 32 bits. In I-type instruction, I stand for immediate which means that operations use Registers and Immediate value for their execution and are not related with memory location. This instruction type is used in immediate and load operations. The entire 32 bits instruction is divided into 5 fields as shown below.

# I-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

The next subfield is known as rd field which is referred as Destination Register. The rd field is of length 5 bits and is used to store the final result of operation.

The next subfield is func3 also referred as function 3. Here the ‘3’ represents the size of this field. This field tells the detail about the operation, i.e., the type of arithmetic and logical that is performed.

The next subfield is the source registers, rs1 of length 5 bits. It is mainly used to store and manipulate the data during the execution of instructions.

The only difference between R-type and I-type is rs2 and func7 field of R-type has been replaced by 12-bits signed immediate, imm[11:0].


# 3. S-type Instruction
In RV32, each instruction is of size 32 bits. In S-type instruction, S stand for store which means it is store type instruction that helps to store the value of register into the memory. Mainly, this instruction type is used for store operations. The entire 32 bits instruction is divided into 6 fields as shown below.

# S-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

S-type instructions encode a 12-bit signed immediate, with the top seven bits imm[11:5] in bits [31:25] of the instruction and the lower five bits imm[4:0] in bits [11:7] of the instruction.

S-type instruction doesn’t have rd fields which states that these instructions are not used to write value to a register, but to write/store a value to a memory.

The value to be stored is defined in rs1 field and address to which we have to store this value is calculated using rs1 and immediate field. The width of the operation and types of instruction is defined by func3, it can be a word, half-word or byte.


# 4. B-type Instruction
In RV32, each instruction is of size 32 bits. In B-type instruction, B stand for branching which means it is mainly used for branching based on certain conditions. The entire 32 bits instruction is divided into 8 fields as shown below.

# B-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

B-type instructions encode a 12-bit signed immediate, with the most significant bit imm[12] in bit [31] of the instruction, six bits imm[10:5] in bits [25:30] of the instruction, four bits imm[4:1] in bits [11:8] and one bit imm[11] on bit[7].

There are two source registers rs1 and rs2 on which various operations are performed based on certain conditions, and those conditions are defined by func3 field.

After performing operations on the source register based on the conditions, it is evaluated that if the condition is true, Program Counter value gets updated by PC = Present PC Value + Immediate Value, and if the condition is false then PC will be given as PC = Present PC value + 4 bytes, which states that PC will move to next instruction set.

RV32 instructions are word-aligned, which means that address is always defined in the multiple of 4 bytes.


# 5. U-type Instruction
In RV32, each instruction is of size 32 bits. In U-type instruction, U stand for Upper Immediate instructions which means it is simply used to transfer the immediate data into the destination register. The entire 32 bits instruction is divided into 3 fields as shown below.

# U-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

The U-type instruction only consists of two instructions, i.e., LUI and AUIPC.

For Example, lets take the instruction lui rd, imm and understand this instruction. lui x15, 0x13579 : This instruction will be executed and the immediate value 0x13579 will be written in the MSB of the rd x15, and it will look like x15 = 0x13579000.


# 6. J-type Instruction
In RV32, each instruction is of size 32 bits. In U-type instruction, J stand for jump, which means that this instruction format is used to implement jump type instruction. The entire 32 bits instruction is divided into 6 fields as shown below.

# J-type

The first field in the instruction format is known as opcode, also referred as operation code. The opcode is of length 7 bits and is used to determine the type of instruction format.

The J-type instruction only consists of single instruction, JAL.

J-type instruction encode 20 bits signed immediate which is divided into four fields.

The J-type instructions are often used to perform jump to the desired memory location. The address of the desired memory location is defined in the instruction. These instructions are also used to implement loops.


Now, let's analyse each instruction given to us one by one

# ADD r6, r2, r1  

              All the arithmetic and logical operations are performed using R-type instruction format, hence this instruction belongs to R-type instruction set.r6 is the destination register that will hold the sum of values stored in the register r2 and r1.

                    Opcode for ADD = 0110011
                    rd = r6 = 00110
                    rs1 = r2 = 00010
                    rs2 = r1 = 00001
                    func3 = 000
                    func7 = 0000000

32 bits instruction : 
   0000000_00001_00010_000_00110_0110011

# SUB r7, r1, r2

             All the arithmetic and logical operations are performed using R-type instruction format, hence this instruction belongs to R-type instruction set.r7 is the destination register that will hold the difference of values stored in the register r1 and r2.

                    Opcode for SUB = 0110011
                    rd = r7 = 00111
                    rs1 = r1 = 00001
                    rs2 = r2 = 00010
                    func3 = 000
                    func7 = 0100000

32 bits instruction : 
   0100000_00010_00001_000_00111_0110011

# AND r8, r1, r3

             All the arithmetic and logical operations are performed using R-type instruction format, hence this instruction belongs to R-type instruction set.r8 is the destination register that will hold the value of r1 & r3, means performing AND operation bit by bit.

                   Opcode for AND = 0110011
                   rd = r8 = 01000
                   rs1 = r1 = 00001
                   rs2 = r3 = 00011
                   func3 = 111
                   func7 = 0000000

32 bits instruction :
   0000000_00011_00001_111_01000_0110011

# OR r9, r2, r5

                   All the arithmetic and logical operations are performed using R-type instruction format, hence this instruction belongs to R-type instruction set.r9 is the destination register that will hold the value of r2 | r5, means performing OR operation bit by bit.

                           Opcode for OR = 0110011
                           rd = r9 = 01001
                           rs1 = r2 = 00010
                           rs2 = r5 = 00101
                           func3 = 110
                           func7 = 0000000

32 bits instruction :  
   0000000_00101_00010_110_01001_0110011

# XOR r10, r1, r4

                   All the arithmetic and logical operations are performed using R-type instruction format, hence this instruction belongs to R-type instruction set.r10 is the destination register that will hold the value of r1 ^ r4, means performing XOR operation bit by bit.

                           Opcode for XOR = 0110011
                           rd = r10 = 01010
                           rs1 = r1 = 00001
                           rs2 = r4 = 00100
                           func3 = 100
                           func7 = 0000000

32 bits instruction : 
   0000000_00100_00001_100_01010_0110011

# SLT r11, r2, r4

                  Since the logical operation is performed on registers, hence this instruction belongs to R-type instruction set.r1 is the destination register that sets to 1, if r2 is less than r4, else 0 if r2 is greater than r4.

                           Opcode for SLT = 0110011
                           rd = r1 = 01011
                           rs1 = r2 = 00010
                           rs2 = r4 = 00100
                           func3 = 010
                           func7 = 0000000

32 bits instruction : 
   0000000_00100_00010_010_01011_0110011

# ADDI r12, r4, 5

             In this instruction ADD means Addition, I means Immediate, therefore ADDI means Addition with Immediate, hence this instruction belongs to I-type instruction set.r12 is the destination register that will store the value of r5 sum-up with the immediate value 5.

                           Opcode for ADDI = 0010011
                           rd = r12 = 01100
                           rs1 = r4 = 00100
                           imm[11:0] = 5 = 000000000101
                           func3 = 000

32 bits instruction : ] 
   000000000101_00100_000_01100_0010011

# SW r3, r1, 2

               In this instruction SW means store word, hence this instruction belongs to S-type instruction set.r3 is the source register. This instruction will store the value located in register r3 at the address obtained by adding the immediate address 2 with the address located in register r1.

                            Opcode for SW = 0100011
                            rs2 = r3 = 00011
                            rs1 = r1 = 00001
                            imm[11:0] = 2 = 000000000010
                            func3 = 010

32 bits instruction : 
   0000000_00011_00001_010_00010_0100011

# SRL r16, r14, r2

               SRL means Logical Shift Right and since the operation is performed on registers, this instruction belongs to R-type instruction set.r16 is the destination register, in which the value stored in r14 will be written after performing logical right shift based on the number stored in r2.

                           Opcode for SRL = 0110011
                           rd = r16 = 10000
                           rs1 = r14 = 01110
                           rs2 = r2 = 00010
                           func3 = 101
                           func7 = 0000000
			   
32 bits instruction : 
   0000000_00010_01110_101_10000_0110011

# BNE r0, r1, 20

                BNE is a branching instruction (B-type) based on conditions. Here BNE specifies the condition that the value stored in r0 != (is not equal to) the value stored in r1. If the condition becomes true, Program Counter will be updated by PC + 20, else PC + 4 for next instruction.

                           Opcode for BNE = 1100011
                           rs1 = r0 = 00000
                           rs2 = r1 = 00001
                           imm[12:1] = 20 = 000000010100
                           func3 = 001
			   
32 bits instruction : 
   0_000001_00001_00000_001_0100_0_1100011

# BEQ r0, r0, 15

                BEQ is a branching instruction (B-type) based on conditions. Here BEQ specifies the condition that the value stored in r0 == (is equal to) the value stored in r0. If the condition becomes true, Program Counter will be updated by PC + 15, else PC + 4 for next instruction.

                           Opcode for BEQ = 1100011
                           rs1 = r0 = 00000
                           rs2 = r0 = 00000
                           Imm[12:1] = 000000001111
                           func3 = 000
			   
32 bits instruction : 
   0_000000_00000_00000_000_1111_0_1100011

# LW r13, r1, 2

                LW stands for Load Word. Word is equal to 32 bits or 4 bytes. Since there is an immediate value given in the instruction which helps to calculate the address of memory from where we have to fetch the data, hence this instruction belongs to I-type.r13 is the destination register that will hold the value fetched from the memory location calculated by using (address value stored in r1 + immediate value)

                           Opcode for LW = 0000011
                           rd = r13 = 01101
                           rs1 = r1 = 00001
                           imm[11:0] = 000000000010
                           func3 = 010
			   
32 bits instruction : 
   000000000010_00001_010_01101_0000011

# SLL r15, r1, r2

                SLL means Logical Shift Left and since the operation is performed on registers, this instruction belongs to R-type instruction set.r15 is the destination register, in which the value stored in r1 will be written after performing logical left shift based on the number stored in r2.

                           Opcode for SLL = 0110011
                           rd = r15 = 01111
                           rs1 = r1 = 00001
                           rs2 = r2 = 00010
                           func3 = 001
                           func7 = 0000000
			   
32 bits instruction :
                     0000000_00010_00001_001_01111_0110011


