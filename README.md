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
   - Yosys 1 good mux 
  
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

**good_mux.v**

``` v
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
**tb_good_mux.v**

``` v
timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

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
  
<img width="269" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/bc2242db-49e8-4c19-a06e-8f8e82f55729">

+ In a sequential circuit, clock period depends on:
  - Clock to Q of flip-flop A.
  - Propagation delay of combinational circuit.
  - Setup time of flip-flop B.

<img width="142" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/112de4cd-6e0c-46ec-ad94-0cb6540af7e1">

+ **Why need fast and slow cells?**
  - To ensure that there are no HOLD issues at flip-flop B, we require slow cells.
  - For a smaller propagation time, we need faster cells.

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
     
   - To view a smaller code
     
     ` write_verilog -noattr good_mux_netlist.v`
     
     `!gvim good_mux_netlist.v`
  
  
<img width="400" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/74fc2a01-3c35-4db1-8220-96595c6c236e">

<img width="479" alt="image" src="https://github.com/Veda1809/pes_asic_class/assets/142098395/7adc16f5-f635-4532-b90c-a9f9c496f95f">


</details>
