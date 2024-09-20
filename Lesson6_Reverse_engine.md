# Reverse Engineering


## X86_64 Assembly
- There are 16 general purpose 64-Bit registers
- %rax      the first return register
- %rbp      the base pointer that keeps track of the base of the stack
- %rsp      the stack pointer that points to the top of the stack
- You will see arguments passed to functions as something like:```[%ebp-0x8]```

## X86_64 Assembly - Common Terms
- Heap                Memory that can be allocated and deallocated
- Stack               A contiguous section of memory used for passing arguments
- General Register    A multipurpose register that can be used by either programmer or user to store data or a memory location address
- Control Register    A processor register that changes or controls the behavior of a CPU
- Flags Register      Contains the current state of the processor

## X86_64 Assembly - Memory Offset
- There is one instruction pointer register that points to the memory offset of the next instruction in the code segment:
```
------------------------------------------------------------------------------------------------------------------
64-Bit  -  Lower 32 bits  -  Lower 16 bits  -  Descrition
RIP     -  EIP            -  IP             -  Instruction Pointer; holds address for next instruction to be executed
--------------------------------------------------------------------------------------------------------------------
```

## X86_64 Assembly - Common Instruction Pointers
- MOV     move source to destination
- PUSH    push source onto stack
- POP     Pop top of stack to destination
- INC     Increment source by 1
- DEC     Decrement source by 1
- ADD     Add source to destination
- SUB     Subtract source from destination
- CMP     Compare 2 values by subtracting them and setting the %RFLAGS register. ZeroFlag set means they are the same.
- JMP     Jump to specified location
- JLE     Jump if less than or equal
- JE      Jump if equal


## Reverse Engineering Workflow (Software)
- Static
- Behavioral
- Dynamic
- Disassembly
- Document Findings
- Reverse Engineering Workflow    #https://git.cybbh.space/sec/public/-/jobs/artifacts/master/raw/guides/Reverse_engineering_workflow.pdf?job=genpdf

## Portable Executable Patching / Software Analysis
- Perform Debugging and Disassembly
- Find the Success/Failure
- Adjust Instructions
- Apply Patch and Save
- Execute Patched Binary
























