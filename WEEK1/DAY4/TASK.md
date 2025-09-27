# Day 4: Handling Simulation Mismatch & Verilog Assignments

This session focused on advanced verification topics essential for reliable VLSI design, specifically:

* Gate-Level Simulation (GLS)
* Synthesis-Simulation Mismatch
* Correct usage of Blocking and Non-Blocking assignments in Verilog

---

## 1️⃣ Gate-Level Simulation (GLS)

| Aspect                     | Explanation                                                                                                                   |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| **What is GLS?**           | Running the same test bench used for RTL, but with the actual gate-level implementation (Netlist) of the design.              |
| **Why is it needed?**      | To verify the logical correctness of the design after synthesis. Ensures gate-level design behaves exactly like RTL.          |
| **Flow (using iverilog):** | Design, Gate-Level Models, and Test Bench are passed to `iverilog`, which generates a `.vcd` file for viewing in **GTKWave**. |

---

## 2️⃣ Synthesis-Simulation Mismatch

Occurs when the RTL simulation works, but the synthesized netlist behaves differently.

### 🔹 2.1 Missing Sensitivity List

* In combinational logic, missing input signals in the sensitivity list can cause mismatches.
* **Best Practice:** Always use `always @(*)` to automatically include all inputs.

### 🔹 2.2 Blocking vs. Non-Blocking Assignments

| Assignment Type  | Symbol | Behavior                                               | Use Case                                                    |
| ---------------- | ------ | ------------------------------------------------------ | ----------------------------------------------------------- |
| **Blocking**     | `=`    | Executes sequentially in order written                 | Used in **combinational logic** (`always @(*)`)             |
| **Non-Blocking** | `<=`   | Evaluates RHS in parallel, assigns at end of time step | Mandatory in **sequential logic** (`always @(posedge clk)`) |

---

## 🧪 Lab Tasks & Results

### Lab Task 1: GLS & Sensitivity List Issue

* **Goal:** Show mismatch caused by missing signals in sensitivity list.

```verilog
module ternary_operator_mux (
    input  i0,
    input  i1,
    input  sel,
    output y
);
    assign y = sel ? i1 : i0;
endmodule
```
<img width="1859" height="1049" alt="image" src="https://github.com/user-attachments/assets/cc63d8aa-1d9c-4975-8d83-178cc6d4545d" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/9eeaba37-f887-4c98-8302-1cdc3222080d" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/079dfbd2-ba4e-4970-841b-8762dbb113c3" />

```verilog
module bad_mux (
    input  i0,
    input  i1,
    input  sel,
    output reg y
);
    always @(sel) begin
        if (sel)
            y <= i1;
        else
            y <= i0;
    end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/b333f2bd-cd02-499e-a548-5b2efe4b07f7" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/e9691300-b1cb-4240-993d-efc73d8a4a7d" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/cb8a2a37-c0c6-4ce8-abb8-9d7844982cb1" />

📊 **Expected:** Mismatch visible in **GTKWave** between correct and bad code.

---

### Lab Task 2: Blocking vs. Non-Blocking Issues

* **Goal:** Show mismatch when blocking (`=`) is used in sequential logic.

```verilog
module blocking_caveat (
    input a, input b, input c,
    output reg d
);
    reg x;
    always @(*) begin
        d = x & c;
        x = a | b;
    end
endmodule
```
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/9ce1a16b-9eae-4071-8d55-438ae72a4057" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/0726acb0-d464-4988-9018-64c22dbdea54" />
<img width="1856" height="1046" alt="image" src="https://github.com/user-attachments/assets/d35d7653-8590-4e44-83c8-ecf7701b1f91" />

📊 **Result:** Simulation output differs from expected hardware behavior.

---

## 💡 Analysis & Takeaways

* ✅ **Sequential Logic:** Always use **non-blocking (`<=`)** with `@posedge clk`.
* ✅ **Combinational Logic:** Use **blocking (`=`)** with `always @(*)`.
* ✅ **Debugging Tool:** Gate-Level Simulation (GLS) is essential to catch synthesis mismatches.

---
