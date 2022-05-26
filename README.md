# RISC-V_based_MYTH
RISC-V based MYTH

![](risc-v/risc-v_banner.png)
### ABOUT THE WORKSHOP
The Workshop is a 5-day basic to advance program that is design for fresher and professional who wants to build a career in VLSI industry. It is a cloud based workshop that comprises of training courses that covers RISC-V specs, RISC-V software, How to implement RISC-V basic specs using TL-Verilog and Simulate your own RISC-V core. In short, you are going to write RTL and build RISC-V core on your own.
### AUTHOR OF THE WORKSHOP
#### Mr. Kunal Ghosh
Co-founder of VLSI System Design (VSD) Corporation Private Limited
### AGENDA
 [Day 1 : Introduction to RISC-V ISA and GNU compiler toolchain](#Day1)
  * [Part 1: Introduction to RISC-V basic keywords](#Part1-Introduction-to-RISC-V-basic-keywords)
  * [Part 2: Labwork for RISC-V software toolchain](#Part2-Labwork-for-RISC-V-software-toolchain)
  * [Part 3: Integer number representation](#Part3-Integer-number-representation)
 
 [Day 2: Introduction to ABI and basic verification flow](#Day2)
  * [Part 1: Application Binary interface (ABI)](#Part1-Application-Binary-Interface-ABI)
  * [Part 2: Lab work using ABI function calls](#Part2-Lab-work-using-ABI-function-calls)
  * [Part 3: Basic verification flow using iverilog](#Part3-Basic-verification-flow-using-iverilog)

 [Day 3 : Digital Logic with TL-Verilog and Makerchip](#Day3)
  * [Part 1: Combinational logic in TL-Verilog using Makerchip](#Part1-Combinational-logic-in-TL-Verilog-using-Makerchip)
  * [Part 2: Sequential and pipelined logic](#Part2-Sequential-and-pipelined-logic)
  * [Part 3: Validity](#Part3-Validity)
  * [Part 4: Hierarchy](#Part4-Hierarchy)

 [Day 4 : Basic RISC-V CPU micro-architecture](#Day4)
  * [Part 1: Microarchitecture and testbench for a simple RISC-V CPU](#Part1-Microarchitecture-and-testbench-for-a-simple-RISC-V-CPU)
  * [Part 2: Fetch, decode, and execute logic](#Part2-Fetch,-decode,-and-execute-logic)
  * [Part 3: RISC-V control logic](#Part3-RISC-V-control-logic)

 [Day 5 : Complete Pipelined RISC-V CPU micro-architecture/store](#Day5)
  * [Part 1: Pipelining the CPU](#Part1-Pipelining-the-CPU)
  * [Part 2: Load and store instructions and memory](#Part2-Load-and-store-instructions-and-memory)
  * [Part 3: Completing the RISC-V CPU](#Part3-Completing-the-RISC-V-CPU)
  * [Part 4: Wrap-up and future opportunities](#Part4-Wrap-up-and-future-opportunities)
  
## Day1

## Part1 Introduction to RISC-V basic keywords
A RISC-V ISA is defined as a base integer ISA, which must be present in any implementation, plus optional extensions to the base ISA. Each base integer instruction set is characterized by
- Width of the integer registers (XLEN)
- Corresponding size of the address space
- Number of integer registers (32 in RISC-V)
More details on RISC-V ISA can be obtained here.
Overview of GNU compiler toolchain
The GNU Toolchain is a set of programming tools in Linux systems that programmers can use to make and compile their code to produce a program or library. So, how the machine code which is understandable by processer is explained below.
* Preprocessor - Process source code before compilation. Macro definition, file inclusion or any other directive if present then are preprocessed.
* Compiler - Takes the input provided by preprocessor and converts to assembly code.
* Assembler - Takes the input provided by compiler and converts to relocatable machine code.
* Linker - Takes the input provided by Assembler and converts to Absolute machine code.
Under the risc-v toolchain,
To use the risc-v gcc compiler use the below command:
```riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o <object filename> <C filename>```
More generic command with different options:
```riscv64-unknown-elf-gcc <compiler option -O1 ; Ofast> <ABI specifier -lp64; -lp32; -ilp32> <architecture specifier -RV64 ; RV32> -o <object filename> <C filename>```
More details on compiler options can be obtained here
To view assembly code use the below command,
```riscv64-unknown-elf-objdump -d <object filename>```
To use SPIKE simualtor to run risc-v obj file use the below command,
```spike pk <object filename>```
To use SPIKE as debugger
```spike -d pk <object Filename>``` with degub command as ```until pc 0 <pc of your choice>```
To install complete risc-v toolchain locally on linux machine,
- RISC-V GNU Toolchain
- RISC-V ISA SImulator - Spike
Once done with installation add the PATH to .bashrc file for future use.
![](risc-v/rv-day1lec1.png)
![](risc-v/rv-day1lec2.png)
![](risc-v/rv-day1lec3.png)
## Part2 Labwork for RISC-V software toolchain
Labs question:
1)   For the C program used in labs, use a value of n=9, compile and simulate using gcc compiler. What is the output you get?
```ans. 45```
![](risc-v/rv-assd1lab1.png)
2)   As shown in labs, compile the C program (n=9) using riscv-gcc compiler with O1 switch and look at assembly code using riscv-objdmp. What is the memory location of "printf" subroutine ?
```ans. 10408```
![](risc-v/rv-assd1labprintf1.png)
3)   How many instructions are used in "printf" subroutine for C program (n=9) compiled with riscv-gcc and O1 switch?
```ans. 21```
![](risc-v/rv-assd1labq3.png)
4)   As shown in labs, compile the C program (n=9) using riscv-gcc compiler with Ofast switch and look at assembly code using riscv-objdmp. How many instructions are used by "main" program ?
```ans. 11```
![](risc-v/rv-assd1labq4.png)
5)   Debug C program (n=9) with spike and run until PC is 100b0. What are the contents of register a0?
```ans. 1```
![](risc-v/rv-assd1labq5.png)
6)   Debug C program (n=9) with spike and run until PC is 100b0. What are the contents of register sp?
```ans. 0x0000003ffffffb40```
![](risc-v/rv-assd1labq6.png)
7)   Debug C program (n=9) with spike and run until PC is 100c4. What are the contents of register a0?
```ans. 21180```
![](rv-day1ass2q7ans.png)
8)   Debug C program (n=9) with spike and run until PC is 100dc. What is the output on shell?
```ans. Sum of numbers from 1 to 9 is 45```
![](risc-v/rv-assd1labq8.png)
## Part3 Integer number representation
In this lab u need to cast ```unsigned long long int``` before the pow function. To resolve the variable limitation of int.
![](risc-v/rv-assd1lab2q4.png)
4)   Modify the unsignedHighest.c program to display highest and lowest 64-bit signed integers. Debug using spike. Run until PC is 100d8. What message gets printed at this point?
```ans. highest number represented by signed long long int ...```
```highest number represented by signed long long int is 9223362036854775807 and lowest number represented by signed long long int is -9223362036854775808```
![](risc-v/rv-assd1lab2q4ans.png)
5)   Modify the unsignedHighest.c program to display highest and lowest 64-bit signed integers. View the assembly code using riscv-objdmp. What is the address location of "printf" subroutine ?
```ans. 10420```
![](risc-v/rv-assd1lab2q5ans.png)

## Day2

## Part1 Application Binary interface (ABI)
An Application Binary Interface is a set of rules enforced by the Operating System on a specific architecture. So, Linker converts relocatable machine code to absolute machine code via ABI interface specific to the architecture of machine.
So, it is system call interface used by the application program to access the registers specific to architecture. Overhere the architecture is RISC-V, so to access 32 registers of RISC-V below is the table which shows the calling convention (ABI name) given to registers for the application programmer to use.
![](risc-v/rv-day2lec.png)
## Part2 Lab work using ABI function calls
![](risc-v/rv-day2labass3labs1.png)
![](risc-v/rv-day2lab.png)
![](risc-v/rv-day2labq2.png)
![](risc-v/rv-day2labq3.png)
![](risc-v/rv-day2labass2q4and5ans.png)
## Part3 Basic verification flow using iverilog
![](risc-v/rv-day2labass3labs.png)
![](risc-v/rv-day2labass3labs1.png)
![](risc-v/rv-day2ass3labq1ans.png)

## Day3
## Day4
## Day5
