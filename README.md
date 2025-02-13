# VSD_SquadronInternship
The program is based on the RISC-V architecture and uses open-source tools to teach people about VLSI chip design and RISC-V. The instructor for this internship is Kunal Ghosh Sir.

<details>
<summary><b>Task 1:</b> C based and RISC-V based programs for sum of n numbers</summary>   
<br>

C based
------------------------------------------

Install leafpad editor 

*Use the following command for installing leafpad*
```
sudo apt install leafpad
```
Now we need to write a program in c for sum of 1 to n numbers, and save the file as "sum1ton.c"

![c program sum1ton](https://github.com/user-attachments/assets/b180bdc1-1a9e-4b64-b215-1f6f199b9d8d)

Now after we compile this and run using the commands :

```
gcc sum1ton.c
./a.out
```
The output of the c code is :

![C sum1ton_output](https://github.com/user-attachments/assets/37f78ab9-44da-4f6a-ab16-8caafe2d0a61)

RISC-V based
------------------------------------------

We can view the sum code using the following command :
```
cat sum1ton.c
```
The terminal output of the above the commad :

![viewing_C_sumcode](https://github.com/user-attachments/assets/217bbee9-c294-48e4-9610-2883d24159fa)

For compiling the above code in RISC-V we use the command :
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
```

![o1_input](https://github.com/user-attachments/assets/c131b9bc-9874-49b2-91de-0706cc822201)


Now the file has been saved "sum1ton.o"
In the new tab we need to give the command ``` riscv64-unknown-elf-objdump -d sum1ton.o | less ```

Now the assembly language code for ```O1``` is :

![o1_output](https://github.com/user-attachments/assets/f21d9c9f-a1ed-42e7-b4d1-5ee00920266e)

Here if we calculate the number of instructions, we get the total instructions as 11.
It is calculated as 
``` 
101b0 - 10184 = 2c
2c/4 = b  => 11
```
Now similarly we need to execute the code for ``` Ofast ``` command

The input is shown as :

![Ofast_input](https://github.com/user-attachments/assets/540e85aa-e6cc-47ef-bdf0-20f368c8fa88)

The output of the ``` Ofast ``` command is :

![Ofast_output](https://github.com/user-attachments/assets/290aae34-f470-4972-ba2e-4a1d87828e40)

Again if we calculate the number of instructions , we get the instructions as 11.
It is calculated as 
``` 
100dc - 100b0 = 2c
2c/4 = b  => 11
```

-
</details>

------------------------------------

<details>
<summary><b>Task 2:</b> Simulating and Debugging C code with SPIKE </summary>   
<br>

Spike simulation
------------------------------------------
In the previous task we have seen the contents of the assembly language program for the program ```sum1ton.o``` .
Now if we debug the code we get the output of sum of 1 to n numbers. 
Now the same thing should be outputed in a RISC-V compiler. We can show this using the spike command.
Spike is a RISC-V simulator. 
It is used for running and testing codes for RISC-V based processors.
Now using the below command we can simulate the ```sum1ton.o``` code and verify the instructions.


*Use the following command*
```
spike pk sum1ton.o
```
Now we can give the input as follows:

![tsak2_spike_pk_sum1ton](https://github.com/user-attachments/assets/874bef71-58fc-4e10-83f4-f7db94558673)

The assembly langguage program for ```Ofast``` compiler is :


![new_task1_12instr](https://github.com/user-attachments/assets/56d2ec70-05cc-4ea6-ac71-ca8d580f2949)


Now let us debug this code:

![Task2_Ofast_output](https://github.com/user-attachments/assets/949c04ad-a5dd-4735-8378-8465036c514e)

* We debug the assembly language program using the command ```spike -d pk sum1ton.o``` .
* In this debugger we debug the code for each instruction (or till the required instruction) 
* At the address of ```100b4``` the value of the stack pointer is ```0x0000003ffffffb50``` and after the executing the next instruction we get the value of the stackl pointer as ```0x0000003ffffffb40```.

The next instruction is executed using the command ```  addi    sp, sp, -16 ``` . So if we subtract 16 in decimal it is equivalent to 10 in hexadecimal which is shown below in the calculator :

![task2_Ofast_calculator](https://github.com/user-attachments/assets/454bee73-e31d-4338-8c1a-d828e46f799e)

* As we have seen in the command ```  addi    sp, sp, -16 ```, the instruction addi adds the immediate offset to the source register(sp in this case) and stores in the destination register(sp in this case, hence it is overwriting the same register ).
* Now after executing all the instructions we get the output of the ```Ofast``` assembly code.

![Task2_output_Ofast](https://github.com/user-attachments/assets/8b5f5ad9-127f-4e8f-92a2-a875a30d55ae)

Now similarily if we execute the code for ```O1``` compiler:

![task2_O1_output](https://github.com/user-attachments/assets/47e86de5-c4a7-4e33-9dcf-b4e3e7ff6ad0)

* We can see that the command used is ```riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c``` , hence ```O1``` compiler is used.
* Now if we see the assembly language for ```O1``` is

![new_task1_15instr](https://github.com/user-attachments/assets/b0fe01cb-7e90-4f19-8b29-4dfe1ecf5624)

* Again after debugging each instruction we get the same values for the stack pointer as in the ```Ofast``` case.
* At the end of the code, at the address of ```101b4``` the value of the sum is stored.

### Application
--------------------------------

### Modulo Counter -
-------------------------------

A Modulo Counter is a simple digital or software-based counter that increments its value within a fixed range and resets to zero once it reaches a specified maximum. This behavior is widely used in digital systems, embedded applications, and simulation environments to handle cyclic or repetitive operations efficiently.

* The counter starts at an initial value, typically 0
* It increments by a fixed step (usually 1) with each iteration.
* When the counter reaches a predefined maximum value (MODULO), it resets back to 0.
* This cycling behavior ensures the counter remains bounded within a range of 0 to (MODULO - 1).

### C program for the modulo counter (using leafpad)
------------------------------------------------

![c_code_modcount](https://github.com/user-attachments/assets/3c30a03a-080f-4e41-824d-def2cb466d60)

### Output of the C Code in GCC
------------------------------------------------

![modcount_c](https://github.com/user-attachments/assets/810a9d7b-1302-4cc8-8f9c-50dcfce63437)

### Compiling using RISC-V GCC:
------------------------------------------------

![RISC-V_GCC_O1_Ofast](https://github.com/user-attachments/assets/16271517-8739-4918-95da-f05c4fd8fe53)


### Assembly language code for ```O1```:
------------------------------------------------

![modcount_O1_ass_code](https://github.com/user-attachments/assets/7b6c4889-b106-4a66-bdcd-60fa661b46b7)


### Assembly language code for ```Ofast```:
------------------------------------------------

![modcount_Ofast_ass_code](https://github.com/user-attachments/assets/72806583-f8e3-4b46-9299-1238ba4758bc)

### Modulo Counter OUTPUT using ```SPIKE```:
------------------------------------------------

The debugging has been done using the command 
```
spike -d pk modcount.o
```

![modcount_output_spike](https://github.com/user-attachments/assets/f99fda07-2678-4452-aa02-9fd8327e0d80)


</details>

------------------------------------

<details>
<summary><b>Task 3:</b> RISC-V instruction types </summary>   
<br>

# RISC-V Instruction Types Documentation
------------------------------------------

## Instruction Types Overview
The RISC-V ISA supports several instruction formats, each serving specific functionalities. Below are the instruction types included:

- **R-Type (Register-to-Register)**
- **I-Type (Immediate)**
- **S-Type (Store)**
- **B-Type (Branch)**
- **U-Type (Upper Immediate)**
- **J-Type (Jump)**

Each type includes details such as bit-field ranges, example instructions, operations, and opcode.

## Instruction Formats

### 1. R-Type (Register-to-Register)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type (e.g., arithmetic, logical).
- `rd`: [7:11] - Destination register.
- `funct3`: [12:14] - Operation specification (e.g., ADD, SUB).
- `rs1`: [15:19] - First source register.
- `rs2`: [20:24] - Second source register.
- `funct7`: [25:31] - Further distinguishes operations (e.g., ADD vs. SUB).

**Example:** `ADD rd, rs1, rs2`

**Operation:** Adds the values in `rs1` and `rs2` and stores the result in `rd`.

**Opcode:** `0110011`

---

### 2. I-Type (Immediate)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `funct3`: [12:14] - Operation specification (e.g., ADDI, LOAD).
- `rs1`: [15:19] - Source register.
- `imm`: [20:31] - Immediate value (12-bit).

**Example:** `ADDI rd, rs1, imm`

**Operation:** Adds the immediate value `imm` to `rs1` and stores the result in `rd`.

**Opcode:** `0010011`

---

### 3. S-Type (Store)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `imm[4:0]`: [7:11] - Immediate value (lower bits).
- `funct3`: [12:14] - Operation specification (e.g., STORE).
- `rs1`: [15:19] - Base register.
- `rs2`: [20:24] - Source register.
- `imm[11:5]`: [25:31] - Immediate value (upper bits).

**Example:** `SW rs2, imm(rs1)`

**Operation:** Stores the value in `rs2` into the memory address computed as `rs1 + imm`.

**Opcode:** `0100011`

---

### 4. B-Type (Branch)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `imm[11]`: [7] - Immediate bit.
- `imm[4:1]`: [8:11] - Immediate bits (lower).
- `funct3`: [12:14] - Branch operation specification (e.g., BEQ, BNE).
- `rs1`: [15:19] - First source register.
- `rs2`: [20:24] - Second source register.
- `imm[10:5]`: [25:30] - Immediate bits (middle).
- `imm[12]`: [31] - Immediate bit (upper).

**Example:** `BEQ rs1, rs2, imm`

**Operation:** Branches to the address `PC + imm` if `rs1` equals `rs2`.

**Opcode:** `1100011`

---

### 5. U-Type (Upper Immediate)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `imm`: [12:31] - Immediate value.

**Example:** `LUI rd, imm`

**Operation:** Loads the immediate value `imm` shifted left by 12 bits into `rd`.

**Opcode:** `0110111`

---

### 6. J-Type (Jump)
**Bit Ranges:**
- `opcode`: [0:6] - Specifies the operation type.
- `rd`: [7:11] - Destination register.
- `imm[20]`: [12] - Immediate bit.
- `imm[10:1]`: [13:22] - Immediate bits (lower).
- `imm[11]`: [23] - Immediate bit.
- `imm[19:12]`: [24:31] - Immediate bits (upper).

**Example:** `JAL rd, imm`

**Operation:** Jumps to the address `PC + imm` and stores the return address in `rd`.

**Opcode:** `1101111`

---

The below image shows the various RISC-V instruction types

![image](https://github.com/user-attachments/assets/2ef09cf5-ad58-4fd0-ac5e-8f692e04ce34)


THe given below table illustrates the 15 differnt instruction used in the application ( **modulo counter**) :

| **Address** | **Instruction**     |
| ----------- | ------------------- |
| `fc010113`  | `addi sp, sp, -64`  | 
| `02913423`  | `sd s1, 40(sp)`     |
| `05f5e4b7`  | `lui s1, 0x5f5e`    |
| `00000413`  | `li s0, 0`          | 
| `00040593`  | `mv a1, s0`         |
| `3a0000ef`  | `jal ra, 10484`     |
| `0014041b`  | `addiw s0, s0, 1`   | 
| `00813783`  | `ld a5, 8(sp)`      | 
| `fe079ae3`  | `bnez a5, 100f0`    | 
| `fd241ee3`  | `bne s0, s2, 100dc` | 
| `ffff0797`  | `auipc a5, 0xffff0` | 
| `00078863`  | `beqz a5, 10148`    | 
| `0e80006f`  | `j`                 | 
| `00012503`  | `lw a0, 0(sp)`      | 
| `78f18c23`  | `sb a5, 1944(gp)`   |


### Detailed Instruction Breakdown

1. **`addi sp, sp, -64`**  
   - *I-Type Instruction*  
     - **Format:** imm[11:0] | rs1 | funct3 | rd | opcode  
     - **Fields:**  
       - `imm = -64` (signed 12-bit: `1111111111000000`)  
       - `rs1 = x2 (sp)`  
       - `rd = x2 (sp)`  
       - `funct3 = 000`  
       - `opcode = 0010011`  
     - **32-bit Representation:** `11111111110000010 000 00010 0010011`  
     - Adjusts the stack pointer (`sp`) to allocate 64 bytes.

2. **`sd s1, 40(sp)`**  
   - *S-Type Instruction*  
     - **Format:** imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | opcode  
     - **Fields:**  
       - `imm = 40` (12-bit: `000000101000`)  
       - `rs2 = x9 (s1)`  
       - `rs1 = x2 (sp)`  
       - `funct3 = 011`  
       - `opcode = 0100011`  
     - **32-bit Representation:** `00000010100001001 011 00010 0100011`  
     - Stores the value of `s1` into memory at `sp + 40`.

3. **`lui s1, 0x5f5e`**  
   - *U-Type Instruction*  
     - **Format:** imm[31:12] | rd | opcode  
     - **Fields:**  
       - `imm = 0x5f5e000`  
       - `rd = x9 (s1)`  
       - `opcode = 0110111`  
     - **32-bit Representation:** `0101111101011110 00000 0110111`  
     - Loads the upper 20 bits of `s1` with `0x5f5e`.

4. **`li s0, 0`**  
   - *Pseudo-Instruction* (translated to `addi s0, x0, 0`)  
     - **Format:** imm[11:0] | rs1 | funct3 | rd | opcode  
     - **Fields:**  
       - `imm = 0`  
       - `rs1 = x0`  
       - `rd = x8 (s0)`  
       - `funct3 = 000`  
       - `opcode = 0010011`  
     - **32-bit Representation:** `00000000000000000 000 01000 0010011`  
     - Loads immediate `0` into `s0`.

5. **`mv a1, s0`**  
   - *Pseudo-Instruction* (translated to `addi a1, s0, 0`)  
     - **Format:** imm[11:0] | rs1 | funct3 | rd | opcode  
     - **Fields:**  
       - `imm = 0`  
       - `rs1 = x8 (s0)`  
       - `rd = x11 (a1)`  
       - `funct3 = 000`  
       - `opcode = 0010011`  
     - **32-bit Representation:** `00000000000001000 000 01011 0010011`  
     - Copies the value from `s0` into `a1`.

6. **`jal ra, 10484`**  
   - *J-Type Instruction*  
     - **Format:** imm[20|10:1|11|19:12] | rd | opcode  
     - **Fields:**  
       - `imm = 10484` (encoded as `0000010100100000000`)  
       - `rd = x1 (ra)`  
       - `opcode = 1101111`  
     - **32-bit Representation:** `00000101001000000 001 00001 1101111`  
     - Jumps to address `10484` and stores the return address in `ra`.

7. **`addiw s0, s0, 1`**
   - *I-Type Instruction*
     - **Format:**  imm[11:0] | rs1 | funct3 | rd | opcode
     - **Fields:**
       - `imm = 1`
       - `rs1 = x8 (s0)`
       - `rd = x8 (s0)`
       - `funct3 = 000`
       - `opcode = 0011011`
     - **32-bit Representation:** `00000000000101000 000 01000 0011011`
     -  Adds the immediate value `1` to `s0`
       
8. **`ld a5, 8(sp)`**
   - *I-Type Instruction*
     - **Format:**  imm[11:0] | rs1 | funct3 | rd | opcode
     - **Fields:**
       - `imm = 8` (12-bit: 000000001000)
       - `rs1 =x2 (sp)`
       - `rd = x15 (a5)`
       - `funct3 = 011`
       - `opcode = 0000011`
     - **32-bit Representation:** `00000000100000010 011 01111 0000011`
     -  Loads a 64-bit value from memory at `sp + 8` into `a5`

9. **`bnez a5, 100f0`**
   - *B-Type Instruction*
     - **Format:**   imm[12|10:5] | rs2 | rs1 | funct3 | imm[4:1|11] | opcode
     - **Fields:**
       - `imm = 100f0` (encoded as `00001000000000`)
       - `rs2 =x0`
       - `rs1 = x15 (a5)`
       - `funct3 = 001`
       - `opcode = 1100011`
     - **32-bit Representation:** `00001000000000001 001 01111 1100011`
     -  Branches to address `100f0` if the value in `a5` is not `zero`.

10.  **`bne s0, s2, 100dc`**
      - *B-Type Instruction*
        - **Format:**   imm[12|10:5] | rs2 | rs1 | funct3 | imm[4:1|11] | opcode
        - **Fields:**
          - `imm = 100dc` (encoded as `00001000000110`)
          - `rs2 =x18 (sp2)`
          - `rs1 = x8 (s0)`
          - `funct3 = 001`
          - `opcode = 1100011`
        - **32-bit Representation:** `00001000000110001 001 01000 1100011`
        -  Branches to address `100dc` if the value in `s0` is not `s2`.

11.  **`auipc a5, 0xffff0`**  
      - *U-Type Instruction*  
        - **Format:** imm[31:12] | rd | opcode  
        - **Fields:**  
          - `imm = 0xffff0`  
          - `rd =  x15 (a5)`  
          - `opcode = 0010111`  
        - **32-bit Representation:** `11111111111111110 00000 0010111`  
        - Adds the 20-bit immediate value `0xffff0` to the program counter (PC) and stores the result in `a5`.

12.  **`beqz a5, 10148`**
      - *B-Type Instruction*
        - **Format:**   imm[12|10:5] | rs2 | rs1 | funct3 | imm[4:1|11] | opcode
        - **Fields:**
          - `imm = 10148` (encoded as `00001000101000`)
          - `rs2 = x0`
          - `rs1 = x15 (a5)`
          - `funct3 = 000`
          - `opcode = 1100011`
        - **32-bit Representation:** `00001000101000000 000 01111 1100011`
        -   Branches to address `10148` if the value in `a5` is `zero`.

13. **`jal ra, 10484`**  
      - *J-Type Instruction*  
        - **Format:** imm[20|10:1|11|19:12] | rd | opcode  
        - **Fields:**  
          - `imm = Target address `
          - `rd = x0`  
          - `opcode = 1101111`  
        - **32-bit Representation:** `Dependent on the target address`  
        - Performs an unconditional jump to a computed address.

14. **`lw a0, 0(sp)`**
      - *I-Type Instruction*
        - **Format:**  imm[11:0] | rs1 | funct3 | rd | opcode
        - **Fields:**
          - `imm = 0` 
          - `rs1 =x2 (sp)`
          - `rd = x10 (a0)`
          - `funct3 = 010`
          - `opcode = 0000011`
        - **32-bit Representation:** `00000000000000010 010 01010 0000011`
        -  Loads a 32-bit word from memory at address `sp + 0` into `a0`.

15. **`sd s1, 40(sp)`**  
      - *S-Type Instruction*  
        - **Format:** imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | opcode  
        - **Fields:**  
          - `imm = 1944` (12-bit: `000001111001000`)  
          - `rs2 = x15 (a5)`  
          - `rs1 = x3 (gp)`  
          - `funct3 = 000`  
          - `opcode = 0100011`  
        - **32-bit Representation:** `00000111100101111 000 00011 0100011`  
        -  Stores the least significant byte of `a5` into memory at address `gp + 1944`.

</details>

------------------------------------

<details>
<summary><b>Task 4:</b> Functional simulation of RISC-V Core Verilog netlist and testbench and observing the waveforms </summary>   
<br>

For performing the simulation, we need to first simulate. We can perform it by coding it in verilog and simulating the code in gtkwave.

Hence we can install them using the command 

```sudo apt install iverilog gtkwave```

![iverlog_install](https://github.com/user-attachments/assets/d9b41866-1d5b-4605-bd2a-0d09e089a32f)



# Steps to perfrom the functional simulation
--------------------------------------------

- We can perform the simulation by either cloning the github repository or by creating a new directory.
- If we are cloning, then we need to clone the repository :  https://github.com/vinayrayapati/rv32i/   ,
   - We need to use the command ``` git clone ```
   - ![gitclonedone](https://github.com/user-attachments/assets/ce018e69-6c17-4753-ae84-df771ec73772) 
   - Then ``` ls -ltr```
   - ```cd iiitb_rv32i ``` to code in the ```iitb_rv32i``` directory.
   - ![gitclone_ls-ltr](https://github.com/user-attachments/assets/be68ceb5-a50c-425a-ac1f-d3294f09a438)
   - Then in order to simulate and run the verilog code ``` iverilog -o iiitb_rv32i rj_rv32i.v rj_rv32i_tb.v```
   - ```ls -ltr``` to list the files.
   - ```./iitb_rv32i``` for generating the vcd file.
   - Then in order to visualize the output using gtkwave we use the command ```gtkwave iiitb_rv32i.vcd```
   - Now we need to check all the instructions.
- If we are creating a new directory and performing in it
   - Creating a new directory using ``` mkdir rohan```
   - Creating 2 files using ```touch``` as rohan_rv32i.v and rohan_rv32i_tb.v
   - Copy the code the from the reference github (because writing the testbench and designing it is not part of this internship) and paste it in our reference files in rohan_rv32i.v and rohan_rv32i_tb.v files respectively.
   - ![mkdir_rohan](https://github.com/user-attachments/assets/46e60469-caff-4021-8410-4d200076d3f1)
   - In order to simulate the code we follow the above simulation commands with the new files in your command.
   - ![gtk_St](https://github.com/user-attachments/assets/1386fe5a-a9c4-43b9-b756-1d5fc2340f16)


- Then the GTKWave will be opened and we need to check for all the instructions.

Now we need to analyse the waveforms of the instructions that are used in the verilog code

**``` Instruction 1: ADD R6,R2,R1  ```**

![add_4](https://github.com/user-attachments/assets/c21db68c-0288-4cda-bdaf-26396a85438a)


**``` Instruction 2: SUB R7,R1.R2  ```**

![sub_4](https://github.com/user-attachments/assets/312147d9-d32a-462b-8e5d-c0493307b31e)


**``` Instruction 3: AND R8,R1,R3  ```**

![and_3_4](https://github.com/user-attachments/assets/6e957583-26fc-49cd-ad6c-cd6edf031ca6)


**``` Instruction 4: OR R9,R2,R5  ```**

![OR_4_4](https://github.com/user-attachments/assets/7a0d5ae5-92cc-4a8e-b594-6bc9689f81c6)


**``` Instruction 5: XOR R10,R2,R4  ```**

![XOR_5_4](https://github.com/user-attachments/assets/56f3a33f-bb00-4332-a54f-e14c46828437)


**``` Instruction 6: SLT R1,R2,R4  ```**

![SLT_6_4](https://github.com/user-attachments/assets/4342c554-0862-402f-9580-18fccc3d912d)


**``` Instruction 7: ADDI R12,R4,5  ```**

![ADDI_7_4](https://github.com/user-attachments/assets/64189f1c-5a75-4487-a313-c53a347f8a7b)


**``` Instruction 8: BEQ R0,R0,15  ```**

![BEQ_8_4](https://github.com/user-attachments/assets/f7ddc0bb-63ea-4a39-b7ca-4be5bfeb2524)


**``` Instruction 9: BNE R0,R1,2  ```**

![BNE_9_4](https://github.com/user-attachments/assets/c48ac39a-1f8c-4a54-932d-924c784dae0f)


**``` Instruction 10: SLL R15,R1,R2  ```**

![SLL_10_4](https://github.com/user-attachments/assets/3deefd03-aa00-4673-8f4a-613c9e4b365e)

</details>
