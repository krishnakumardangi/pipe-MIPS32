This repository for pipe-MIPS32 verilog code.

The MIPS32 is the instruction set architecture of a popular Reduced Instrucon Set Architecture (RISC) processor.
	– It is	a 32-bit processor, i.e. can operate on 32 bits	of data	at a time.

## A Quick Look at MIPS32 ##
* MIPS32 registers:
	a) 32-bit general purpose registers (GPRs), R0 to R31.
		- Register R0 contains a constant 0; cannot be written.
	b) A special-purpose 32-bit program counter (PC).
		- Points to the next instruction in memory to be fetched and executed.
* No flag registers (zero, carry, sign etc).
* Very few addressing modes (register, immediate, register indexed etc).
	- Only load and stire instructions van access memory.
* We assume memory word size is 32 bits (word addressable).

## The MIPS32 Instruction Subset Being Considered ##
• Load and Store Instructions	
	LW R2,124(R8)	// R2 = Mem[R8+124] 
	SW R5,-10(R25)  // Mem[R25-10] = R5 

• Arithmetic and Logic Instructions	(only register operands)
	ADD R1,R2,R3    // R1 = R2 + R3     
	ADD R1,R2,R0    // R1 = R2 + 0
	SUB R12,R10,R8  // R12 = R10 – R8 
	AND R20,R1,R5   // R20 = R1 & R5    
	OR  R11,R5,R6   // R11 = R5 | R6 
	MUL R5,R6,R7    // R5 = R6 * R7 
	SLT R5,R11,R12  // If R11 < R12, R5=1; else R5=0

• Arithmetic and Logic Instructions (immediate operand)
	ADDI R1,R2,25   // R1 = R2 + 25 
	SUBI R5,R1,150  // R5 = R1 – 150  
	SLTI R2,R10,10  // If R10<10, R2=1; else R2=0 

• Branch Instructions	
	BEQZ R1,Loop    // Branch to Loop if R1=0 
	BNEQZ R5,Label  // Branch to Label if R5!=0 

• Jump Instruction	
	J Loop          // Branch to Loop unconditionally 

• Miscellaneous	Instruction	
	HLT             // Halt execution


## MIPS Instruction Encoding ##
• All MIPS32 instructions can be classified into three groups in terms of instruction encoding.
	– R-type (Register), I-type (Immediate), and J-type (Jump).
	– In an instruc on encoding, the 32 bits of the instruction are divided into several fields of fixed widths.
	– All instructions may not use all the fields.

• Since the relative positions of some of the fields are same across instructions, instruction decoding becomes very simple.



## MIPS32 Instruction Cycle ##
• We divide the instruction execution cycle into five steps:
a) IF   : Instruction Fetch
b) ID   : Instruction Decode/Register Fetch
c) EX   : Execution/Effective Address Calculation	
d) MEM  : Memory Access/Branch Completion
e) WB   : Register Write-back

• We now show the generic micro-instructions carries out in the various steps.
