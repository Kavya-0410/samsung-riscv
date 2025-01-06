# Samsung RISC-V Project
"Repository for RISC-V related projects and experiments under Samsung's ecosystem."

Task 1-
C Language and RISC-V Based Compilation Lab
This repository contains the tasks and steps related to compiling C code using both GCC (GNU Compiler Collection) and RISC-V GCC compiler. It involves writing C code to calculate the sum of numbers from 1 to N and compiling the code using both traditional GCC and the RISC-V GCC compiler.
Task 1.1: C Language-based Compilation
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

Task 1.2: RISC-V Based Compilation
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


