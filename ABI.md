# ABI Basics (Application Binary Interface)

---

## What is an ABI?
- **Application Binary Interface (ABI)** defines the low-level interface between:
  - Application programs
  - The operating system
  - The processor hardware
- It specifies **how software uses hardware resources** such as:
  - Registers
  - Memory
  - System calls
- ABI is critical from:
  - **Processor designer perspective** (hardware–software contract)
  - **Programmer perspective** (writing portable and correct programs)

---

## ABI vs Architecture (Conceptual View)
- The ABI can be compared to the **external appearance of a building**:
  - Users interact with doors, switches, and elevators
  - Internal details (pipes, wiring) are hidden
- Similarly:
  - Programmers care about *what* a system does
  - They usually do not care *how* the processor is internally implemented
- ABI hides microarchitectural details while exposing a stable interface

---

## Layered Interaction in Computer Systems
Application programs do not directly access hardware. Instead, they use multiple layers:

### 1. API (Application Programming Interface)
- High-level interface provided by libraries
- Examples:
  - `stdio.h` in C
  - Java standard classes
- APIs are **language-specific**

### 2. ABI (Application Binary Interface)
- Connects compiled programs to:
  - Operating system
  - Instruction Set Architecture (ISA)
- Defines:
  - Calling conventions
  - Register usage
  - System call mechanism

---

## ISA and RTL
- **Instruction Set Architecture (ISA)**:
  - Defines the machine instructions visible to software
  - Examples:
    - RISC-V
    - ARM
    - x86
- **Register Transfer Level (RTL)**:
  - Describes how the ISA is implemented in hardware
  - Defines data movement between registers and logic blocks

---

## Accessing System Resources
- Applications cannot access hardware directly
- The ABI provides **system calls** that:
  - Transfer control to the OS
  - Allow safe access to hardware resources
- System calls use predefined registers and conventions

---

## Registers in RISC-V (ABI Perspective)
- RISC-V defines **32 integer registers**
- In RV64 architecture:
  - Each register is **64 bits wide** (XLEN = 64)
- ABI specifies:
  - Which registers hold arguments
  - Which registers must be saved/restored
  - Which registers are temporary

---

# Memory Allocation for Double Words (64-bit)

---

## Why 32 Registers?
- 32 registers provide:
  - Good performance
  - Reasonable hardware complexity
- Register index uses **5 bits** (`2^5 = 32`)
- This balance is ideal for RISC architectures

---

## Registers with XLEN = 64
- All integer registers are **64-bit wide**
- Registers:
  - Hold temporary data
  - Store addresses
- Large data structures cannot fit entirely in registers → use memory

---

## Loading Data into Registers
- Data can be:
  - Loaded directly from memory
  - Stored temporarily in registers
- Memory is **byte-addressable**:
  - Each address stores **1 byte (8 bits)**

---

## Memory Organization
- A **64-bit (double-word)** value occupies **8 bytes**
- These bytes are stored in **consecutive memory addresses**

---

## Endianness
### Little Endian (Used by RISC-V)
- Least Significant Byte (LSB) stored at the lowest address
- Example:
 - Address: M[0] M[1] M[2] ... M[7]
 - Data: LSB MSB


### Big Endian
- Most Significant Byte (MSB) stored first
- Byte order is reversed

---

## Addressing 64-bit Data
- Memory addresses increase by 1 byte
- A 64-bit value uses addresses:
- M[n] to M[n+7]
- 64-bit aligned addresses are multiples of 8:
- M[0], M[8], M[16], ...


---

# Representation of Load, Store, and Add

---

## 1. Registers and Memory Access
- Registers store 64-bit values
- Memory stores data byte by byte
- Load and store instructions move data between memory and registers

---

## 2. Loading Data from Memory
- Load instructions copy data from memory to registers
- Example (Load Double Word):
- assembly
- ld x0, 16(x23)
- Meaning:
- Base address in x23
- Offset = 16 bytes
- Load 64-bit value into x0

## 3. Instruction Encoding

- RISC-V instructions are 32 bits wide
- Fields include:
- Opcode ---> LSB
- Source registers
- Destination register
- Immediate (offset) ---> MSB

## 4. Addition Using Registers

Example:

- add x0, x1, x2
- Operation:
- x0 = x1 + x2
- This is an **R-Type** instruction

## 5. Storing Data Back to Memory

Store instructions copy data from registers to memory
Example:
- sd x0, 8(x23)
- Stores contents of x0 into memory at address x23 + 8

## 6. Limited Registers and Memory Usage

Registers are limited resources
- Compilers:
- Spill values to memory
- Reload them when required

## RISC-V Instruction Types and Registers

- Instruction Categories

- **R-Type:**
    - Register-to-register operations
    - Example: add

- **I-Type:**
      - Register + immediate
      - Example: ld

- **S-Type:**
      - Store instructions
      - Example: sd

**Register Encoding**

Each register field is 5 bits
Allows 32 registers
Same encoding used across instruction formats

## RISC-V Register Naming (ABI Convention)

|Register|	  |Name|	   |Purpose|
|x0|	        |zero|	   |Constant 0|
|x1|          | ra |      Return address
|x2|	        | sp |      Stack pointer
|x3|	        | gp |	      Global pointer
|x4|            tp	      Thread pointer
|x5–x7|	       t0–t2	    Temporaries
|x10–x17|	     a0–a7	    Function arguments
|x18–x27|	     s1–s11	    Saved registers
|x28–x31|	     t3–t6	    Temporaries

## Role of ABI in Register Usage

**ABI defines:**
 - Which registers a function can overwrite
 - Which registers must be preserved
 - How arguments and return values are passed
 - This ensures:
       - Compatibility across compilers
       - Correct function calls
       - Stable system behavior
