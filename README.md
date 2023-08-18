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
  Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.
The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.
A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.
An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.
 RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.
Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

3. Detail Description of Course Content

Labwork for RISCV Toolchain
1. C Program
<img width="345" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2d5e3fe1-f8fd-434b-8faf-2912d3c056e1">
<img width="545" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/0b7e7911-d0b2-4a6a-aefd-cd9b4d520a4f">

2. RISCV GCC Compiler and Dissemble
<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/98843b92-0beb-4bfc-ba4b-1dac5c93ed3c">
<img width="422" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3eb7afcd-0645-4340-bcac-ae2dc3258ce3">

3. Spike Simulation and Debug
<img width="523" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2fa7d825-102f-41ed-b9e6-a31c2417cb22">
<img width="317" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/be6fcaa9-ab93-46e0-8da3-7b8056d09f0c">

Integer Number Representation  
1. Unsigned Numbers
2. Signed Numbers
3. Labwork

# DAY_2 Introduction to ABI and Basic Verification Flow
Application Binary Interface
1. Introduction
2. Memmory Allocation for Double Words
3. Load, Add and Store Instructions
4. 32-Registers and their ABI Names

Labwork using ABI Function Calls
1. Algorithm for C Program using ASM
2. Review ASM Function Calls
3. Simulate C Program using Function Call
