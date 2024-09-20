# Reverse Engineering
https://sec.cybbh.io/public/security/latest/lessons/lesson-6-reverse_sg.html

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
- Reverse Engineering Workflow
```
https://git.cybbh.space/sec/public/-/jobs/artifacts/master/raw/guides/Reverse_engineering_workflow.pdf?job=genpdf
```
![](https://github.com/jdbonner/Security/blob/main/images/reverse_engine_workflow.png)


## Portable Executable Patching / Software Analysis
- Perform Debugging and Disassembly
- Find the Success/Failure
- Adjust Instructions
- Apply Patch and Save
- Execute Patched Binary


## Assembly example 1
```
main:
  mov rax, 16         //move in rax the value of 16.
  push rax            //push the value of rax (16) onto the stack. stack grows by 8 bytes.
  jmp mem2            //jump to mem2 function

mem1:       
  mov rax, 8          //move in rax the value of 8
  ret                 //return the value of what is in the first return registry.

mem2:   
  pop r8              //pop the value at the top of the stack (16) into r8
  cmp rax, r8         //compare to the value of rax (16) the value of r8 (16). They are equal; zero flag is set.
  je mem1             //zero flag from last instruction is set. jump to mem1 function.
```
## Assembly example 2
```
main:
  mov rcx, 25       //move into rcx the value of 25
  mov rbx, 62       //move into rbx the value of 62
  jmp mem1          //jump to location mem1

mem1:
  sub rbx, 40       //subtract from rbx the value of 40, rbx is now 22
  mov rsi, rbx      //move rsi into rbx
  cmp rcx, rsi      //compare the value of rcx (25) to the value of rsi (22). flag indicating less than is set.
  jle mem2          //jump if less than or equal to flag is set. rsi is less than rcx, jump to mem2.

mem2:
  mov rax, 0        //move into rax the value of 0
  ret               //returns the value of what is in the first return registry. returns 0
```





















