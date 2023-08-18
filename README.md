# VLSI Physical Design for ASICs
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a digital circuit's logical representation into a physical layout that meets various performance, power, area, and manufacturability requirements.
# SKILL OUTCOMES
1. Architectural Design
2. RTL Design / Behavioral Modeling
3. Floorplanning
4. Placement
5. Clock Tree Synthesis
6. Routing

# TABLE OF CONTENTS
# DAY_1 Introduction to RISCV ISA and GNU Compiler Toolchain
Introduction to Basic Keywords
1. Introduction

ISA (Instruction Set Archhitecture)

ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks. It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

RISC-V

Reduced Instruction Set Computing - Five.
It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.  RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4eabe0b7-4581-419b-88e7-84c7ac1dac8e">

2. From Apps to Hardware

Apps

  Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.

  System software
  
System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.

Operating System

The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

Compiler

A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

Assembler

An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

RTL

 RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 Hardware
 
Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

3. Detail Description of Course Content

Labwork for RISCV Toolchain

1. C Program

We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

<img width="345" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2d5e3fe1-f8fd-434b-8faf-2912d3c056e1">

Using the gcc compiler, we compiled the program to get the output.

<img width="545" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/0b7e7911-d0b2-4a6a-aefd-cd9b4d520a4f">


2. RISCV GCC Compiler and Dissemble

Using the riscv gcc compiler, riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c, we compiled the C program.

Using ls -ltr sum1ton.c, we can check that the object file is created.

To get the assembly code for the C program, riscv64-unknown-elf-objdump -d sum1ton.o | less .

In order to view the main section, type /main.

Here, since we used -O1 optimisation, the number of instructions are 15.

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/98843b92-0beb-4bfc-ba4b-1dac5c93ed3c">

When we use -Ofast optimisation, we can see that the number of instructions have been reduced to 12.
<img width="422" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3eb7afcd-0645-4340-bcac-ae2dc3258ce3">

3. Spike Simulation and Debug

spike pk sum1ton.o is used to check whether the instructions produced are right to give the correct output.

<img width="523" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2fa7d825-102f-41ed-b9e6-a31c2417cb22">

spike -d pk sum1ton.c is used for debugging.

The contents of the registers can also be viewed.

<img width="317" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/be6fcaa9-ab93-46e0-8da3-7b8056d09f0c">


Integer Number Representation 

1. Unsigned Numbers

Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
Range: 0 to 2^(N-1) - 1.

2. Signed Numbers

 Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
 Range : -(2^(N-1)) to 2^(N-1) - 1.
 
3. Labwork

# DAY_2 Introduction to ABI and Basic Verification Flow
Application Binary Interface
1. Introduction to ABI
2. Memmory Allocation for Double Words
3. Load, Add and Store Instructions
4. 32-Registers and their ABI Names

Labwork using ABI Function Calls
1. Algorithm for C Program using ASM
2. Review ASM Function Calls
3. Simulate C Program using Function Call
