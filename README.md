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

Don't forget to add PATH in .bashrc and source the .bashrc file  
  
Acknowledgement : Bhargav D V , Colleauge(IIIT-B)
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


64-bit signed number system: The 64-bit signed number system is another crucial aspect of computer science and digital systems. It's an extension of the 64-bit unsigned number system that allows the representation of both positive and negative integers using binary digits. In this system, the leftmost bit (most significant bit) is used as the sign bit, determining whether the number is positive or negative. The remaining 63 bits represent the magnitude of the number.

![image](https://github.com/Pruthvi-Parate/RISC-V/assets/72121158/fea22a66-d184-4254-a786-8406fd36044c)


</details>

[Reference Section]:#
## References
1. https://github.com/kunalg123/riscv_workshop_collaterals
