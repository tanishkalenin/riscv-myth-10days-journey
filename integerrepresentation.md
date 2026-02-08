# Integer Number Representation

## Introduction to 64-bit Binary Numbers
- **Decimal vs. Binary**: Humans work with decimal numbers, whereas computers operate using binary (base-2). Therefore, a conversion mechanism is required to translate between these two number systems.
- **Example**: A 64-bit binary number is commonly used in modern computer systems to represent data such as addresses, instructions, and integer values processed by the CPU.
- **Importance**: Understanding binary number representation is fundamental to understanding how data is stored, processed, transferred, and manipulated inside a computer system.

---

## Basic Structure of 64-bit Representation
- **Word Definition**: A word refers to a fixed-size unit of data processed by a processor. In modern systems, a word is typically 32 bits or 64 bits.
- **Least Significant Bit (LSB)**: The rightmost bit in a binary number. It represents the smallest value.
- **Most Significant Bit (MSB)**: The leftmost bit in a binary number. It represents the highest value and may indicate the sign in signed representations.
- **Byte**: A byte consists of 8 bits.  
  - 1 word (32-bit) = 4 bytes  
  - 1 double word (64-bit) = 8 bytes (2 words)

---

## Unsigned Binary Representation
- **Formula**: Using `n` bits, the total number of possible bit patterns is `2^n`.  
  - Example: Using 3 bits → `2^3 = 8` possible values (0 to 7).
- **64-bit Representation**: In a 64-bit unsigned system, there are `2^64` unique patterns, allowing representation of extremely large numbers.

---

## Understanding Large Numbers
- **Representation**: A binary number is interpreted by summing the weighted values of each bit, where each bit position corresponds to a power of 2.
- **Overflow Flag**: When arithmetic operations exceed the maximum value that can be represented using 64 bits, an overflow condition occurs and the overflow flag is set.

---

## Maximum Unsigned Number in 64-bit
The largest value representable using a 64-bit unsigned integer is:


---

## Signed vs. Unsigned Numbers
- **Unsigned Numbers**
  - Represent only non-negative values
  - Range: `0` to `2^64 - 1`
- **Signed Numbers**
  - Represent both positive and negative values
  - Use **two’s complement** to represent negative numbers

---

## Negative Numbers and Two's Complement

### 1. Two’s Complement Representation
- Two’s complement is the standard method used by modern processors to represent signed integers.
- To represent a negative number:
  1. Invert all bits (1’s complement)
  2. Add `1` to the result

### 2. MSB (Most Significant Bit)
- **MSB = 0** → Positive number  
- **MSB = 1** → Negative number

### 3. Converting Negative Numbers
- Identify MSB = 1
- Take the two’s complement
- Convert to decimal and apply a negative sign

### 4. Binary Representation Rules
- Positive numbers are represented directly in binary
- Negative numbers are represented using two’s complement

### 5. Range of Signed 64-bit Numbers
- Largest positive number:
- Smallest negative number:

### 6. Binary to Decimal Conversion
- **Positive numbers**: Direct binary-to-decimal conversion
- **Negative numbers**:
  - MSB = 1
  - Apply two’s complement
  - Use `-2^(n-1)` for MSB weight

### 7. Special Observations
- MSB determines the sign of a signed number
- Two’s complement simplifies arithmetic operations

### 8. Range of Numbers in RV64 Architecture
- Unsigned integers range: `0` to `2^63 - 1`
- Signed integers range: `-2^63` to `-1`

---

## Application in Integer Instructions (RISC-V Architecture)

### Handling Integers in RISC-V
- RV64 uses 64-bit registers
- Signed and unsigned integers use the same storage format
- Instruction type determines signed or unsigned interpretation
- Two’s complement is used for signed arithmetic
