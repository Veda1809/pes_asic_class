# VLSI Physical Design for ASICs
## Objective
The objective of VLSI (Very Large Scale Integration) physical design for ASICs (Application-Specific Integrated Circuits) is to transform a logical design description (RTL - Register Transfer Level) into a physical layout that can be fabricated as an integrated circuit. This involves translating the high-level functional representation of the circuit into a physical implementation that meets design constraints, performance targets, and manufacturability requirements.

# SKILL OUTCOMES
+ Architectural Design
+ RTL Design / Behavioral Modeling
+ Floorplanning
+ placement
+ clock Tree Synthesis
+ Routing

# INSTALLATION
<details>
<summary> Riscv_toolchain Installation </summary>

https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh

+ Download the run.sh
+ Open terminal
+ `cd Downloads`
+ `./run.sh `
+ If permission denied, then
   - `chmod +x run.sh`
   - `./run.sh`
+ If error in configure,
  
  <img width="432" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/cab4ecd6-5228-43e6-9181-0a025e5bc655">
  
     - `cd`
     - `cd riscv_toolchain/iverilog `
     - `./configure `
     - ` make`
     - `sudo make install`
       
+ To check if riscv-gcc compiler is in the path,
     - `gedit ~/.bashrc `
     -  insert this in the bash file if not present:
       
           `export PATH=~/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH `

   ### End of installation
</details>

<details>
<summary> Yosys with GTKwave Installation </summary>
	
+ `cd`
+ `git clone https://github.com/YosysHQ/yosys.git`
+ `cd yosys`
+ `sudo apt install make`
+ `sudo apt-get update`
+ `sudo apt-get install build-essential clang bison flex  libreadline-dev gawk tcl-dev libffi-dev git  graphviz xdot pkg-config python3 libboost-system-dev libboost-python-dev libboost-filesystem-dev zlib1g-dev`
+ `make config-gcc`
+ `make`
+ `sudo make install`
+ `sudo apt install gtkwave`
+ Type `yosys`
  
  <img width="358" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e2ef73dd-d9b5-4f6c-9db5-d1e89c7fa88a">
  
  If received as shown above, installation is successful.

    ### End of installation
</details>

# TABLE OF CONTENTS
## DAY 1 
**Introduction to RISCV ISA and GNU Compiler Toolchain**
+ [Introduction to Basic Keywords](#introduction-to-basic-keywords)
  - Introduction
  - From Apps to Hardware
  - Detail Description of Course Content
+ [Labwork for RISCV Toolchain](#labwork-for-riscv-toolchain)
  - C Program
  - RISCV GCC Compiler and Dissemble
  - Spike Simulation and Debug
+ [Integer Number Representation](#integer-number-representation) 
  - 64-bit Unsigned Numbers
  - 64-bit Signed Numbers
  - Labwork For Signed and Unsigned Numbers

## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ [Application Binary Interface](#application-binary-interface)
  - Introduction to ABI
  - Memory Allocation for Double Words
  - Load, Add and Store Instructions
  - 32-Registers and their ABI Names
+ [Labwork using ABI Function Calls](#labwork-using-abi-function-calls)
  - Algorithm for C Program using ASM
  - Review ASM Function Calls
  - Simulate C Program using Function Call
  - Lab to Run C-Program On RISCV-CPU

## DAY 3
**Introduction to Verilog RTL design and Synthesis**
+ [Introduction to Open-Source Simulator iVerilog](#introduction-to-open-source-simulator-iverilog)
   - Introduction to iVerilog Design Testbench
+ [Labs using iVerilog and GTKwave](#labs-using-iverilog-and-gtkwave)
   - Introduction to Lab
   - iVerilog GTKwave Part-1
   - iVerilog GTKwave Part-2
+ [Introduction to Yosys and Logic synthesis](#introduction-to-yosys-and-logic-synthesis)
   - Introduction to Yosys
   - Introduction to Logic Synthesis
+ [Labs using Yosys and Sky130 PDKs](#labs-using-yosys-and-sky130-pdks)
   - Yosys good mux
 
## DAY 4
**Timing Libs, Hierarchical vs Flat Synthesis and Efficient Flop Coding Styles**
+ [Introduction to Timing Dot Libs](#introduction-to-timing-dot-libs)
  - Introduction to Dot Lib
+ [Hierarchical vs Flat Synthesis](#hierarchical-vs-flat-synthesis)
  - Hierarchical Synthesis Flat Synthesis 
+ [Various Flop Coding Styles and Optimization](#various-flop-coding-styles-and-optimization)
  - Why Flops and Flop Coding Styles
  - Lab Flop Synthesis Simulations
  - Interesting Optimisations

## DAY 5
**Combinational and Sequential Optmizations**
+ [Introduction to Optimisations](#introduction-to-optimisations)
+ [Combinational Logic Optimisations](#combinational-logic-optimisations)
+ [Sequential Logic Optimisations](#sequential-logic-optimisations)
+ [Sequential Optimisations for Unused Outputs](#sequential-optimisations-for-unused-outputs)

## DAY 6
**GLS, Blocking vs Non-Blocking and Synthesis-Simulation Mismatch**
+ [GLS Synthesis-Simulation Mismatch and Blocking Non-Blocking Statements](#gls-synthesis-simulation-mismatch-and-blocking-non-blocking-statements)
  - GLS Concepts And Flow Using Iverilog
  - Synthesis Simulation Mismatch
  - Blocking And Non Blocking Statements In Verilog
  - Caveats With Blocking Statements
+ [Labs on GLS and Synthesis-Simulation Mismatch](#labs-on-gls-and-synthesis-simulation-mismatch)
+ [Labs on Synth-Sim Mismatch for Blocking Statement](#labs-on-synth-sim-mismatch-for-blocking-statement)

# Day-1   
## Introduction to Basic Keywords
<details>
<summary> Introduction </summary>
	
- **ISA (Instruction Set Archhitecture)**
  - ISA defines the interface between a computer's hardware and its software, specifically how the processor and its components interact with the software instructions that drive the execution of tasks.
  - It encompasses a set of instructions, addressing modes, data types, registers, memory organization, and the mechanisms for executing and managing instructions.

- **RISC-V (Reduced Instruction Set Computing - Five)**.
  - It is an open-source Instruction Set Architecture (ISA) that has gained significant attention and adoption in the world of computer architecture and semiconductor design.
  - RISC architectures simplify the instruction set by focusing on a smaller set of instructions, each of which can be executed in a single clock cycle. This approach usually leads to faster execution of individual instructions. 

<img width="536" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4eabe0b7-4581-419b-88e7-84c7ac1dac8e">

</details>

<details>
<summary> From Apps to Hardware </summary>

1. **Apps:** Application software, often referred to simply as "applications" or "apps," is a type of computer software that is designed to perform specific tasks or functions for end-users.
2. **System software:** System software refers to a category of computer software that acts as an intermediary between the hardware components of a computer system and the user-facing application software. It provides essential services, manages hardware resources, and enables the execution of application programs. System software plays a critical role in maintaining the overall functionality, security, and performance of a computer system.'
3. **Operating System:** The operating system is a fundamental piece of software that manages hardware resources and provides various services for both users and application programs. It controls tasks such as memory management, process scheduling, file system management, and user interface interaction. Examples of operating systems include Microsoft Windows, macOS, Linux, and Android.

4. **Compiler:** A compiler is a type of software tool that translates high-level programming code written by developers into assembly-level language.

5. **Assembler:** An assembler is a software tool that translates assembly language code into machine code or binary code that can be directly executed by a computer's processor.

6. **RTL:** RTL serves as an abstraction level in the design process that represents the behavior of a digital circuit in terms of registers and the operations that transfer data between them.

 7. **Hardware:** Hardware refers to the physical components of a computer system or any electronic device. It encompasses all the tangible parts that make up a computing or electronic device and enable it to perform various tasks.

</details>

<details>
<summary> Detail Description of Course Content </summary>

**Pseudo Instructions:** Pseudo-instructions are used to simplify programming, improve code readability, and reduce the number of explicit instructions a programmer needs to write. They are especially useful for common programming patterns that involve multiple instructions.
`Ex: li, mv`.

**Base Integer Instructions:** The term "base integer instructions" refers to the fundamental set of instructions that form the foundation for performing basic arithmetic, logical, and data movement operations.
`Ex: add, sub, and, or, xor, sll`.

**Multiply Extension Intructions:** The RISC-V architecture includes a set of multiply and multiply-accumulate (MAC) extension instructions that enhance the instruction set to perform efficient multiplication and multiplication-accumulate operations.
`Ex: mul, mulh, mulhu, mulhsu`.

**Single and Double Precision Floating Point Extension:** The RISC-V architecture includes floating-point extensions that provide support for both single-precision (32-bit) and double-precision (64-bit) floating-point arithmetic operations. These extensions are often referred to as the "F" and "D" extensions, respectively. Floating-point arithmetic is essential for handling real numbers with fractional parts and for performing accurate calculations involving decimal values.

**Application Binary Interface:** ABI stands for "Application Binary Interface." It is a set of rules and conventions that govern how software components interact with each other at the binary level. The ABI defines various aspects of program execution, including how function calls are made, how parameters are passed and returned, how memory is allocated and managed, and more.

**Memory Allocation and Stack Pointer** 
- Memory allocation refers to the process of assigning and managing memory segments for various data structures, variables, and objects used by a program. It involves allocating memory space from the system's memory pool and releasing it when it is no longer needed to prevent memory leaks.
- The stack pointer is a register used by a program to keep track of the current position of the program's execution on the call stack. 

</details>

## Labwork for RISCV Toolchain

<details>
<summary> C Program </summary>

+ We wrote a C program for calculating the sum from 1 to n using a text editor, leafpad.

`leafpad sumton.c`
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=111;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
<img width="345" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2d5e3fe1-f8fd-434b-8faf-2912d3c056e1">

+ Using the gcc compiler, we compiled the program to get the output.

`gcc sumton.c`
`.\a.out`

<img width="545" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/0b7e7911-d0b2-4a6a-aefd-cd9b4d520a4f">

</details>

<details>
<summary> RISCV GCC Compiler and Dissemble </summary>

+ Using the riscv gcc compiler, we compiled the C program.

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c`

+ Using `ls -ltr sum1ton.c`, we can check that the object file is created.

+ To get the dissembled ALP code for the C program, 

`riscv64-unknown-elf-objdump -d sum1ton.o | less` .

+ In order to view the main section, type 
   - `/main`
   - press ENTER
   - press `n` to search next occurance
   -  press `N` to search for previous occurance

+ Here, since we used -O1 optimisation, the number of instructions are 15.

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/98843b92-0beb-4bfc-ba4b-1dac5c93ed3c">

+ When we use -Ofast optimisation, we can see that the number of instructions have been reduced to 12.

<img width="422" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3eb7afcd-0645-4340-bcac-ae2dc3258ce3">

   - -Onumber : level of optimisation required
   - -mabi : specifies the ABI (Application Binary Interface) to be used during code generation according to the requirements
   - -march : specifies target architecture

+ In order to view the different options available for these fields, use the following commands

 go to the directory where riscv64-unkonwn-elf is present

  - -O1 : ``` riscv64-unkonwn-elf --help=optimizer```
  - -mabi : ```riscv64-unknown-elf-gcc --target-help```
  - -march : ```riscv64-unknown-elf-gcc --target-help```

+ To quit:
  - use ```esc :q``` to quit

</details>

<details>
<summary> Spike Simulation and Debug </summary>

+ `spike pk sum1ton.o` is used to check whether the instructions produced are right to give the correct output.

<img width="523" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2fa7d825-102f-41ed-b9e6-a31c2417cb22">


+ `spike -d pk sum1ton.c` is used for debugging.

+ The contents of the registers can also be viewed.

<img width="317" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/be6fcaa9-ab93-46e0-8da3-7b8056d09f0c">

   - press ENTER : to show the first line and successive ENTER to show successive lines
   - reg 0 a2 : to check content of register a2 0th core
   - q : to quit the debug process

</details>

## Integer Number Representation 

<details>
<summary> Unsigned Numbers </summary>

- Unsigned numbers, also known as non-negative numbers, are numerical values that represent magnitudes without indicating direction or sign.
- Range: [0, (2^n)-1 ]

</details>

<details>
<summary> Signed Numbers </summary>

- Signed numbers are numerical values that can represent both positive and negative magnitudes, along with zero.
- Range :
   - Positive : [0 , 2^(n-1)-1]
   - Negative : [-1 to 2^(n-1)]

</details>

<details>
<summary> Labwork </summary>

+ We wrote a C program that shows the maximum and minimum values of 64bit unsigned numbers.

``` c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```
<img width="531" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1195a00a-9b42-4a33-bce0-6095e5350647">


+ We wrote a C program that shows the maximum and minimum values of 64bit signed numbers.
``` c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```
<img width="481" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/48c4c465-8324-4765-98fe-20584143f33f">

</details>

# Day-2
## Application Binary Interface

<details>
<summary> Introduction to ABI </summary>

+ An Application Binary Interface (ABI) is a set of rules and conventions that dictate how binary code interacts with and communicates with other binary code, typically at the level of machine code or compiled code. In simpler terms, it defines the interface between two software components or systems that are written in different programming languages, compiled by different compilers, or running on different hardware architectures.
+ The ABI is crucial for enabling interoperability between different software components, such as different libraries, object files, or even entire programs. It allows components compiled independently and potentially on different platforms to work seamlessly together by adhering to a common set of rules for communication and data representation.

</details>

<details>
<summary> Memory Allocation for Double Words </summary>

64-bit number (or any multi-byte value) can be loaded into memory in little-endian or big-endian. It involves understanding the byte order and arranging the bytes accordingly
1. **Little-Endian:**
In little-endian representation, you store the least significant byte (LSB) at the lowest memory address and the most significant byte (MSB) at the highest memory address.
2. **Big-Endian:**
In big-endian representation, you store the most significant byte (MSB) at the lowest memory address and the least significant byte (LSB) at the highest memory address.
#### For example, consider the 64-bit hexadecimal value 0x0123456789ABCDEF. 
In Little-Endian representation, it would be stored as follows in memory:

<img width="453" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8c63e751-8882-4b1e-a2f8-84da628ee604">


In Big-Endian representation, it would be stored as follows in memory:

<img width="454" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3954540e-800f-4503-97ef-6c77daacd058">

</details>

<details>
<summary> Load, Add and Store instructions </summary>

Load, Add, and Store instructions are fundamental operations in computer architecture and assembly programming. They are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.

</details>

<details>
<summary> 32-Registers and their ABI Names </summary>

The choice of the number of registers in a processor's architecture, such as the RISC-V RV64 architecture with its 32 general-purpose registers, involves a trade-off between various factors. While modern processors can have more registers but increasing the number of registers could lead to larger instructions, which would take up more memory and potentially slow down instruction fetch and decode.
#### ABI Names
ABI names for registers serve as a standardized way to designate the purpose and usage of specific registers within a software ecosystem. These names play a critical role in maintaining compatibility, optimizing code generation, and facilitating communication between different software components. 

<img width="430" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3b7aed64-37cd-492f-b9b5-cd840103566a">

</details>

## Labwork using ABI Function Calls

<details>
<summary> Algorithm for C Program using ASM </summary>

- Incorporating assembly language code into a C program can be done using inline assembly or by linking separate assembly files with your C code.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.
<img width="477" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/6afb1381-2237-46b0-831a-984e73e1e289">

</details>

<details>
<summary> Review ASM Function Calls </summary>

- We wrote C code in one file and your assembly code in a separate file.
- In the assembly file, we declared assembly functions with appropriate signatures that match the calling conventions of your platform.

**C Program**
`custom1to9.c`
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
```
**Asseembly File**
`load.s`
``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```

</details>

<details>
<summary> Simulate C Program using Function Call </summary>

+ **Compilation:** To compile C code and Asseembly file use the command

`riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o custom1to9.o custom1to9.c load.s` 

this would generate object file `custom1to9.o`.

+ **Execution:** To execute the object file run the command 

`spike pk custom1to9.o`

<img width="517" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/46d311ec-4bf9-4ad8-b758-b39eef1dbc7c">

</details>

<details>
<summary> Lab to Run C-Program on RICV-CPU </summary>


+ `git clone https://github.com/kunalg123/riscv_workshop_collaterals.git`

+ `cd riscv_workshop_collaterals`

+ `ls -ltr`

+ `cd labs`

+ `ls -ltr`

+ `chmod 777 rv32im.sh`

+ `./rv32im.sh`

<img width="517" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/16c15f04-b5c9-441f-9b87-f9e35b19dc6f">

</details>

# Day-3
## Introduction to Open-Source Simulator iVerilog
<details>
<summary> Introduction to iVerilog Design Testbench </summary>

 - **Simulator**
   - It is a tool used for simulating the design. It looks for the changes on the input signals to evaluate the outputs.
   - If there is no change in the inputs, the simulator doesn't evaluate the outputs.
   - RTL is checked for adherence to the spec by simulating the design.
   - The tool used here is **iverilog** .

- **iVerilog**
  -  It is an open-source Verilog simulator used for testing and simulating digital circuit designs described in the Verilog hardware description language (HDL).
  -  Both the design and the testbench are fed to the simulator and it produces a vcd (value change dump) file.
  -  In order to view the vcd file, we use the GTKwave where we can see the wave forms.
    
   <img width="526" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/37b643b5-e41e-425d-85f0-a55d7e190571">

- **Design**
  - It is the actual verilog code or set of verilog codes which ahs the intended functionality to meet with the required specifications.
  - Verilog is used to describe the behavior and structure of digital circuits at different levels of abstraction, from high-level system descriptions down to low-level gate-level representations. 

- **Testbench**
  - A testbench is a specialized Verilog module or program used to verify the functionality and behavior of another Verilog module, circuit, or design. Testbenches are essential for testing and simulating digital designs before they are synthesized or manufactured as physical chips.
  - It is a setup to apply stimulus to the design to check its functionality.

    <img width="526" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/72e6ffe4-abba-41f1-b79f-240f125b410b">

</details>

## Labs using iVerilog and GTKwave

<details>
<summary> Introduction to Lab </summary>

+ Make a directory named vsd `mkdir vsd`.
+ `cd vsd`.
+ `git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git`
+ Creates a folder called `sky130RTLDesignAndSynthesisWorkshop` in the `vsd` directory.

 <img width="377" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/0a28a7e8-7567-4d5a-8734-5da2e9533a28">

  - my_lib : contains all the library files

  - lib : contains sky130 standard cell library used for our synthesis

  - verilog_model : contains all the standard cell verilog modules of the standard cells contained in the .lib

  - verilog_files : contains all the verilog source files and testbench files which are required for labs

</details>

<details>
<summary> iVerilog GTKwave Part-1 </summary>	


+ `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`

+ we have loaded the source code along with the testbench code into the iverilog simulator

+ `iverilog good_mux.v tb_good_mux.v`

+ We can see that an output file `a.out` has been created.

+ `./a.out`

+ The output of the iverilog, a vcd file,  is created which is loaded into the simualtor gtkwave.

+ ` gtkwave tb_good_mux.vcd `

<img width="767" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/14bdf7a7-7a4b-4a1f-9875-96575f59239e">


<img width="497" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e7627aaf-6048-445a-aaae-1117212d9670">

</details>

<details>
<summary> iVerilog GTKwave Part-2 </summary>

+ In order to view the contents in the files,

+ `gvim tb_good_mux.v -o good_mux.v`

<img width="367" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/ef3c8e61-2e45-4087-9584-f84fd3584cd3">

</details>

## Introduction to Yosys and Logic Synthesis

<details>
<summary> Introduction to Yosys </summary>

+ **Synthesizer**
  - It is a tool used for converting RTL design code to netlist.
  - Here, the synthesizer used is **Yosys**.

+ **Yosys**
  - It is an open-source framework for Verilog RTL synthesis and formal verification.
  - Yosys provides a collection of tools and algorithms that enable designers to transform high-level RTL (Register Transfer Level) descriptions of digital circuits into optimized gate-level representations suitable for physical implementation on hardware.

 <img width="561" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5f879aaa-ec65-4362-9f91-f39999069732">

   - Design and .lib files are fed to the synthesizer to get a netlist file.
   - **Netlist** is the representation of the design in the form of standard cells in the .lib
     
+ Commands used to perform different opertions:
  - `read_verilog` to read the design
  - `read_liberty` to read the .lib file
  - `write_verilog` to write out the netlist file
 
+ To verify the synthesis

<img width="566" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fd73f6b8-f594-4e4f-bb1a-b600fb4475f8">

   - Netlist along with the tesbench is fed to the iverilog simulator.
   - The vcd file generated is fed to the gtkwave simulator.
   - The output on the simulator must be same as the output observed during RTL simulation.
   - Same RTL testbench can be used as the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

</details>

<details>
<summary> Introduction to Logic Synthesis </summary>

+ **Logic Synthesis**
  - Logic synthesis is a process in digital design that transforms a high-level hardware description of a digital circuit, typically in a hardware description language (HDL) like Verilog or VHDL, into a lower-level representation composed of logic gates and flip-flops.
  - The goal of logic synthesis is to optimize the design for various criteria such as performance, area, power consumption, and timing.

 + **.lib**
   - It is a collection of logical modules like And, Or, Not etc.
   - It has different flavors of same gate like 2 input AND gate, 3 input AND gate etc with different performace speed.
  
+ **Why different flavors  of gate?**
  - In order to make a circuit faster, the clock frequency should be high.
  - For that, the time period of the clock should be as low as possible.
  
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bc2242db-49e8-4c19-a06e-8f8e82f55729">

+ In a sequential circuit, clock period depends on:
  - Clock to Q of flip-flop A.
  - Propagation delay of combinational circuit.
  - Setup time of flip-flop B.

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/112de4cd-6e0c-46ec-ad94-0cb6540af7e1">

+ **Why need fast and slow cells?**
  - To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
  - For a smaller propagation time, we need faster cells.
  - The collection forms the .lib

+ **Faster Cells vs Slower Cells**
  - Load in digital circuit is of Capacitence.
  - Faster the charging or dicharging of capacitance, lesser is the cell delay.
  - However, for a quick charge/ discharge of capacitor, we need transistors capable of sourcing more current i.e, we need **wide transistors**.
  - Wider transistors have lesser delay but consume more area and power.
  - Narrow transistors have more delay but consume less area and performance.
  - Faster cells come with a cost of area and power.
 
+ **Selection of the Cells**
  - We have to guide the Synthesizer to choose the flavour of cells that is optimum for implementation of logic circuit.
  - More use of faster cells leads to bad circuit in terms of power and area and also hold time violations.
  - More use of slower cells leads to sluggish circuits amd may not meet the performance needs.
  - Hence the guidance is offered to the synthesiser in the form of **constraints**.
 
</details>

## Labs using Yosys and Sky130 PDKs
<details>
<summary> Yosys good_mux  </summary>	

+ To invoke **yosys**
  - `cd`
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - Type `yosys`

  <img width="396" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9e007d9e-c66d-4f8d-a4db-0dadd4bada38">

+ To read the library
    
     ` read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
    
+ To read the design

    `read_verilog good_mux.v`

 + To syntheis the module

      ` synth -top good_mux`

  <img width="334" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/f75014c5-c9f0-4813-ae56-ddbb71f79111">
  <img width="287" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4ab7cd35-c5d7-4ca9-a310-8d76056a67e1">

+ To generate the netlist

  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

  <img width="271" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/97358dfc-ec44-40e0-ac79-97c3576e6300">

It gives a report of what cells are used and the number of input and output signals.

+ To see the logic realised

  `show`

  <img width="300" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9b2957ea-f0bc-4f2c-b796-aa565bd0865c">

  The mux is completely realised in the form of sky130 library cells.

+ To write the netlist

   - `write_verilog good_mux_netlist.v`
   - `!gvim good_mux_netlist.v`
     
   - To view a simplified code
     
     ` write_verilog -noattr good_mux_netlist.v`
     
     `!gvim good_mux_netlist.v`
  
  
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/74fc2a01-3c35-4db1-8220-96595c6c236e">

<img width="479" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7adc16f5-f635-4532-b90c-a9f9c496f95f">


</details>

# Day 4
## Introduction to Timing Dot Libs
<details>
<summary> Introduction to Dot Lib </summary>	

+ To view the contents in the .lib

  `gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

  <img width="443" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/91edd5d4-bb82-48ec-b0bd-ca233d8a8063">

  + The first line in the file `library ("sky130_fd_sc_hd__tt_025C_1v80") ` :
    
    - tt : indicates variations due to process and here it indicates **Typical Process**.
    - 025C : indicates the variations due to temperatures where the silicon will be used.
    - 1v80 : indicates the variations due to the voltage levels where the silicon will be incorporated.
+ It also displays the units of various parameters.

  <img width="284" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d01d750e-fc1c-4de0-8e72-e6842c14f90b">
  <img width="229" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/39f26ac7-7302-4dc7-a517-6a5a031e2cae">

+ It gives the features of the cells
+ To enable line number `:se nu`
+ To view all the cells `:g//`
+ To view any instance `:/instance`
+ Since there are 5 inputs, for all the 32 possible combinations, it gives the delay, power and all the other parameters for each cell.
+ The below image shows the power consumption and area comparision.
  
<img width="911" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2a6b20a3-33d1-47e0-814f-6cff100ec2a7">

</details>

## Hierarchical vs Flat Synthesis
<details>
<summary> Hierarchical Synthesis Flat Synthesis </summary>	

**Hierarchical Synthesis**
  Hierarchical synthesis is an approach in digital design and logic synthesis where complex designs are broken down into smaller, more manageable modules or sub-circuits, and each module is synthesized individually. These synthesized modules are then integrated back into the overall design hierarchy. This approach helps manage the complexity of large designs and allows designers to work on different parts of the design independently.
  
+ The file we used in this lab is `multiple_modules.v`

  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  -  `gvim multiple_modules.v`

<img width="321" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/384b4475-a6e7-4905-9a70-cfdff657e6db">

+  `multiple_modules` instantiates `sub_module1` and `sub_module2`

+  Launch `yosys`
+  read the library file  `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  read the verilog file ` read_verilog multiple_modules.v`
+  `synth -top multiple_modules` to set it as top module

  <img width="380" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a69395c3-1e50-49cc-b356-6afe8b1f9c5e">
  <img width="219" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7163c184-566d-4568-abff-fcda8f6c9f63">
  
+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ To view the netlist `show multiple_modules`

  <img width="304" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/721a0563-1fbe-4ce7-975c-0ef8d50e7fe6">

- Here it shows `sub_module1` and `sub_module2` instead of AND gate and OR gate.

+ `write_verilog -noattr multiple_modules_hier.v`
+ `!gvim multiple_modules_hier.v`

<img width="371" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fcc68430-e284-4b54-80af-dfbcfbade0ea">
 <img width="300" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4e8ffd10-6efb-4d2d-878e-221d685502c1">

 **Flattened Synthesis**
  Flattened synthesis is the opposite of hierarchical synthesis. Instead of maintaining the hierarchical structure of the design during synthesis, flattened synthesis combines all modules and sub-modules into a single, flat representation. This means that the entire design is synthesized as a single unit, without preserving the modular organization present in the original high-level description.

+  Launch `yosys`
+  read the library file  `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  read the verilog file ` read_verilog multiple_modules.v`
+  `synth -top multiple_modules` to set it as top module
+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `flatten` to write out a flattened netlist
+ `show`

<img width="924" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bd069e1f-4da5-473a-b041-562cbef042f0">

+ `write_verilog -noattr multiple_modules_flat.v`
+ `!gvim multiple_modules_flat.v`
  
<img width="365" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/18760a81-9f03-4b11-9b8f-dd4758a25ab7">
<img width="300" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e3a80209-7339-4cef-833c-2c3bb1fc4dec">


</details>

## Various Flop Coding Styles and Optimization
<details>
<summary> Why Flops and Flop Coding Styles</summary>	

**Why do we need a Flop?**

+ A flip-flop (often abbreviated as "flop") is a fundamental building block in digital circuit design.
+ It's a type of sequential logic element that stores binary information (0 or 1) and can change its output based on clock signals and input values.
+ In a combinational circuit, the output changes after the propagation delay of the circuit once inputs are changed.
+ During the propagation of data, if there are different paths with different propagation delays, then a glitch might occur.
+ There will be multiple glitches for multiple combinational circuits.
+ Hence, we need flops to store the data from the combinational circuits.
+ When a flop is used, the output of combinational circuit is stored in it and it is propagated only at the posedge or negedge of the clock so that the next combinational circuit gets a glitch free input thereby stabilising the output.
+ We use control pins like **set** and **reset** to initialise the flops.
+ They can be synchronous and asynchronous.

**D Flip-Flop with Asynchronous Reset**
+ When the reset is high, the output of the flip-flop is forced to 0, irrespective of the clock signal.
+ Else, on the positive edge of the clock, the stored value is updated at the output.

 `gvim dff_asyncres_syncres.v`
 
<img width="445" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/582609c7-faf6-4981-9643-ec5ad543b65f">

**D Flip_Flop with Asynchronous Set**
+ When the set is high, the output of the flip-flop is forced to 1, irrespective of the clock signal.
+ Else, on positive edge of the clock, the stored value is updated at the output.

`gvim dff_async_set.v`

<img width="357" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/f45ca71f-8eef-402a-a966-9035a51fa21d">

**D Flip-Flop with Synchronous Reset**
+ When the reset is high on the positive edge of the clock, the output of the flip-flop is forced to 0.
+ Else, on the positive edge of the clock, the stored value is updated at the output.

  `gvim dff_syncres.v`

<img width="409" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d22a7aa2-059f-48bd-b0c4-32a294248c8b">

**D Flip-Flop with Asynchronous Reset and Synchronous Reset**
+ When the asynchronous resest is high, the output is forced to 0.
+ When the synchronous reset is high at the positive edge of the clock, the output is forced to 0.
+ Else, on the positive edge of the clock, the stored value is updated at the output.
+ Here, it is a combination of both synchronous and asynchronous reset DFF.

`gvim dff_asyncres_syncres.v`

<img width="439" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8ee2f2a5-31e9-447c-a23f-b347fc7b642c">

</details>

<details>
<summary> Lab Flop Synthesis Simulations </summary>	

**D Flip-Flop with Asynchronous Reset**
+ **Simulation**
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `iverilog dff_asyncres.v tb_dff_asyncres.v`
  - `./a.out`
  - `gtkwave tb_dff_asyncres.vcd`
  
<img width="549" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c114ede9-357a-4d75-9f4a-dea6fd71f1ce">

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/326bf88d-74d9-407f-8c45-1e1e28ea1911">

+ **Synthesis**
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_asyncres.v`
  - `synth -top dff_asyncres`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show`

    <img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/92f225cf-a014-4a89-be7a-a9560a6d6359">

 **D Flip_Flop with Asynchronous Set**
 + **Simulation**
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_async_set.v tb_dff_async_set.v`
   - `./a.out`
   - `gtkwave tb_dff_async_set.vcd`

<img width="551" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3d0eebd4-1d03-4bdb-9f76-4907b8b87ac3">


<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/51dd2cf5-ea6c-4b00-bf2a-5ae8674e2272">

+ **Synthesis**
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_async_set.v`
  - `synth -top dff_async_set`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show` 

<img width="922" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/87e93a5e-c904-4eca-b3a7-4657c8f8f0cc">

**D Flip-Flop with Synchronous Reset**
+ **Simulation**
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_syncres.v tb_dff_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_syncres.vcd`
 
     
   <img width="542" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bd4493f9-da25-45ce-b9a6-660944032e75">
   

  <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/472e9a2d-bb95-437d-b790-cfe72294ad07">
  

+ **Synthesis**
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `yosys`
  - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `read_verilog dff_syncres.v`
  - `synth -top dff_syncres`
  - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
  - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
  - `show`

<img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/ff5b11e7-11a8-40c9-9e08-e090eeb0f547">

</details>

<details>
<summary> Interesting Optimisations </summary>	

+ `gvim mult_2.v`

 <img width="434" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d37ce39a-16c6-428a-a6be-ef6a5fc3c2aa">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog mult_2.v`
+ `synth -top mul2`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/05011316-bfc4-41c3-8e87-46855d117243">

+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="305" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fb4d176c-0d06-43e3-bad9-7945e02c2889">

+ `write_verilog -noattr mul2_netlist.v`
+ `!gvim mul2_netlist.v`
  
 <img width="436" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9a0eca57-0656-4cb3-99f0-ad7a0d0f356e">

+ `gvim mult_8.v`

  <img width="443" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3f9fa46f-56b9-43bf-8d46-325d75f76a95">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib  `
+ `read_verilog mult_8.v`
+ `synth -top mult8`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/13359e0d-0676-4313-b791-3992655ee4f7">

+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4c8b811f-b793-45fa-a8e7-a65663ef3f74">

+ `write_verilog -noattr mult8_netlist.v`
+ `!gvim mult8_netlist.v`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/37c89aea-497d-4e0d-99c5-c46dffd63b7d">

</details>

# Day 5
## Introduction to Optimisations 

<details>
<summary> Combinational Optimisation </summary>
	
+ Combinational logic refers to logic circuits where the outputs depend only on the current inputs and not on any previous states.
+ Combinational optimization is a field of study in computer science and operations research that focuses on finding the best possible solution from a finite set of options for problems that involve discrete variables and have no inherent notion of time.
+ Optimising the combinational logic circuit is squeezing the logic to get the most optimized digital design so that the circuit finally is area and power efficient.
+ Techniques for Optimisations:
  - **Constant propagation** is an optimization technique used in compiler design and digital circuit synthesis to improve the efficiency of code and circuit implementations by replacing variables or expressions with their constant values where applicable.
  - **Boolean logic optimization**, also known as logic minimization or Boolean function simplification, is a process in digital design that aims to simplify Boolean expressions or logic circuits by reducing the number of terms, literals, and gates required to implement a given logical function.

</details>

<details>
<summary> Sequential Logic Optimisations </summary>	

+ Sequential logic optimizations involve improving the efficiency, performance, and resource utilization of digital circuits that include memory elements like flip-flops and latches.
+ Optimizing sequential logic is crucial in ensuring that digital circuits meet timing requirements, consume minimal power, and occupy the least possible area while maintaining correct functionality.
+ Optimisation methods:
  - **Sequential constant propagation**, also known as constant propagation across sequential elements, is an optimization technique used in digital design to identify and propagate constant values through sequential logic elements like flip-flops and registers. This technique aims to replace variable values with their known constant values at various stages of the logic circuit, optimizing the design for better performance and resource utilization.
  - **State optimization**, also known as state minimization or state reduction, is an optimization technique used in digital design to reduce the number of states in finite state machines (FSMs) while preserving the original functionality.
  - **Sequential logic cloning**, also known as retiming-based cloning or register cloning, is a technique used in digital design to improve the performance of a circuit by duplicating or cloning existing registers (flip-flops) and introducing additional pipeline stages. This technique aims to balance the critical paths within a circuit and reduce its overall clock period, leading to improved timing performance and better overall efficiency.
  - **Retiming** is an optimization technique used in digital design to improve the performance of a circuit by repositioning registers (flip-flops) along its paths to balance the timing and reduce the critical path delay. The primary goal of retiming is to achieve a shorter clock period without changing the functionality of the circuit.
 
</details>

## Combinational Logic Optimisations

<details>
<summary> opt_check </summary>	
	
+ `gvim opt_check.v`

  <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/dad0961e-10d4-4a0c-9991-0ad6daea169f">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check.v`
+ `synth -top opt_check`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/44d6a65e-1405-49b6-a569-66a7c976308c">

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8861528b-55be-45e4-952e-c0600c811685">

</details>

<details>
<summary> opt_check2 </summary>	
	
+ `gvim opt_check2.v`

  <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d957a7b5-fb8a-4e59-a9d3-cb1730a7dd25">
  
+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check2.v`
+ `synth -top opt_check2`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c85299a9-10df-4b40-8f0f-f19ead681ad3">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d0b4fb18-71ff-4aa6-92b9-49eac8dd889b">

</details>

<details>
<summary> opt_check3 </summary>	
	
+ `gvim opt_check3.v`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3183db65-f77d-443a-9814-dc776c3c0990">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check3.v`
+ `synth -top opt_check3`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/13709061-55c2-43ca-b798-c8398e1c7fdb">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/2c885b4d-c274-4bae-abd0-15853f864f62">

</details>

<details>
<summary> opt_check4 </summary>
	
+ `gvim opt_check4.v`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/75c65195-8f6b-416e-8074-306a46263746">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog opt_check4.v`
+ `synth -top opt_check4`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a1acd352-c271-4330-9fd8-6aafe72b8f11">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/498cf442-ec8e-468e-a310-d1f93b93ce1a">

</details>

<details>
<summary> multiple_module_opt </summary>
	
+ `gvim multiple_module_opt.v`

 <img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/ad570bd8-44b5-4408-8715-02f1c5d15a29">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog multiple_module_opt.v`
+ `synth -top multiple_module_opt`
+ `opt_clean -purge`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`
 
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4c3fd4bc-c599-41cf-af42-c07280dcca11">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1344d22d-51f5-439e-bc34-96b2a742474e">

</details>

## Sequential Logic Optimisations

<details>
<summary> dff_const1 </summary>	

+ `gvim dff_const1.v`

<img width="331" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/abec2938-5f2c-4cd5-b369-103c1b09f098">

**Simulation**

+ `iverilog dff_const1.v tb_dff_const1.v`
+ `/a.out`
+ `gtkwave tb_dff_const1.vcd`

<img width="572" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/551d623c-c25c-4c42-882f-7455f451e752">

<img width="503" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/51301173-fdbd-476c-842e-2d08078f020d">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const1.v`
+ `synth -top dff_const1`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="194" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c542c8b4-3624-4a22-92c5-35a4b1458c35">

<img width="925" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/fa1d8b2f-431e-4836-8a75-8c2bd3ce326e">

</details>

<details>
<summary> dff_const2 </summary>	

+ `gvim dff_const2.v`

<img width="355" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e0e6e4da-0429-49db-b687-d99ab365ed17">

**Simulation**

+  `iverilog dff_const2.v tb_dff_const2.v`
+ `/a.out`
+ `gtkwave tb_dff_const2.vcd`

<img width="535" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d50ca5c4-3cf0-45ce-a987-07c10a9bc737">

 <img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a90d628f-dd7d-4ae6-8b4d-072b6a9960b9">

 **Synthesis**
 
+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const2.v`
+ `synth -top dff_const2`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="206" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d4859923-36a2-4cf2-bcef-6befaf718913">

<img width="305" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8e3503dd-d315-426f-9a3e-bd487014600a">

</details>

<details>
<summary> dff_const3 </summary>

+ `gvim dff_const3.v`

 <img width="272" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/3ce28559-0063-4ef1-9d7e-a3af839dd7e3">

**Simulation**

+ `iverilog dff_const3.v tb_dff_const3.v`
+ `/a.out`
+ `gtkwave tb_dff_const3.vcd`

<img width="519" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9f8b58c1-3f03-4bad-a238-062c751f5401">

<img width="502" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/aed6c933-5c06-4687-ba9e-9c782626c030">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const3.v`
+ `synth -top dff_const3`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="197" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7cc2308b-b988-4ba9-965f-06abf2472e2b">

<img width="922" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bdea6f33-d357-47f4-a9fd-cc655dcce869">

</details>

<details>
<summary> dff_const4 </summary>	

+ `gvim dff_const4.v`

<img width="311" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bc5661c4-50c6-4ccf-8aab-a5ace3ccfa14">

**Simulation**

+ `iverilog dff_const4.v tb_dff_const4.v`
+ `/a.out`
+ `gtkwave tb_dff_const4.vcd`

<img width="530" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c51fb049-bb70-477a-8aa4-9951d1ea684c">

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1a9ee230-2ad6-4c92-8e37-0a753832180f">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const4.v`
+ `synth -top dff_const4`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="193" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a152102c-a880-499d-98e6-f2d26201ea85">

<img width="306" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/4d4d33fc-11ec-4cb5-867d-2f34d892255a">

</details>

<details>
<summary> dff_const5 </summary>	

+ `gvim dff_const5.v`

<img width="251" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/af7acfca-6fb0-4b62-bb1e-d32746d0c07e">

**Simulation**

+ `iverilog dff_const4.v tb_dff_const4.v`
+ `/a.out`
+ `gtkwave tb_dff_const4.vcd`

<img width="529" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e27a9ee5-6332-4147-8bf9-c246ca7d7996">

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7eb3b371-189e-483c-80d9-37d38c062cd2">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog dff_const4.v`
+ `synth -top dff_const4`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="205" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/e2719af7-b746-4830-b04f-87df97143f86">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8d95c49d-9fd9-4d76-bba1-b893c6f163fc">

</details>

## Sequential Optimisations for Unused Outputs
<details>
<summary> counter_opt </summary>

 + `gvim counter_opt.v`

<img width="349" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/cb5798fa-2ee9-4cf0-9372-3da9ff17bd66">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog counter_opt.v`
+ `synth -top counter_opt`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="184" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/1c876b33-9d26-4efe-95cf-5d0814415da5">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/b65d5ac8-3961-4a7b-9e8a-18bc0229f104">

</details>

<details>
<summary> counter_opt2 </summary>	

+ `gvim counter_opt2.v`

 <img width="347" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/b6262d9a-5892-4360-91fa-18f7e2aa39e7">

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog counter_opt2.v`
+ `synth -top counter_opt2`
+ `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

 <img width="200" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/14aadea7-9607-40a8-b5ed-e48eb255cd10">

<img width="923" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/78af2250-6ee8-4d94-b91b-138cb2877b1e">

</details>

# Day 6
## GLS Synthesis-Simulation Mismatch and Blocking Non-blocking Statements

<details>
<summary> GLS Concepts And Flow Using Iverilog </summary>	

 + **Gate Level Simualtion**
   - Gate-level simulation is a technique used in digital design and verification to validate the functionality of a digital circuit at the gate-level implementation.
   - It involves simulating the circuit using the actual logic gates and flip-flops that make up the design, as opposed to higher-level abstractions like RTL (Register Transfer Level) descriptions.
   - This type of simulation is typically performed after the logic synthesis process, where a high-level description of the design is transformed into a netlist of gates and flip-flops.
   - We perform this to verify logical correctness of the design after synthesizing it. Also ensuring the timing of the design is met.
  
<img width="608" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/6298b067-2f45-4dbc-ad25-762ac3d8be63">

+ **Synthesis-Simulation Mismatch**
  - A synthesis-simulation mismatch refers to a situation in digital design where the behavior of a circuit, as observed during simulation, doesn't match the expected or desired behavior of the circuit after it has been synthesized.
  - This discrepancy can occur due to various reasons, such as timing issues, optimization conflicts, and differences in modeling between the simulation and synthesis tools.
  - This mismatch is a critical concern in digital design because it indicates that the actual hardware implementation might not perform as expected, potentially leading to functional or timing failures in the fabricated chip.

+ **Blocking Statements**
  - Blocking statements are executed sequentially in the order they appear in the code and have an immediate effect on signal assignments.
  - Example:

  ``` v
   module BlockingExample(input A, input B, input C, output Y, output Z);
    wire temp;

    // Blocking assignment
    assign temp = A & B;

    always @(posedge C) begin
        // Blocking assignment
        Y = temp;
        Z = ~temp;
    end
   endmodule
  ```

+ **Non-Blocking Statements**
  - Non-blocking assignments are used to model concurrent signal updates, where all assignments are evaluated simultaneously and then scheduled to be updated at the end of the time step.
  - Example:
   ``` v
    module NonBlockingExample(input clock, input D, input reset, output reg Q);

    always @(posedge clock or posedge reset) begin
        if (reset)
            Q <= 0;  // Reset the flip-flop
        else
            Q <= D;  // Non-blocking assignment to update Q with D on clock edge
    end
  endmodule
   ```

+ **Caveats with Blocking Statements**
  + Blocking statements in hardware description languages like Verilog have their uses, but there are certain caveats and considerations to be aware of when working with them. Here are some important caveats associated with using blocking statements:
    - Procedural Execution: Blocking statements are executed sequentially in the order they appear within a procedural block (such as an always block). This can lead to unexpected behavior if the order of execution matters and is not well understood.
    - Lack of Parallelism: Blocking statements do not accurately represent the parallel nature of hardware. In hardware, multiple signals can update concurrently, but blocking statements model sequential behavior. As a result, using blocking statements for modeling complex concurrent logic can lead to incorrect simulations.
    - Race Conditions: When multiple blocking assignments operate on the same signal within the same procedural block, a race condition can occur. The outcome of such assignments depends on their order of execution, which might lead to inconsistent or unpredictable behavior.
    - Limited Representation of Hardware: Hardware systems are inherently concurrent and parallel, but blocking statements do not capture this aspect effectively. Using blocking assignments to model complex combinational or sequential logic can lead to models that are difficult to understand, maintain, and debug.
    - Combinatorial Loops: Incorrect use of blocking statements can lead to unintentional combinational logic loops, which can result in simulation or synthesis errors.
    - Debugging Challenges: Debugging code with many blocking assignments can be challenging, especially when trying to track down timing-related issues.
    - Not Suitable for Flip-Flops: Blocking assignments are not suitable for modeling flip-flop behavior. Non-blocking assignments (<=) are generally preferred for modeling flip-flop updates to ensure accurate representation of concurrent behavior.
    - Sequential Logic Misrepresentation: Using blocking assignments to model sequential logic might not capture the intended behavior accurately. Sequential elements like registers and flip-flops are better represented using non-blocking assignments.
    - Synthesis Implications: The behavior of blocking assignments might not translate well during synthesis, leading to potential mismatches between simulation and synthesis results.

</details>

## Labs on GLS and Synthesis-Simulation Mismatch
<details>
<summary> ternary_operator_mux </summary>	

+ `gvim teranry_operator_mux.v`

<img width="370" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/8539ab94-8f5a-4bff-8465-eb8bb6ca83b8">

**Simulation**

+ `iverilog ternary_operator_mux.v tb_ternary_operator_mux.v`
+ `./a.out`
+ `gtkwave tb_ternary_operator_mux.vcd`

<img width="626" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/893dc1c8-bc64-41bf-bb35-ee83e37b023d">

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c675c505-880e-4c15-b079-3c528032c279">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog ternary_operator_mux.v`
+ `synth -top ternary_operator_mux`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/74fa07aa-5dc3-4f04-8fc1-babe67ded667">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9a4f4ebd-370f-45b5-a1c1-cd95b8e1e556">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

<img width="928" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/97f59e19-d561-4c1e-b8b5-46fb1eb21595">

<img width="498" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5c4652e6-8364-4e81-9cd3-f1795f5d321a">

</details>

<details>
<summary> bad_mux </summary>	

 + `gvim bad_mux.v`

 <img width="290" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/deb388a2-8463-410b-b16e-5eaf81697d69">

**Simualtion**

+ `iverilog bad_mux.v tb_bad_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

<img width="501" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9c68b293-6f55-4742-bb06-5cdf9551a5ae">

<img width="500" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/46266c26-99ce-4a79-9e5c-9558ea15f407">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog bad_mux.v`
+ `synth -top bad_mux`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/a19eb270-87dd-40cc-95f8-3bd3cf02a396">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d15147f9-775d-44bb-93a5-d7249645d9bc">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux_net.v tb_bad_mux.v`
+ `./a.out`
+ `gtkwave tb_bad_mux.vcd`

<img width="878" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/29d0b4bd-2874-4809-bf2b-728a73cccc09">
  
<img width="501" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/9d51d787-22d3-4495-95cc-c87c0ef71d17">

</details>

## Labs on Synth-Sim Mismatch for Blocking Statement

<details>
<summary> blocking_caveat </summary>	

+ `gvim blocking_caveat.v`

<img width="327" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/5827ea02-ec07-4164-9b9f-b064750ede9d">

**Simualtion**

+ `iverilog blocking_caveat.v tb_blocking_caveat.v`
+ `./a.out`
+ `gtkwave tb_blocking_caveat.vcd`

<img width="567" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/09e0265c-b794-4d3f-9e27-4403a6b9122a">

<img width="501" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c3b18d2e-d407-45c4-9e97-ec59042ec2bd">

**Synthesis**

+ `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `read_verilog blocking_caveat.v`
+ `synth -top blocking_caveat`
+ `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `show`

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7f942ace-02b0-4421-8d20-5e7126cbb3df">

<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/d660d89b-8a9a-43d3-9e78-ab1f7054a667">

**GLS to Gate-Level Simulation**

+ `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat_net.v tb_blocking_caveat.v`
+ `./a.out`
+ `gtkwave tb_blocking_caveat.vcd`

<img width="926" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c541ebb5-b42d-4629-b12a-734541df3071">

<img width="503" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/c78704db-de4c-4958-880f-0747f78090d9">

</details>
