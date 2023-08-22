# RISC-V

<details>
<summary>Installation steps</summary>
Below are the steps and commands to install risc-v toolchain

```bash
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
cd riscv_workshop_collaterals
chmod 755 run.sh
./run.sh
```
Once the cloning is done and if there is not any error then set the PATH variable in 
.bashrc file using below commands

```
gedit .bashrc
export PATH="/home/user/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14/bin:$PATH" #Instead of user replace it with your user name
#save and close the bashrc
source .bashrc
```
Now try the "riscv64-unknown-elf-gcc" command and if there is any error shows below 
is how to debug: If you are getting the error about "iverilog" then use below commands

```
sudo apt-get install libboost-regex-dev
git clone https://github.com/steveicarus/iverilog.git
cd iverilog/
git checkout --track -b v10-branch origin/v10-branch
git pull 
chmod 777 autoconf.sh 
./autoconf.sh 
./configure 
make
sudo make install 
```

If you are getting the error about "riscv-pk" then use below commands

```
sudo apt-get install libboost-regex-dev
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk/
mkdir build
cd build/
../configure --prefix=$pwd/riscv_toolchain/riscv64-unknown-elf-gcc-8.3.0-2019.08.0-x86_64-linux-ubuntu14 --host=riscv64-unknown-elf
make
sudo make install
```

If there is error showing that "Spike-command is not found" when running the spike, Try running run.sh again , it will be resolved.  

Don't forget to add PATH in .bashrc and source the .bashrc file  
  
Acknowledgement : Bhargav D V , Alwin Shaju, Emil Jayanth Lal, Kanish R, Divyam Satle : Colleauges(IIIT-B)
</details>

## Day 1

<details>
<summary>Overview  
</summary>RISC-V is an open-source instruction set architecture (ISA) used for the development of custom processors targeting a variety of end applications. The flow
of this architecture from application software or apps to the hardware and there is
system software block which consists of os, compiler and assembler and the flow is as follows: Os which handle IO operations, allocate memory and low level synthesis functions.
Compiler converts c,c++, java to instructions and then assembler converts this instructions
into the binary data which hardware can understand. Below shown the diagram

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/bd3dedc1-8163-4931-ae31-5b1b74f7f382)


</details>

<details><summary>
Integer number representation
</summary>
The 64-bit number system for unsigned numbers is a fundamental concept in computer science and digital systems. It is an integral part of modern computing architectures and plays a crucial role in representing and manipulating numerical data. This number system is based on the binary (base-2) numeral system, which uses only two symbols, typically 0 and 1, to represent all numbers. In the context of a 64-bit number system, each number is composed of 64 binary digits, commonly referred to as "bits."
The number of bits determines the range of values that can be represented. For a 64-bit system(RISC-V doubleword), the range of possible values for an unsigned number is from 0 to 2^64 - 1.

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/4e73d6a2-81c4-4d20-95dd-9470f66f36c6)

![unsignrisc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/5a1d03a5-585e-4e68-bf8f-74ee436b1786)


64-bit signed number system: The 64-bit signed number system is another crucial aspect of computer science and digital systems. It's an extension of the 64-bit unsigned number system that allows the representation of both positive and negative integers using binary digits. In this system, the leftmost bit (most significant bit) is used as the sign bit, determining whether the number is positive or negative. The remaining 63 bits represent the magnitude of the number.

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/fea22a66-d184-4254-a786-8406fd36044c)


</details>

<details><summary>RISCV gcc compilation and assembly </summary>
Below is the command to compile the c code through riscv compiler

```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o 1ton.o 1ton.c
```

![sum1ton-main](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/edfbdff1-45c6-4db7-9cf6-28a8e9032aae)

![sum1ton](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f1bab766-3da2-48b3-8210-c1a73bffecfa)

![Ofast](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/3a807239-f7b1-4966-9124-6b456c69eb77)


Below command is to observe the result

```
riscv64-unknown-elf-objdump -d 1ton.o
```
Get the output file using spike  
Below is the command to get the object output
```
spike pk 1ton.o
```

![1ton-spikepk](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/fdcd8d89-d12f-4b7f-afe6-8f196b56b8d2)

To debug the output 

```
spike -d pk 1ton.o
```

Now to observe the file and memory locations use following commands  

```
until pc 0 100b0
reg 0 a1
```
![untilpc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/2f088c10-49c0-4222-ac17-2ada219c8a95)

Below is the architecture

![pk-arch](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/477726ca-94cb-4642-b5bd-71f29fece4c5)


</details>

## Day 2

<details><summary>Application Binary Interface
</summary>
Application binary interface (ABI) is an interface between two binary program modules. Often, one of these modules is a library or operating system facility, and the other is a program that is being run by a user.  
  
An ABI defines how data structures or computational routines are accessed in machine code, which is a low-level, hardware-dependent format. In contrast, an application programming interface (API) defines this access in source code, which is a relatively high-level, hardware-independent, often human-readable format. A common aspect of an ABI is the calling convention, which determines how data is provided as input to, or read as output from, computational routines.  

Here below shown the diagram

![ABI](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/81e17793-c86e-476b-be5b-7c8cb6dd9b74)

![thisisABI](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f5811a26-4fe6-4332-b6d3-acf3e147a1b1)


Memory allocation for double words typically involves reserving contiguous blocks of memory in a computer's RAM (Random Access Memory) to store data that is twice the size of a standard word, which is often 32 bits or 4 bytes on many computer architectures. Double words are typically 64 bits or 8 bytes in size. This allocation process is fundamental in computer programming, as it allows for the efficient storage and manipulation of larger data structures and numeric values, such as long integers or floating-point numbers with higher precision. When allocating memory for double words, it's essential to ensure proper alignment, so the memory addresses are consistent with the system's architecture, as misaligned memory access can result in performance penalties or even program crashes.  

![ABI-registers](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/3ee1b562-6e89-4ab6-8268-33838c825a93)

Load and store single register instructions can transfer a 32-bit word, a 16-bit halfword, or an 8-bit byte between memory and a register. Byte and halfword loads can be automatically zero extended or sign extended as they are loaded.

Load and store instructions have three primary addressing modes:
  
offset
  
pre-indexed
  
post-indexed.
  
The address is formed by adding or subtracting an immediate or register- based offset to or from a base register. Register-based offsets can also be scaled with shift operations. Pre-indexed and post-indexed addressing modes update the base register with the result of the offset calculation.

Below shown the representation 

![load](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/2c9b3151-1d3c-4c6f-98f6-78760cc46bef)

![add](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/4bebbace-7d9f-4ef3-8381-84fa88e5d941)

![store](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/fe8782e7-d3ca-4164-9cf7-f356a821dcc5)


</details>
<details>
  <summary>ABI function cells</summary>

Below is the custom file: 

![custom-main](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/97a2eca9-5150-47c3-a8df-bfb974804300)

Below is the objdump:

![objdump](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/d9a7d029-3037-4326-9219-22d65822386d)

Below is using spike command: 

![spike1to9](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/cfd9cf42-d77c-4024-b323-8d0405495e9f)

![firmwarehex](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/b7596c64-19d4-487a-bdbf-4ba95855cbae)

Below is another method command:

![rv32im](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/44fba369-9ac0-43e1-8177-932378b42152)

Below is the conclusion: 

![conclusion1](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/186ae721-39f1-489b-b866-4d9a178030dc)


</details>

## Day 3 (Digital Logic with TL-Verilog and Makerchip)

<details><summary>Combinational logic in TL-Verilog using Makerchip</summary>
Below shown logic gates representation and their truth tables

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/d78dcd40-5703-4c95-96b0-7257bc2e5b24)

Consider below full adder circuit which shows interconnection of logic gates to get the output S(sum) and Cout

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/54cf8cb5-7e8a-4f0a-b3f9-008c4fd06735)

Below shown representation of boolean operators:  

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/318c3594-331a-4c81-9451-e21115f16593)

To write code of mux in verilog 

```
assign f = s ? x1 : x2;
```

**Makerchip IDE**  
Go to the makerchip.com there are several examples below shown some of the examples  (**Combinational logic**)
Below shown multiplexer  

![mux](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/68b292bb-9e27-419e-932d-575375805237)

Below shown FPGA multiplier:  

![fpga-mult](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/3e63ff17-0d9c-47f0-95a0-32a2bd1492d2)

Below shown ripple carry :  

![ripplecarry](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/1e71e8cc-b3c1-4822-88a1-bf771daf6925)

Below is adder:  

![adder](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/be99b02b-56b6-4fe0-86e5-589f821b6ac7)

</details>

<details><summary>Sequential circuits</summary>
 Sequential circuits are digital circuits that store and use the previous state information to determine their next state.  

    
 Sequential circuits are commonly used in digital systems to implement state machines, timers, counters, and memory elements. The memory elements in sequential circuits can be implemented using flip-flops, which are circuits that store binary values and maintain their state even when the inputs change.  

  ![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/c0172920-48bb-462a-9c72-7e1bed0497dc)

Below shown makerchip of fibonacci series:  

![fibbonaci](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/a5ed1ba0-2dcf-4143-b602-7605366e3df6)

Below is the representation of counter: 

![counter](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/9b1e1876-641f-4d88-bf31-2b5a865d79e1)

Below is sequential calculator:  

![seqcalc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/84ee72d0-9c9b-48cb-ac7e-20757675264f)


</details>

<details><summary>Pipelined Logic</summary>

Below shown pipeline logic:  

![pipelinelogic](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/c6205460-b625-45c3-88ec-0a4aff90e960)

Below is pythagorans thm makerchip implementation:  

![pythagor-thm](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/840a6611-29f8-4c3b-bec3-432682bf6561)

Here below shown errorpipe implementation :  

![Errorpipe](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/db2d409b-bbb6-4eca-8097-e6e01c6dafcd)


Here is difference between TL-verilog and system verilog representation whish shows code reduction:  

![TL-Systemveri](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/7a37e34d-ed16-41e2-94f6-38d091e54eed)

Here below shown diagram Fibonacci in a pipeline :  

![fibbpipe](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/ac777063-87d4-4e51-b020-4337457e869d)

Below is makerchip implementation:  

![fibbocode](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/9c043ba1-96d0-4bb7-878a-b430781639ab)

Below is Counter and Calculator in pipeline:  

![countcalc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/5646b4bf-d5b6-4c06-b37e-5c6f5ed88d3f)

Below shown cyclic calculator diagram:  

![cycliccalc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/2690964f-2536-467a-b6a8-dc995616f45b)

Below is makerchip implementation of counter calculator:  

![countcalccode](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/696755f0-dbda-45f3-9b61-249542d928d5)

Below is makerchip implementation of two cycle calculator: 

![2cyclecalc](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f82547c7-41d4-4597-ab57-a783835ede09)


</details>

<details><summary>Validity</summary>

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/88fe97ed-2f16-4c29-a40a-ac3647edc20d)

Below shown diagram of total distance calculator: 

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/e8305d16-7591-4492-b5f5-360431bb7b72)

Below is makerchip implementation of total_dist calculator:  

![total_dist](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/2baec529-40f0-4a49-9864-1669f6dfba37)

Below shown makerchip implementaion of pythagorans thm validity:  

![Valditypythagor-pipelined](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/82073eda-dac3-400c-b3f6-839296dad84a)


Below shown the structure of the two cycle calculator with validity:  

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/272c5fce-15bf-45f3-a1aa-9ec8fcc8ee3b)

And below is its makerchip implementation:  

![valdity2-cycle](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f28892d0-99ce-46b2-8bfb-c554864ab8a0)

Below shown the structure of the calculator with single value memory :  

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/0b46c36a-a5c2-4a02-b39f-57b227769ccf)

And below is it's makerchip implementation:  

![single-memory](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/4b360d0e-f437-48ae-975a-a71da4b389cc)

Below is makerchip implementation of Conway's Game of Life :  

![conways game of life](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/88e04801-4e0b-404d-8c13-a7bd0a1b1086)


</details>

## Day 4 (Basic RISC-V CPU micro-architecture)

<details><summary>Introduction</summary>
  
The term architecture describes the functional specification of a processor. It describes what functionality the software can rely on the hardware to provide. Architecture does not tell you how a processor is built. It tells you what a processor can do. Micro-architecture on the other hand describes how a processor is built and designed. Micro-architecture defines, the number and size of caches, cycle counts of instructions, pipeline length, and more.

  Below shown micro-architecture: 
  
  ![Microarch](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/bc5ad178-b926-48da-9937-bafc014ece78)

  ![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/e9e804b1-f584-4003-970a-fb4a5615c941)

Below is makerchip implementation:  

![top_cpu](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/9c35f02a-536b-4960-bec1-1927fb6bf587)



</details>
<details><summary>Instruction Fetch and Decode</summary>

Below is startpoint: 

![startpoint1](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/fff99b07-c8ff-4e67-97c0-0c39665dc0c3)


Below is makerchip implementation of Instruction fetch:

![logic-fetch1](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f1b55f1b-d166-4178-92ca-053dbc21cc8d)

Below is instruction fetch logic2: 

![logic-fetch2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/5068305e-0cd2-4b70-a309-bf8b33ed523f)

Below shown diagram of instruction Decode where ALU RF read and RF write is there: 

![instruct-decode](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/b5d50541-2d9a-4576-8207-bcb41889328e)

Below showed complet circled instructions: 

![decodeIndInstruct](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/6424be25-ce86-48c6-aafc-07baadc7ba69)

Here is instr[6:2] determine instruction type which are I, R, S, B, J, U: 

![instruction_decode2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/50906c44-be78-4fe5-b15d-55e1fb437623)


Below is makerchip implementation:

![decodeinstruct2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/f1be9023-7f27-4f9f-a301-ce748901f314)

Below shown immediate decode logic makerchip implementation: 

![decodeinstruct(immediate)](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/20b3a216-de02-4a14-a028-10aa6ab5e2cf)

Decode other fields of instructions :   
Here below shown I, S, B , U, J-immediate instruction in below diagram:
  

![decode-other-fields](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/d253e64b-cf6a-4df4-afdf-4b1185daec44)


</details>

<details><summary>Control logic</summary>
Here below shown register file read diagram:
  
![regFileRead](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/9ce4bba5-1e99-48da-be9a-4301f6a260be)

![diagRegFileRead](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/c506597b-69a9-4e85-ab47-3b893a0649f1)

Below shown makerchip implementation:  

![regRead1](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/98beda1e-5d10-4206-b187-74aace04256f)

Here is register read file2 : 

![Regreadpart2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/5e9ad605-4716-418c-8fdd-28e2e86dbe5d)

Below its makerchip implementation:  

![regRead2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/1299c6a7-fea2-42e1-8fb7-14694f4e79ca)

Below shown ALU diagram for operation add/addi:  

![AluDiag](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/20f733df-3ec9-41e5-a263-9d0cdd02240d)

And below is its makerchip implementation:  

![AluImplem](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/bbb72830-f192-4ab1-944a-cb37e0dcfa00)

Here is reg file write diagram:  

![RegFileWrite](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/4d7012a6-5c16-4b3a-b30a-dcd3204e1fe5)


Below is its makerchip implementation:  

![RegWritecode](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/d53b8b25-970d-4637-9efd-5957d7bad1b7)

Now lets start with Branch instruction and to understand see below diagrams:  

![BranchInstruct](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/7a1a71fe-acf6-456e-a675-a9d769e3b0a1)

Below is its makerchip implementation:  

![BranchInstruct1](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/e5ab030f-a353-471d-9927-f515b162a1da)


![BranchIns2Diag](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/9360b89b-286b-4b17-abc0-5a4f97a62f35)

Makerchip implementation:  

![BranchInstruct2](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/5ac2b227-36ad-41e7-8b7c-9cc8a64579ea)

Now lets see about testbench:  

```
*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
```

![Infotestbench](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/46d3c1ef-0b38-458f-a663-70c763f5d923)

Below is its makerchip implementation:  

![testbench](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/94f7927e-6511-44c5-8311-0e219b034572)


</details>

## Day 5 (Complete Pipelined RISCV CPU micro-arch)

<details><summary>Pipelining the CPU </summary>

To understand the pipeline look below the waterfall logic diagram

![Alt text](image.png)

Where there are multiple stages in pipeline mode ex. stage-0, stage-1..  

Having 3 cycles delay rest all are pipelined.  
Here below is the code shown:  

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$taken_br) ? >>3$br_tgt_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $lui = $dec_bits ==? 11'bx_xxx_0110111;
         $auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $jal = $dec_bits ==? 11'bx_xxx_1101111;
         $jalr = $dec_bits ==? 11'bx_000_1100111;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $lui ? ({$imm[31:12], 12'b0}) :
                         $auipc ? $pc + $imm :
                         $jal ? $pc + 4 :
                         $jalr ? $pc + 4 : 32'bx;
                         
      // Register File Write
         $rf_wr_en = $valid ? (($rd == 5'b0) ? 1'b0 : $rd_valid) : 1'b0;     
         ?$rf_wr_en
            $rf_wr_index[4:0] = $rd[4:0];
      
         $rf_wr_data[31:0] = $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         
         
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      //m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```

Below is makerchip implementation:  

![Alt text](pipelining.png)


</details>

<details><summary>Load and Store</summary>

Below is the load-store diagram shown:  

![Alt text](image-1.png)

Below is the waterfall diagram:  

![Alt text](image-2.png)

Below is the code for load-store:  

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the value of r10 into address 17.
   m4_asm(LW, r17, r0, 10000)           // Load the value from 
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$taken_br) ? >>3$br_tgt_pc : 
                     (>>3$is_load) ? >>3$inc_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $lui = $dec_bits ==? 11'bx_xxx_0110111;
         $auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $jal = $dec_bits ==? 11'bx_xxx_1101111;
         $jalr = $dec_bits ==? 11'bx_000_1100111;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $lui ? ({$imm[31:12], 12'b0}) :
                         $auipc ? $pc + $imm :
                         $jal ? $pc + 4 :
                         $jalr ? $pc + 4 : 
                         ($is_load || $is_s_instr) ? $src1_value + $imm : 32'bx;
                         
      // Register File Write
         $rf_wr_en = ($rd_valid && $valid && $rd != 5'b0) || >>2$valid_load;
         ?$rf_wr_en
            $rf_wr_index[4:0] = !$valid ? >>2$rd[4:0] : $rd[4:0];
      
         $rf_wr_data[31:0] = !$valid ? >>2$ld_data[31:0] : $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         
      // Load
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         
         
      @4
         $dmem_rd_en = $valid_load;
         $dmem_wr_en = $valid && $is_s_instr;
         $dmem_addr[3:0] = $result[5:2];
         $dmem_wr_data[31:0] = $src2_value[31:0];
         
      @5   
         $ld_data[31:0] = $dmem_rd_data[31:0];
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic
                       // @4 would work for all labs
\SV
   endmodule
```

Below is the makerchip implementation:

![Alt text](load-store.png)


</details>

<details><summary>Complete final CPU</summary>

Below is the final code: 

```
\m4_TLV_version 1d: tl-x.org
\SV
   // This code can be found in: https://github.com/stevehoover/RISC-V_MYTH_Workshop
   
   m4_include_lib(['https://raw.githubusercontent.com/BalaDhinesh/RISC-V_MYTH_Workshop/master/tlv_lib/risc-v_shell_lib.tlv'])

\SV
   m4_makerchip_module   // (Expanded in Nav-TLV pane.)
\TLV
 m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the value of r10 into address 17.
   m4_asm(LW, r17, r0, 10000)           // Load the value from 
   
   // Optional:
   // m4_asm(JAL, r7, 00000000000000000000) // Done. Jump to itself (infinite loop). (Up to 20-bit signed immediate plus implicit 0 bit (unlike JALR) provides byte address; last immediate bit should also be 0)
   m4_define_hier(['M4_IMEM'], M4_NUM_INSTRS)

   |cpu
      @0
         $reset = *reset;
      
      //Fetch
         // Next PC
         $pc[31:0] = (>>1$reset) ? '0 : 
                     (>>3$valid_taken_br) ? >>3$br_tgt_pc : 
                     (>>3$valid_load) ? >>3$inc_pc : 
                     (>>3$valid_jump && >>3$is_jal) ? >>3$br_tgt_pc :
                     (>>3$valid_jump && >>3$is_jalr) ? >>3$jalr_tgt_pc : >>1$inc_pc;
         
         $imem_rd_en = !$reset;
         $imem_rd_addr[31:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         
      @1         
         $instr[31:0] = $imem_rd_data[31:0];
         $inc_pc[31:0] = $pc + 32'd4;  
      // Decode   
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                       $instr[6:2] ==? 5'b001x0 ||
                       $instr[6:2] == 5'b11001;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                       $instr[6:2] ==? 5'b10100 ||
                       $instr[6:2] ==? 5'b0110x;                       
         $is_b_instr = $instr[6:2] == 5'b11000;
         $is_u_instr = $instr[6:2] == 5'b0x101;
         $is_s_instr = $instr[6:2] == 5'b0100x;
         $is_j_instr = $instr[6:2] == 5'b11011;
         
         $imm[31:0] = $is_i_instr ? { {21{$instr[31]}} , $instr[30:20] } :
                      $is_s_instr ? { {21{$instr[31]}} , $instr[30:25] , $instr[11:8] , $instr[7] } :
                      $is_b_instr ? { {20{$instr[31]}} , $instr[7] , $instr[30:25] , $instr[11:8] , 1'b0} :
                      $is_u_instr ? { $instr[31:12] , 12'b0} : 
                      $is_j_instr ? { {12{$instr[31]}} , $instr[19:12] , $instr[20] , $instr[30:21] , 1'b0} : 32'b0;
         
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rs1_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_s_instr || $is_b_instr || $is_i_instr;
         $funct7_valid = $is_r_instr;
         
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
            
         $opcode[6:0] = $instr[6:0];
         
         $dec_bits[10:0] = {$funct7[5],$funct3,$opcode};
         
         // Branch Instruction
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         
         // Arithmetic Instruction
         $is_add = $dec_bits ==? 11'b0_000_0110011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_sltiu = $dec_bits ==? 11'bx_011_0010011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         
         // Load Instruction
         $is_load = $dec_bits ==? 11'bx_xxx_0000011;
         
         // Store Instruction
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         
         // Jump Instruction
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         
         $is_jump = $is_jal || $is_jalr;
         
      @2   
      // Register File Read
         $rf_rd_en1 = $rs1_valid;
         ?$rf_rd_en1
            $rf_rd_index1[4:0] = $rs1[4:0];
         
         $rf_rd_en2 = $rs2_valid;
         ?$rf_rd_en2
            $rf_rd_index2[4:0] = $rs2[4:0];
            
      // Branch Target PC       
         $br_tgt_pc[31:0] = $pc + $imm;
      
      // Jump Target PC
         $jalr_tgt_pc[31:0] = $src1_value + $imm;
         
      // Input signals to ALU
         $src1_value[31:0] = ((>>1$rd == $rs1) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data1[31:0];
         $src2_value[31:0] = ((>>1$rd == $rs2) && >>1$rf_wr_en) ? >>1$result : $rf_rd_data2[31:0];
         
      @3   
         
      // ALU
         $sltu_result = $src1_value < $src2_value ;
         $sltiu_result = $src1_value < $imm ;
         
         $result[31:0] = $is_addi ? $src1_value + $imm :
                         $is_add ? $src1_value + $src2_value : 
                         $is_or ? $src1_value | $src2_value : 
                         $is_ori ? $src1_value | $imm :
                         $is_xor ? $src1_value ^ $src2_value :
                         $is_xori ? $src1_value ^ $imm :
                         $is_and ? $src1_value & $src2_value :
                         $is_andi ? $src1_value & $imm :
                         $is_sub ? $src1_value - $src2_value :
                         $is_slti ? (($src1_value[31] == $imm[31]) ? $sltiu_result : {31'b0,$src1_value[31]}) :
                         $is_sltiu ? $sltiu_result :
                         $is_slli ? $src1_value << $imm[5:0] :
                         $is_srli ? $src1_value >> $imm[5:0] :
                         $is_srai ? ({{32{$src1_value[31]}}, $src1_value} >> $imm[4:0]) :
                         $is_sll ? $src1_value << $src2_value[4:0] :
                         $is_slt ? (($src1_value[31] == $src2_value[31]) ? $sltu_result : {31'b0,$src1_value[31]}) :
                         $is_sltu ? $sltu_result :
                         $is_srl ? $src1_value >> $src2_value[5:0] :
                         $is_sra ? ({{32{$src1_value[31]}}, $src1_value} >> $src2_value[4:0]) :
                         $is_lui ? ({$imm[31:12], 12'b0}) :
                         $is_auipc ? $pc + $imm :
                         $is_jal ? $pc + $imm :
                         $is_jalr ? $pc + $imm : 
                         ($is_load || $is_s_instr) ? $src1_value + $imm : 32'bx;
                         
      // Register File Write
         $rf_wr_en = ($rd_valid && $valid && $rd != 5'b0) || >>2$valid_load;
         ?$rf_wr_en
            $rf_wr_index[4:0] = !$valid ? >>2$rd[4:0] : $rd[4:0];
      
         $rf_wr_data[31:0] = !$valid ? >>2$ld_data[31:0] : $result[31:0];
      
      // Branch
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                     $is_bne ? ($src1_value != $src2_value) :
                     $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                     $is_bltu ? ($src1_value < $src2_value) :
                     $is_bgeu ? ($src1_value >= $src2_value) : 1'b0;
                     
         $valid_taken_br = $valid && $taken_br;
         
      // Load
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load || >>1$valid_jump || >>2$valid_jump);
      
      // Jump
         $valid_jump = $valid && $is_jump;
                  
      @4
         $dmem_rd_en = $valid_load;
         $dmem_wr_en = $valid && $is_s_instr;
         $dmem_addr[3:0] = $result[5:2];
         $dmem_wr_data[31:0] = $src2_value[31:0];
         
      @5   
         $ld_data[31:0] = $dmem_rd_data[31:0];
         
      // Note: Because of the magic we are using for visualisation, if visualisation is enabled below,
      //       be sure to avoid having unassigned signals (which you might be using for random inputs)
      //       other than those specifically expected in the labs. You'll get strange errors for these.

         `BOGUS_USE($is_beq $is_bne $is_blt $is_bge $is_bltu $is_bgeu)
   // Assert these to end simulation (before Makerchip cycle limit).
   *passed = |cpu/xreg[17]>>5$value == (1+2+3+4+5+6+7+8+9);
   *failed = 1'b0;
   
   // Macro instantiations for:
   //  o instruction memory
   //  o register file
   //  o data memory
   //  o CPU visualization
   |cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
   
   m4+cpu_viz(@4)    // For visualisation, argument should be at least equal to the last stage of CPU logic       
\SV
   endmodule
```

Below is the makerchip implementation:  

![Alt text](final.png)

![Alt text](image-3.png)

</details>

[Reference Section]:#
## References
1. https://github.com/kunalg123/riscv_workshop_collaterals
2. https://github.com/RISCV-MYTH-WORKSHOP/RISC-V-CPU-Core-using-TL-Verilog.git
