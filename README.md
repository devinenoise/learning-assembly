# 64-bit Assembly Language Notes

### Why Learn Assembly Language
- Understand how a computer works
- Debugging
- Writing an operating system (device drivers, memory protection, context switching, program states)

### Computer Architecture

The *CPU* communicates with memory and I/O devices over the system bus.  The CPU is the brain of the computer and handles the data processing.

*Registers* store data and temporary results.

The *Control Unit* directs the operations of the CPU.

The *Arithmatic and Logic Unit* performs math, and or, not operations.

The main memory is bits of values 0 or 1.  


## The Processor Mode

### 64-bit mode
The 64 bit architecture introduces a new mode called IA-32e, which contains two sub modes (64 bit Mode and Compatibility Mode).

In 64 bit mode, you can run 64 bit programs and the 64 bit operating system.

- 16  64-bit general purpose registers

- 64-bit flags register `RFLAGS`

- 64-bit instruction pointer `RIP`

- 48-bit virtual address support


### Compatibility Mode
Compatibility Mode allows for 16 and 32-bit programs to run under 64-bit operating system without recompiling those programs.

*General purpose registers* are used for data transfer, arithmatic, and logic operations.

## Data Representation

*Decimal* : 0 - 9 in `Base 10`. (1, 10, 100, 1000, 10000, etc).

*Binary* : 0 + 1 in `Base 2`.  (1, 2, 4, 6, 8, 16, 32, 64, 128, 256, 512, 1024, etc)

*Hexadecimal* : 0 - 9 and A - F (10-15)

| Binary | Hex Convesion|
---| --- |
| 0000 | 0 |
| 0001 | 1 |
| 0010 | 2 |
| 0011 | 3 |
| 0100 | 4 |
| 0101 | 5 |
| 0110 | 6 |
| 0111 | 7 |
| 1000 | 8 |
| 1001 | 9 |
| 1010 | A |
| 1011 | B |
| 1100 | C |
| 1101 | D |
| 1110 | E |
| 1111 | F |

### Hex to Binary Conversion
Hexadecimal is used to convey binary information in Base 16.

7AE Breakdown from Hex To Binary

7 = 0111

A = 1010

E = 1110


### Binary to Hex Conversion

Add zeroes to Binary to make four digits

289 Breakdown from Binary to Hexadecimal

- 10 = 0010 = 2

- 1000 = 1000 = 8

- 1001 = 1001 = 9


## Signed and Unsigned Numbers

Unsigned number is positive (including zero)
- N bits = 0 to 2 to the Nth power - 1

Example - 1 Bit (0 to 2 to the power of 1 - 1)
- 0 = 0
- 1 = 1

Example - 2bits (0 to 2 to the power of 2 - 1)
- 00 = 0
- 01 = 1
- 10 = 2
- 11 = 3

Example - 3bits (0 to 2 to the power of 3 - 1)
- 000 = 0
- 001 = 1
- 010 = 2
- 011 = 3
- 100 = 4
- 101 = 5
- 110 = 6
- 111 = 7

Signed numbers can be positive or negative.
- N bits positive = 0 to 2 to the (Nth power-1) - 1
- 0 is positive, 1 is negative

Use all bits except the sign bit to calculate the value.  
The sign bit is the most significant bit.  
The Negative range = -128 to -1

## ASCII Strings

| Character | Decimal |
---| --- |
| H | 72 |
| E | 69 |
| L | 76 |
| L | 76 |
| O | 79 |

It's customary to add a zero to the end of a string called a *null terminated string* as an additional byte.

## ASCII Table [https://simple.wikipedia.org/wiki/ASCII]

| Decimal | Hex | Char |
---| --- | :---: |
| 65 | 41 | A |
| 66 | 42 | B |
| 67 | 43 | C |
| 68 | 44 | D |
| 69 | 45 | E |
| 70 | 46 | F |
| 71 | 47 | G |
| 72 | 48 | H |
| 73 | 49 | I |
| 74 | 4A | J |
| 75 | 4B | K |
| 76 | 4C | L |
| 77 | 4D | M |
| 78 | 4E | N |
| 79 | 4F | O |
| 80 | 50 | P |
| 81 | 51 | Q |
| 82 | 52 | R |
| 83 | 53 | S |
| 84 | 54 | T |
| 85 | 55 | U |
| 86 | 56 | V |
| 87 | 57 | W |
| 88 | 58 | X |
| 89 | 59 | Y |
| 90 | 5A | Z |
| 91 | 5B | \[ |
| 92 | 5C | \ |
| 93 | 5D | ] |
| 94 | 5E | ^ |
| 95 | 5F | _ |
| 96 | 60 | ` |
| 97 | 61 | a |
| 98 | 62 | b |
| 99 | 63 | c |
| 100 | 64 | d |
| 101 | 65 | e |
| 102 | 66 | f |
| 103 | 67 | g |
| 104 | 68 | h |
| 105 | 69 | i |
| 106 | 6A | j |
| 107 | 6B | k |
| 108 | 6C | l |
| 109 | 6D | m |
| 110 | 6E | n |
| 111 | 6F | o |
| 112 | 70 | p |
| 113 | 71 | q |
| 114 | 72 | r |
| 115 | 73 | s |
| 116 | 74 | t |
| 117 | 75 | u |
| 118 | 76 | v |
| 119 | 77 | w |
| 120 | 78 | x |
| 121 | 79 | y |
| 122 | 7A | z |


## Assembly and Linking Basics

**Source File** > *(Preprocessing Directives)* > **Object File** > *(Linker)* >  **Executable**

The first step in writing assembly code starts with a programmer using a text editor to write assembly code.  Then, the file is saved as a source file.  The assembler starts by reading a source file that uses preprocessing directives to modify the source file before translating it into an object file that uses machine code.  If the project includes some invalid code, the assembler will issue an error and stop the process.  The Linker will read the object file and see if the program references outside code.  If the object file uses any outside libraries, the Linker will link the specific module needed to help create the executable file.  Finally, the Linker creates the executable file.


### Variables
Db - byte size (1 byte or 8bit)

Dw - word size (2 bytes or 16bit)

DD - double size (4 bytes or 32bit)

Dq - quad size (8 bytes or 64bit)

Variables are defined as *name*, *size*, and *value*. *Equ* can used to define a variable to a constant value.  It can't be changed later.

### Directives
*Directives* allocate storage, define symbols, and direct how the assembler works on the program. 
*Section* is also a directive.  Programs are usually divided into different sections where each section has its own purpose.  For example, text section would be used to define instructions and the data section would be used to define variables.
*Global* is a directive that makes a label globally available.

### Label
A *label* ends with a colon and is placed before the instructions.  MAIN is an example of a label.  Label names are case sensitive and can use english letters, numbers, underscore, number sign, tilde and the question mark.

### Instruction
An *instruction* generally contains four parts: the label, instruction mnemonics, operands, and comments.

Example - **CMAIN:** *xor rax, rax* ;an instruction

CMAIN is the label

xor is the mnemonic

rax, rax is the operand (destination, source)

;an instruction is the comment

Label and comments are optional while the mnemonic is required.  The operand is the value that the instruction operates on. Between 0 and 3 operands are allowed.

## Move Instruction (MOV)
Mov instructions are used to transfer data between registers and memory.

### Syntax
*mov destination, source*

mov reg, imm (moves an immediate value(i.e numeric) to a register)

mov reg, reg (transfer data between registers)

move mem, imm (define a variable in memory and then assign an immediate value to it)

### Rules
You cannot move data to an immediate value in the destination.  You cannot move mem to mem; you must use a register as an intermediary.  The source and destination operands must be the same size.

When moving a value to a register or variable, make sure that the value is not larger than the register can store.

## Exchange Instruction (xchg)

xchg is used to exchange the contents of two operands.

### Syntax

xchg reg, reg

xchg reg, mem

xchg mem, reg

### Rules
You cannot exchange an immediate value, operands must be the same size in bits, and two operands cannot be in memaory at the same time (xchg mem, mem).

## Increment Instruction (inc)

inc is used to add one to a register or memory operand.

### Syntax

inc reg

inc mem

## Decrement Instruction (dec)

dec is used to subtract one from a register or memory operand.

### Syntax

dec reg

dec mem

*Both increment and decrement instructions will not accept a constant value (**inc** 8, **dec** 7)*

## Negate Instruction (neg)

neg reverses the sign of a value.  Zero still remains zero.

### Syntax

neg reg

neg mem

## Add/Subtract Instructions (add/sub)

Add instruction adds the value of the source to the destination.  Sub instruction will subtract value from the source.

### Syntax
add sub destination, source

add/sub reg, imm

add/sub reg, reg

add/sub mem, imm

add/sub reg, mem

add/sub mem, reg

### Rules
Destination and source operands must be the same size.

## Rflags
Rflags is a 64 bit register that contains individual bits to control CPU operations and to reflect the result of operations.  The available bits are *carry flag*, *sign flag*, *Overflow flag*, and the *zero flag*.  These are all status flags.

The **carry flag** is set when the result of an operation cannot fit in the destination.  It is used for *unsigned* operations.

The **zero flag** is set when the result of an operation is zero.

The **sign flag** is set when the result of an operation is negative.

The **overflow flag** is set when the result of an operation cannot fit into the destination.  It is used for *signed* operations.

## Bitwise Instructions (and, or, xor)

### And Instruction
and destination, source

and reg, imm

and reg, reg

and mem, imm

and reg, mem

and mem, reg

| x | y | x and y |
---| --- | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 0 | 0 |
| 1 | 1 | 1 |

### Rules
You cannot put an immediate value in the destination operand and the operands must be the same size.  Destination and source cannot be in memory operands at the same time.

### Or Instruction
or destination, source

or reg, imm

or reg, reg

or mem, imm

or reg, mem

or mem, reg

| x | y | x or y |
---| --- | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Rules
You cannot put an immediate value in the destination operand and the operands must be the same size.  Destination and source cannot be in memory operands at the same time.

### Exclusive or (xor) Instruction
xor destination, source

xor reg, imm

xor reg, reg

xor mem, imm

xor reg, mem

xor mem, reg

| x | y | x xor y |
---| --- | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 0 |

### Rules
You cannot put an immediate value in the destination operand and the operands must be the same size.  Destination and source cannot be in memory operands at the same time.

## Flag modifiers for And / Or / Xor
Sign Flag

Zero Flag

- It always clears overflow and carry flags.

### Or Instruction
or destination, source

or reg, imm

or reg, reg

or mem, imm

or reg, mem

or mem, reg

| x | y | x or y |
---| --- | :---: |
| 0 | 0 | 0 |
| 0 | 1 | 1 |
| 1 | 0 | 1 |
| 1 | 1 | 1 |

### Rules
You cannot put an immediate value in the destination operand and the operands must be the same size.  Destination and source cannot be in memory operands at the same time.

### Not Instruction

not reg

not mem

- Inverts all bits in an operand.

### Rules
Does not accept an immediate value.  No flags are affected.

## Branching Instructions

Branch instructions can change the value of the RIP register which alters the flow of control.  The causes execution to continue at a new address.  The basic types are unconditional branch and conditional branch.

The *Unconditional Branch* will branch to a new location in all cases.

The *Conditional Branch* will branch if a certain condition is true.  This enables you to make decisions in the program.  For example, a flag can be used as a condition to make a decision.

## Jump Instruction (jmp)
jmp destination

jmp label

jmp reg

jmp mem

- When you execute the jump instruction the program will branch to the destination.

### Rules
The register must be 64 bits and the memory operand needs to be 64 bits.

## Test Instruction (test)

test reg, imm

test reg, reg

test mem, imm

test reg, mem

test mem, reg

### Rules
Test sets zero and sign flag according to the result.  Test does no modify destination operand.

## Conditional Branch Instructions

je/jz destination (jump if zero flag is set)

jne/jnz destination (jump if zero flag is cleared)

jc destination (jump if carry flag is set)

jnc destination (jump if carry flag is cleared)

jo destination (jump if overflow flag is set)

jno destination (jump if overflow flag is cleared)

js destination (jump if sign flag is set)

jns destination (jump if sign flag is cleared)

### Unsigned Conditions

ja/jnbe destination (jump if left > right)

jae/jnb destination (jump if left >= right)

jb/jnae destination (jump if left < right)

jbe/jna destination (jump if left <= right)

## Compare Instruction (cmp)
cmp left operand, right operand

cmp reg, imm

cmp reg, reg

cmp mem, imm

cmp reg, mem

cmp mem, reg

- Compare performs subtraction and changes the zero, sign, overflow, and carry flags.

### Signed Conditions

jg/jnle (left operand > right)

jge/jnl (left operand >= right)

jl/jngo (left operand < right)

jle/jng (left operand <= right)

### Conditional Structures

A conditional structure is one or more conditional expressions which make choices between different branches.

Each branch causes a different sequence of instructions to execute.

**Start / End**
if statement / endif

if else statement / endif

while loop / endwhile

do while loop / endwhile

## Arrays
An array is a collection of data stored at continuous memory locations.

When accessing an array, the offset of the element varies depending on the data types (2 bytes, 4 bytes, 8 bytes)

### Two-dimensional Array
Arranged by row major order and column major order.

When accessing items in *row major order*, you need to know which row the item is located and the column offset.

When accessing items in *column major order*, you need to know which column the item is located and the row offset.

## Addressing Modes
Addressing mode specifies the rules for calculating the addrss of an operand.

*Immediate addressing* means the instruction contains the operand value instead of using an operand from memory.  The immediate value is constant and can be signed or unsigned.

*Register addressing* means that the operand is in the register sepcified by the instruction.

*Direct addressing* means the address of an operand is given in the instruction as the absolute address.

*Indirect addressing* is base + index * scale + displacement
- base - register or immediate value
- index - register or immediate value
- scale - 1, 2, 4, or 8
- displacement - immediate value

*Rip-relative addressing* is formed by adding the numeric value to the rip register "rel" 

### Endianness
Endianness describes the order in which a sequence of bytes are stored in memory.  

x86 processors uses little-endian order when it stores and reads data from memory, starting with the least significant byte (LSB).

Big-endian order is used in network protocols, starting with the most significant byte (MSB).

### Lea Instruction
The Lea instruction calculates the addrss of a memory location and stores it in the register.

## Multiplication and Division instruction 

### *Unsigned* Multiplication (mul) 
mul reg

mul mem

| multiplier | multiplicand | upper half | lower half |
---| --- | --- | --- |
| 8bit | al | ah | al |
| 16bit | ax | dx | ax |
| 32bit | eax | edx | eax |
| 64bit | rax | rdx | rax |

Will set carry flag and overflow flag if the upper half of the produce is not zero.  Otherwise, the flags are cleared.  If the flags are cleared, you can ignore the upper half since it's zero.  Otherwise, include the upper half of the product in the result.

### *Unsigned* Division (div)
div reg

div mem

| divison | upper half | lower half | quotient | remained |
---| --- | --- | --- | --- |
| 8bit | ah | al | al | ah |
| 16bit | dx | ax | ax | dx |
| 32bit | edx | eax | eax | edx |
| 64bit | rdx | rax | rax | rdx |

Status flags are undefined.

### *Signed* Multiplication Instruction (imul) 

- one operand (register is twice the size for storing the product)

imul 8 bit

imul 16 bit

imul 32 bit

imul 64 bit

- two operands (truncates product to length of the destination and can set carry and overflow flags)

imul reg, imm

imul reg, reg

imul reg, mem

- three operands (multiply second operand by the third one and store in the first operand.  Also truncates the length of the product to the destination)

imul reg, reg, imm

imul reg, mem, imm

### *Signed* Division Instruction (idiv) 

idiv reg

idiv mem

idiv 8 bit - ah al -> al ah

idiv 16 bit - dx ax -> ax dx

idiv 32 bit - edx eax -> eax edx

idiv 64 bit - rdx rax -> rax rdx

In order to properly do signed division you have to use a sign extension.  A sign extension means copying the sign bit of a value into all the upper bits of a large size-value.

### Sign Extension Instructions

- cbw - convert byte to word

- cwd - convert word to double word

- cdq - convert double word to quadword

- cqo - convert quadword to octoword

### Shift Left Instruction (shl/sal)

*Shift left* shifts the bits of a value to the left by the number of bits specified.  The lowest bit is filled with 0.

The bit that is shifted out is moved to the carry flag and the carry flag bit is thrown away.

shl reg, imm

shl reg, cl

shl mem, imm

shl mem, cl

sal = shift arithmetic left

### Shift Right Instruction (shr/sar)

*Logical Shift right* shifts the bits of a value to the right by the number of bits specified starting with the highest bit which is changed to zero.  The lowest bit is moved to the carry flag and the original value in the carry flag is thrown away.

shr reg, imm

shr reg, cl

shr mem, imm

shr mem, cl

*Arithmetic Shift right* is the same as the logical shift except the highest bit is filled with the original signed bit.

sar reg, imm

sar reg, cl

sar mem, imm

sar mem, cl

## Rotate Left Instruction (rol)
The rotate operation doesn't discard bits.  The bit which is rotated out of one end will be filled to the other end.

The highest bit rotated out will be filled to the lowest bit position and copied to the carry flag as well.

rol reg, imm

rol reg, cl

rol mem, imm

rol mem, cl

### Rotate Carry Left (rcl)
*Rotate Carry Left* shifts values to the left and uses the carry flag as an intermediate position.  The value in the carry flag is moved to the lowest bit.

rcl reg, imm

rcl reg, cl

rcl mem, imm

rcl mem, cl

- If you want to clear or set the carry flag before performing the rotate instruction you can use:

clc - clear carry flag

stc - set carry flag

## Rotate Right Instruction (ror)

The lowest bit rotated out will be filled to the highest bit position and copied to the carry flag as well.

ror reg, imm

ror reg, cl

ror mem, imm

ror mem, cl

### Rotate Carry Right (rcr)
*Rotate Carry Right* shifts value to the right and the lowest bit is assigned to the carry flag.  The value in the carry flag is moved to the highest bit.

rcr reg, imm

rcr reg, cl

rcr mem, imm

rcr mem, cl


## Strings

In order to process strings, you can use the *move*, *load*, *store*, and *compare* instructions.

A string ends with a single byte containing zero called a *null-terminated string*.

The instruction will increment or decrement rsi and rdi based on the *direction flag*.  If the direction flag is clear, rsi and rdi will be incremented. This is like forward direction.

The instruction processes the data from low memory address to high memory address.

If the direction flag is set then rsi and rdi will be decremented.  In this case, the instruction processes data from high memory address to low memory address.  This is like reverse direction.

The direction flag needs to be set to the desired value based on your needs before you process strings.

- cld - clear direction flag

- std - set direction flag

### Move Instruction (movs*)
The instructions copy the data in memory, pointed to by the register rsi to the memory pointed to by register rdi.

source: rsi

destination : rdi

| instruction | size | increment/decrement |
| --- | --- | --- |
| movsb | bytes | 1 |
| movsw | words | 2 |
| movsd | doublewords | 4 |
| movsq | quadwords | 8 |

### Store Instruction (stos*)

destination : rdi

stosb al

stosw ax

stosd eax

stosq rax

The rdi register is incremented or decremented based on the state of the direction flag.  If the direction flag is clear, rdi is incremented; otherwise rdi is decremented.

### Load Instruction (lods*)

source : rsi

lodsb al

lodsw ax

lodsd eax

lodsq rax

### Scan Instruction (sca*)
Use scan to look for a value in an array or a string.

destination : rdi

scasb al

scasw ax

scasd eax

scasq rax

### Compare Instruction (cmp*)
Compares in memory the data of registers rsi and rdi.  Status flags are set according to the results.  After the comparison, rdi and rsi registers increment or decrement based on the state of the direction flag.  If the direction flag is 0, the rsi and rdi registers increment.  Otherwise, the registers decrement.

source 1 : rsi

source 2 : rdi

cmpsb

cmpsw

cmpsd

cmpsq

## Stack And Procedures
A *procedure*, also known as a sub routine or function, is a sequence of instructions to perform a specific task.

A *stack* is used to save data on the procedures.  The stack data structure acts as a container with two operations, *push* and *pop*.

A stack frame is part of the stack set aside for parameters, return address, saved registers, and local variables.

The stack grows downward in memory, which means it grows toward the zero address.  The stack pointer, rsp register, holds the address of the top element of the stack.

### Push / Pop
- Push adds a new item to the top of the stack.
- Pop removes the item from the top of the stack.
- Push and Pop must be executed in pairs.
- Pushing or Popping to 8 bit / 32 bit registers is not allowed in 64 bit mode.

push imm

push reg

push mem

pop reg

pop mem

### Procedures
The procedure name is also a label which represents the first instruction of the procedure.  At the end of the procedure, use a return (**ret**) instruction to return from the procedure to the location where it was called.

### Call Instruction (call)
The call instruction pushes the return address on the stack and loads the called procedures address in the rip register.

call label

call reg

call mem

The operand size for the call procedure is 64 bits in 64 bit mode so you cannot use other bit registers.

### Nested Procedure Calls
A nested procedure calls another procedure before it returns.

If you execute a return instruction in a procedure, you need to make sure the state of the stack is the same as when the procedure starts.

### Passing Parameters
The values passed to a procedure is called the parameter.  They can be passed using registers or the stack.

Parameters can be passed to any general purpose register except rsp and rbp registers.

- rsp - stack pointer register

- rbp - frame pointer register

### Local Variable
A local variable is a variable that's local to a procedure.

### Calling Conventions
Calling conventions are a set of rules about procedures which specify how and where parameters are passed, which registers must be preserved, where return values are stored, and is responsible for cleaning up the stack.

#### Microsoft x64 Calling Convention
- First Four Parameters - rcx, rdx, r8, r9

- Return Value - rax

- Caller Saved Registers (volatile) - rax, rcx, rdx, r8, r9, r10, r11

- Callee Saved Registers (non volatile) - rbx, rbp, rdi, rsi, r12, r13, r14, r15

Volatile can be altered by called procedurs.  To preserve their value, save them on a stack before calling a procedure.

Non Volatile must be preserved by the procedures.

When calling a procedure, rsp register must be aligned on a 16 byte boundary.  You must provide 32 bytes of shadow space on the stack.  The caller should remove space allocated for parameters and shadow space.

### Macro
A macro is a named block of code, which can be called in a program.

- "% define" is a directive for a single-line macro.  A macro expansion is a text substitution.

### Multi-line Macro
A multi-line macro is a macro with a number of parameters.

- "% macro", name and number of parameters.  Then, "%endmacro"

### I/O Macros

PRINT_DEC size, data (signed)

PRINT_UDEC size, data (unsigned)

PRINT_HEX size, data

PRINT_STRING data

NEWLINE insert space in output window

Get DEC size, data (signed)

GET_UDEC size, data (unsigned)

GET_HEX size, data

GET_STRING data, max size

## Final Notes

In 64 bit mode, immediate value is generally 32 bits wide.  A value larger than 32 bits will be truncated.

The *mov* instruction is the only instruction that takes a 64 bit immediate value.
