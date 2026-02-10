# Makerchip Platform
# Understanding Multiplexers (MUX) using TL-Verilog

📌 Introduction

A Multiplexer (MUX) is a fundamental combinational digital circuit that selects one of multiple input
signals and forwards it to a single output line. It works like a digital switch, where the selection is
controlled by one or more select lines.

Multiplexers are widely used in:
- Data routing
- CPU datapaths
- Memory addressing
- Control logic design

This project demonstrates 2-to-1 and 4-to-1 multiplexers, along with their Verilog / TL-Verilog
implementations, using the Makerchip IDE.

---

🛠️ 2-to-1 Multiplexer (Basic MUX)

🔹 Description

A 2-to-1 MUX selects one of two inputs based on a single select signal.

🔹 Inputs

x1 : Data input 1  
x2 : Data input 2  
s  : Select signal (1-bit)

🔹 Output

f : Selected output

---

🔢 Truth Table

| Select (s) | Output (f) |
|------------|------------|
| 0          | x2         |
| 1          | x1         |

---

🧮 Boolean Expression

f = (s & x1) | (~s & x2)

---

💻 Verilog Implementation (Ternary Operator)

```verilog
assign f = s ? x1 : x2;

he ternary operator (? :) behaves like an if–else statement:

If s = 1 → output is x1

If s = 0 → output is x2

This implementation is:

Concise

Readable

Efficient for synthesis

🧩 4-to-1 Multiplexer (Extended MUX)

🔹 Description

A 4-to-1 MUX selects one of four inputs using a 2-bit select signal.

🔹 Inputs

a, b, c, d : Data inputs
sel[1:0] : Select lines

🔹 Output

f : Selected output

🔢 Selection Logic

|sel[1:0]|	Output|
|--------|---------|
|00	     |     a   |
|01	     |     b   |
|10	     |    c    |
|11	     |    d     |

💻 Verilog Implementation (Ternary Chain)

assign f = (sel == 2'b00) ? a :
           (sel == 2'b01) ? b :
           (sel == 2'b10) ? c : d;


✅ Why Ternary Chains Are Preferred

Compact syntax

High readability

Optimized hardware synthesis

Easy scalability

🚀 Makerchip IDE – TL-Verilog Integration

Makerchip is an online IDE specifically designed for TL-Verilog, enabling faster and more intuitive
hardware design.

🔧 Key Features

✅ Browser-Based Code Editor – No local installation required
✅ Live Cloud Simulation – Instant waveform generation
✅ Automatic Circuit Visualization – RTL to schematic view
✅ Waveform Viewer – Signal-level debugging over time

✅ Integrated Debugging Tools

Syntax error highlighting

Direct navigation to faulty logic

✅ Save & Clone Projects

Bookmarkable project URLs

✅ Built-in Documentation & Examples

🧭 Using Makerchip (Workflow)

1. Open Makerchip IDE

2. Navigate to Examples section

3. Select the required TL-Verilog example

4. Modify the code for your design

5. Run simulation

6. Observe waveforms and circuit diagrams
