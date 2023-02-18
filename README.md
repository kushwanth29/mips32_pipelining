# mips32_pipelining
Stages of Pipelining


![image](https://user-images.githubusercontent.com/82768295/216562593-bd36dfdc-a194-4822-b843-0a4a9948561a.png)

#The multicycle implementation breaks instructions down into multiple steps. These steps typically are the:

1)Instruction fetch step

2)Instruction decode and Register fetch step

3)Execution, memory address computation, or branch completion step

4)Memory access or R-type instruction completion step

5)Memory read completion step





# Risc based instuctions

RR_ALU:

ADD: EX_MEM_ALUOut <= #2 ID_EX_A + ID_EX_B;

SUB: EX_MEM_ALUOut <= #2 ID_EX_A - ID_EX_B;

AND: EX_MEM_ALUOut <= #2 ID_EX_A & ID_EX_B;

OR: EX_MEM_ALUOut <= #2 ID_EX_A | ID_EX_B;

SLT: EX_MEM_ALUOut <= #2 ID_EX_A < ID_EX_B;

MUL: EX_MEM_ALUOut <= #2 ID_EX_A * ID_EX_B;



RM_ALU: 

ADDI: EX_MEM_ALUOut <= #2 ID_EX_A + ID_EX_Imm;

SUBI: EX_MEM_ALUOut <= #2 ID_EX_A - ID_EX_Imm;

SLTI: EX_MEM_ALUOut <= #2 ID_EX_A < ID_EX_Imm;

default: EX_MEM_ALUOut <= #2 32'hxxxxxxxx;



LOAD, STORE:

EX_MEM_ALUOut <= #2 ID_EX_A + ID_EX_Imm;

EX_MEM_B <= #2 ID_EX_B;



BRANCH: 

EX_MEM_ALUOut <= #2 ID_EX_NPC + ID_EX_Imm;

EX_MEM_cond <= #2 (ID_EX_A == 0);



# Implementation

Successfully Implemented 

On Xilinx Vivado,

Converted behavioral to structural description using yosys

![Screenshot from 2023-02-03 13-07-22](https://user-images.githubusercontent.com/82768295/216568174-697d07ce-bb42-4c90-beb8-d2c515fd70e8.png)
![Screenshot from 2023-02-03 13-06-40](https://user-images.githubusercontent.com/82768295/216568202-67d6d3d2-85af-45a2-82a3-0ff78ef98a67.png)

And verified testbench results on ep wave i.e on eda playground

![Screenshot (31)](https://user-images.githubusercontent.com/82768295/216602679-1945d847-81f6-4129-be84-df2c6ac82cb0.png)


# Hazards

1)Structural Hazards:

This Hazard occurs, when two (or) more instructions need to utilize the same resource at atime.

Example:

1. One memory unit is used for instruction fetch and datafetch.

2. Since many floating point instructions require many cycles it is easy for them to interfere with

each other.

2)Data Hazards:

Data hazards occur when data is used before it is ready. As shown in the figure below, the ADD

instruction releases its result after the execute stage. But that is needed by the SUB instruction

even before it is released

3)Control Hazards:

If the main program is branching towards a sub-program, it needs the return address in main

memory. Then only it jumps towards subroutine. The control hazard occurs if the instruction is

not specified in the return address. 







