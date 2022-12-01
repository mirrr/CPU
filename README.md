# CS61CPU

alu.circ: Created subcircuits within alu.circ built-in gates and other logic. Utilized tunnels and mux to implement the selection of each ALU operation   

regfile: Used built-in register to create 32 registers, demux to select which register writeEN should be turned on for, and mux to select output values from the specific registers wanted  

addi: Set up immediate generator to split and retrieve imm for an addi instruction. Set up control logic for addi using constants. Completed cpu.circ following spec, utilizing alu, regfile, immgen, and control_logic for the five stages. Added a register in between stages 1 and 2 for pipelining.  
  
cpu: logic from single cycle datapath diagrams used in lecture and discussion (csr, pc, imm_gen, alu, writeback, regfile, alu, branch_comp, control inputs)
    
control_logic: 
PCSel, Asel, Bsel, CSR inputs, BrUn - Used chain of muxes to set PCSel = 1 for when jal, jalr, and branch instructions where branch would be taken. Let CSRWen = 1, if instruction is a csr type. Let CSRSel be 1 if an immediate is used. Let BrUn be 1 only if instruction is bltu or bgeu.  
Asel, Bsel, WBSel, ALUSel, RegWEn, ImmSel; Set Asel with a mux to be 1 for jal, auipc, and branch instructions, 0 otherwise. Use mux to set Bsel = 0 when instruction is r type, otherwise Bsel = 1. Set WBSel = 1 for i type load instructions, WBSel = 2 for jal and jalr instructions, WBSel = 0 otherwise. Set ALUSel to desired alu computation noted by the opcode, func3 and func7 codes. Set ALUSel = 0 otherwise. Set RegWEn = 0 if s type or b type, set RegWEn = 0 otherwise. Set ImmSel = 0 if r type, ImmSel = 1 if i type, ImmSel = 2 if s type, ImmSel = 3 if sb type, ImmSel = 4 if j type, and ImmSel = 5 if uj type. 
    
branch comparator: used comparators to set output values for BrLt and BrEq. Used BrUn to determine whether comparison would be signed or unsigned.   
 
  -imm_gen: Miranda, U type debugging: Jenny - used splitters to generate immediates for each instruction type following green sheet and provided table in spec  
  -pipelining: Jenny - added registers to store PC and instruction, added nop for jump instructions and branch instructions (if branch was taken) based on PCSel == 1  
  
custom tests:
Unit tests for R-types, I-types (lb, lh, lw, addi, slli, slit, xori, srli, srai, ori, andi), S-types, SB-types, and U-types. Jenny: Unit tests for register coverage, J-types and I-types (jalr, csrw, csrwi). Integration tests for loads and stores, branches, U-types, and jumps. Edge cases for lui, loads and stores. Integration tests for R-types, I-types and S-types. Edge cases for branch-jump, full memory, loads and stores.
  
   
