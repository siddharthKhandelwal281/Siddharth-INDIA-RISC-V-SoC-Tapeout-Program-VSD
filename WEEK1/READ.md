# 📕 VLSI Design — Week 1

This repository documents **Week 1** of RTL-to-GDS learning using **Verilog, Icarus Verilog, GTKWave, and Yosys with Sky130 PDK**.
It includes **concepts, labs, and Verilog examples** from **Day 1 → Day 5**.

---

## 📘 Day 1: Verilog RTL, Simulation, and Open-Source Synthesis

### 🔹 Verilog RTL Design

* RTL describes **cycle-accurate behavior** mapped to gates and flops.
* Best practices: complete assignments, non-blocking (`<=`) in clocked blocks.

### 🔹 Simulation with Icarus Verilog

* Flow: `iverilog` → `vvp` → GTKWave for waveform inspection.
* Supports `$dumpfile` / `$dumpvars` for VCD generation.

### 🧪 Labs

* Build testbench, dump signals, visualize in GTKWave.
* Exercise: clock/reset sequencing, output checking.

### 🔹 Yosys Synthesis

* Flow: `read_verilog → proc/opt → abc → write_verilog/json`.
* Sky130 PDK used for gate mapping.

### 🧪 Labs

* Synthesize **1-bit mux (“good mux”)**.
* Verify RTL vs gate-level netlist equivalence with GTKWave.

---

## 📘 Day 2: Timing Libraries, Synthesis Styles, and Flop Coding

### 🔹 Liberty (`.lib`) Files

* Describe cell function, pin directions, capacitance, setup/hold, clock-to-Q, power, corners.
* Used by synthesis and STA for timing/power analysis.

### 🧪 Labs

* Inspect inverter/NAND entries → arcs, tables.
* Change load/slew → observe interpolation.

### 🔹 Hierarchical vs Flat Synthesis

* **Hierarchical:** preserves boundaries, easier debug, less optimization.
* **Flat:** global optimization, better area/timing, harder ECO/debug.

### 🧪 Labs

* Compare gate count, WNS/TNS, netlist readability for hierarchical vs flat.

### 🔹 Flop Coding Styles

* Non-blocking (`<=`) for sequential logic.
* Blocking (`=`) with `always @(*)` for combinational logic.
* Prefer synchronous resets.

### 🧪 Labs

* Simulate DFFs with async/sync resets and enables.
* Compare synthesized flop choices under constraints.

### 🔹 Optimizations

* **Constant propagation** → tie-offs removed, mux collapse.
* **Register retiming/enable extraction** → balance timing paths.

---

## 📘 Day 3: Combinational and Sequential Optimizations

### 🔹 Combinational Optimization

* Reduce gates with constant propagation & Boolean simplification.

**Example:**

```
Y = ((A & B) | C)' → Y = C' (when A=0)
```

### 🔹 Sequential Optimization

* Remove logic driven by constant flops.
* State optimization, retiming, logic cloning.

### 🔹 Boolean Simplification

* Reduces nested muxes → simpler XOR forms.

### ✅ Benefits

* Lower gate count → area/power reduction.
* Shorter depth → better timing closure.

### 💻 Example Code Snippets

* `opt_check.v`, `opt_check2.v`, `opt_check3.v`
* `dff_const1.v`, `dff_const2.v`, `dff_const3.v`
* `counter_opt.v`

---

## 📘 Day 4: Handling Simulation Mismatch & Verilog Assignments

### 🔹 Gate-Level Simulation (GLS)

* Run same testbench on RTL vs synthesized netlist.
* Use `iverilog` + GTKWave for `.vcd` inspection.

### 🔹 Synthesis-Simulation Mismatch

* Causes:

  1. Missing sensitivity list in combinational blocks.
  2. Wrong use of blocking (`=`) vs non-blocking (`<=`).

### ✅ Rules

* Sequential logic (`@posedge clk`) → use non-blocking (`<=`).
* Combinational (`always @(*)`) → use blocking (`=`).

### 🧪 Labs

* **Task 1:** GLS mismatch with bad sensitivity list (`bad_mux.v` vs `ternary_operator_mux.v`).
* **Task 2:** Blocking in sequential logic (`blocking_caveat.v`).

---

## 📘 Day 5: IF/CASE Constructs, Latch Inference & Generate Statements

### 🔹 IF/CASE Constructs

* Complete coverage avoids latches.
* Overlapping cases → ambiguity → use `unique case` or ordered if-else.
* Always include **default** branch.

### 🔹 Latch Inference

* Happens when outputs left unassigned.
* Avoid unless intentional.

### 🔹 For-Generate Loops

* Replicate hardware with static bounds.
* Useful for mux, demux, and RCA.

### 🧪 Labs & Code Examples

* Incomplete vs complete case (`incomp_case.v`, `comp_case.v`).
* Incomplete IF (`incomp_if.v`, `incomp_if2.v`).
* Bad case (`bad_case.v`).
* Generate MUX/DEMUX (`mux_generate.v`, `demux_case.v`, `demux_generate.v`).
* Ripple-Carry Adder (`rca.v` + `fa.v`).

### ✅ Takeaways

* Cover all branches → prevent latches.
* Default cases mandatory.
* For-generate loops → scalable structural design.

---

# ✅ Week 1 Summary

* **Day 1:** RTL design, simulation, Yosys intro.
* **Day 2:** Timing libs, synthesis styles, flop coding.
* **Day 3:** Combinational & sequential optimizations.
* **Day 4:** Simulation mismatches, blocking vs non-blocking.
* **Day 5:** IF/CASE constructs, latch inference, generate loops.

👉 This completes **Week 1 (Day 1–5)** of RTL-to-GDS flow fundamentals.
