# 🚀 RISC-V Microarchitecture Overview

This document explains the architecture and implementation of a **simple RISC-V CPU microarchitecture**, including:

- Core components (PC, ALU, Register File, Memory)
- Control flow and branching
- Load/store operations
- Single-cycle execution model
- Next PC logic and reset handling
- Visualization and debugging using Makerchip

---

# 1️⃣ RISC-V Microarchitecture Basics

## What is RISC-V?

- **RISC-V** is an **Instruction Set Architecture (ISA)**.
- It defines the instructions a CPU can execute.
- It does NOT define how the CPU is internally built.

## What is Microarchitecture?

- The **microarchitecture** is the internal hardware design that implements the ISA.
- It includes:
  - Program Counter (PC)
  - Instruction Memory
  - Decode Logic
  - Register File
  - ALU
  - Data Memory
  - Control Logic

In this project, we build a **simple educational RISC-V CPU**.

---

# 2️⃣ Core Components of the CPU

## 🧭 A. Program Counter (PC)

- Holds the address of the **next instruction**
- Points into instruction memory
- Updates every clock cycle

Normal behavior:
```
PC = PC + 4
```

Why +4?
- Each RISC-V instruction is 32 bits (4 bytes)

If branch/jump occurs:
```
PC = branch_target
```

---

## 📘 B. Instruction Memory

- Stores program instructions
- Indexed by PC
- Returns fetched instruction to decode logic

Flow:
```
PC → Instruction Memory → Instruction
```

---

## 🔎 C. Instruction Decode Logic

Breaks instruction into fields:

- Opcode
- rs1 (source register 1)
- rs2 (source register 2)
- rd (destination register)
- Immediate value

Example:
```
add x1, x2, x3
```

Decode extracts:
- Opcode → ADD
- rs1 → x2
- rs2 → x3
- rd → x1

---

## 🗂 D. Register File

- Stores 32 general-purpose registers
- Two read ports
- One write port

Supports:
- Reading two registers simultaneously
- Writing one register per cycle

Flow:
```
rs1, rs2 → Register File → ALU
ALU result → Register File (rd)
```

---

## ➕ E. Arithmetic Logic Unit (ALU)

Performs:

- ADD
- SUB
- AND
- OR
- XOR
- Comparison operations

Acts like a calculator:
```
Input A
Input B
Operation select
→ Result
```

Result is written back to register file.

---

# 3️⃣ Branching and Control Flow

## Branch Instructions

Branch instructions:

- Contain immediate offset
- Contain condition

Example:
```
beq x1, x2, offset
```

If condition true:
```
PC = PC + offset
```

Else:
```
PC = PC + 4
```

---

## Branch Target Calculation

Branch target:
```
Branch Target = Current PC + Immediate Offset
```

Uses an adder.

---

# 4️⃣ Memory Access Instructions

## Load Instruction

```
lw x1, 16(x2)
```

Address calculation:
```
Address = x2 + 16
```

Data read from memory → written to x1

---

## Store Instruction

```
sw x3, 8(x4)
```

Address calculation:
```
Address = x4 + 8
```

Data from x3 → written to memory

---

# 5️⃣ Single-Cycle Execution Model

This workshop uses a simplified **single-cycle model**:

- Fetch
- Decode
- Execute
- Memory
- Write-back

All happen in one clock cycle.

Assumptions:
- No memory delay
- No multi-cycle operations
- Ideal behavior for learning purposes

---

# 6️⃣ Execution Flow Summary

1. PC fetches instruction
2. Instruction decoded
3. Registers read
4. ALU executes
5. Memory accessed (if needed)
6. Result written back
7. PC updated

---

# 7️⃣ Workshop Shell and Infrastructure

The provided GitHub repository includes:

- Preloaded instruction memory
- Register file implementation
- Data memory module
- Pass/fail communication logic
- Logging macros
- CPU visualization tools

The test program:
- Sums numbers from 1 to 9
- Runs for 40 cycles
- Indicates pass/fail automatically

---

# 8️⃣ Visualization in Makerchip

Visualization shows:

- Instruction memory (disassembled)
- Program Counter movement
- Register file updates
- Binary instruction representation
- Decode behavior
- Pipeline activity

Features:
- Wrong path instructions shown in gray
- Real-time register updates
- Instruction stepping

If visualization fails:
- Use waveform debugging

---

# 9️⃣ Debugging Using Waveform

Waveform shows:

- PC
- Instruction
- Register reads
- ALU outputs
- Control signals

Use waveform to:
- Verify PC increment
- Confirm register updates
- Detect incorrect branch behavior

---

# 🔟 Next PC Logic Implementation

## Basic Sequential PC Logic

```
$pc[31:0] = (>>1$pc + 32'd4);
```

But we must handle reset properly.

---

## Reset Handling

Requirement:
- After reset, PC must start at 0
- Must NOT skip first instruction

Correct TL-Verilog logic:

```verilog
$reset = *reset;

$pc[31:0] =
    (>>1$reset) ? 32'd0 :
    (>>1$pc + 32'd4);
```

Explanation:

- If previous cycle was reset → set PC to 0
- Else → increment PC by 4

---

## Why Use Previous Reset?

If we used direct reset:
- PC may increment immediately
- First instruction could be skipped

Using `>>1$reset` ensures:
- First post-reset cycle PC = 0
- Proper execution begins

---

# 1️⃣1️⃣ Verifying PC Behavior

Simulation checklist:

- After reset → PC = 0
- Next cycle → PC = 4
- Then → PC = 8
- Continues incrementing by 4
- Branch logic (added later) modifies PC correctly

---

# 1️⃣2️⃣ Future Branch & Jump Support

When branch logic is added:

```
if (branch_taken)
    PC = branch_target;
else
    PC = PC + 4;
```

Design should allow easy integration of branch logic later.

---

# 1️⃣3️⃣ Step-by-Step Development Strategy

1. Implement PC increment by 4
2. Add reset handling
3. Verify waveform
4. Add instruction fetch
5. Add decode
6. Add ALU
7. Add register write-back
8. Add memory operations
9. Add branch logic

Test each step individually.

---

# 🔥 Key Design Principles

- Keep logic modular
- Always verify using waveform
- Handle reset carefully
- Ensure PC never skips first instruction
- Design next PC logic extensibly
- Debug small components before integration

---

# 📌 Conclusion

This microarchitecture demonstrates:

- Core CPU building blocks
- Instruction execution flow
- Memory access handling
- Reset-safe PC logic
- Visualization-based debugging

It provides a strong foundation for:

- Pipelined CPU design
- Multi-cycle architectures
- Advanced RISC-V features

---

RISC-V CPU Microarchitecture Implementation  
Workshop-based structured learning project.
