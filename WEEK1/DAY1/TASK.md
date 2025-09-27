# 📘 Day 1: Verilog RTL, Simulation, and Open-Source Synthesis

This session introduces **Verilog RTL design**, **simulation with open-source tools**, and **logic synthesis** using Yosys.

---

## 🔹 Verilog RTL Design and Synthesis

* **RTL (Register Transfer Level):**

  * Describes **cycle-accurate behavior** using combinational and sequential constructs.
  * Synthesizers map RTL → **gates and flip-flops**.

* **Best Practices:**

  * Always write **complete assignments** in combinational blocks.
  * Use **non-blocking (`<=`)** assignments in clocked blocks.
  * Ensures **simulation = synthesis intent**.

---

## 🔹 Open-Source Simulator: Icarus Verilog

* **Icarus Verilog (`iverilog`)**: compiles RTL + testbench into a runnable simulation.
* **VCD waveform dumping:** `$dumpfile`, `$dumpvars`.
* **GTKWave**: view and debug signal transitions.

**Typical Flow:**

1. Compile: `iverilog -o simv design.v tb.v`
2. Run: `vvp simv`
3. View: open `dump.vcd` in GTKWave

---

## 🧪 Labs: Icarus Verilog and GTKWave

* **Part 1:** Write a simple testbench, print results.
* **Part 2:** Add `$dumpfile` / `$dumpvars` for VCD output.
* **Part 3:** Inspect waveforms in GTKWave.

**Key Skills Practiced:**

* Stimulus generation
* Clock/reset sequencing
* Output checking against expected behavior

---

## 🔹 Intro to Yosys and Logic Synthesis

* **Yosys Flow:**

  1. `read_verilog` – parse RTL
  2. `hierarchy` – resolve modules
  3. `proc; opt` – process and optimize
  4. `abc` – map logic to standard cells
  5. `write_verilog` or `write_json` – output netlist

* Performs **optimizations:** constant propagation, Boolean simplification, tech mapping.

---

## 🧪 Labs: Yosys with Sky130 PDKs

* Build a **1-bit mux (“good mux”)** using Sky130 standard-cell library.
* Inspect synthesized netlist and chosen cells.
* Verify **functional equivalence**:

  * Simulate RTL and synthesized netlist with same testbench.
  * Compare waveforms in GTKWave.

---

## ✅ Takeaways

* Write **clean RTL** → ensures synthesis matches intent.
* Use **iverilog + GTKWave** for quick simulation/debugging.
* Yosys enables **open-source synthesis** with Sky130 PDK.
* Always verify **RTL vs gate-level equivalence** before moving forward.
