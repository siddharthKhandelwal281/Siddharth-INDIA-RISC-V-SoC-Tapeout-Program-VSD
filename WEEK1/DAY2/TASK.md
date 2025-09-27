# 📘 Day 2: Timing Libraries, Synthesis Styles, and Flop Coding

This session explores how **timing libraries**, **synthesis strategies**, and **RTL coding styles** directly influence synthesis quality, area, power, and timing closure.

---

## 🔹 Timing `.lib` Files

**Liberty (.lib)** is a text-based format describing:

* ✅ **Cell function**
* ✅ **Pin directions & capacitances**
* ✅ **Input transition limits**
* ✅ **Setup/Hold & Clock-to-Q tables** (vs. input slew and output load)
* ✅ **Operating conditions (corners)**
* ✅ **Cell area & power models**

**Why it matters:** Synthesis and STA tools depend on `.lib` data for gate selection, timing interpolation, and power estimation.

---

## 🧪 Labs: `.lib` Exploration (Parts 1–3)

* Inspect **inverter/NAND entries** → check function, `related_pin` arcs, timing/power tables.
* Change **load/slew values** → observe delay/power interpolation.
* Understand **buffering and sizing trade-offs**.

---

## 🔹 Hierarchical vs Flat Synthesis

| Approach         | Pros                                                            | Cons                                            |
| ---------------- | --------------------------------------------------------------- | ----------------------------------------------- |
| **Hierarchical** | Preserves module boundaries, faster compile, easier debug/reuse | May miss cross-boundary optimizations           |
| **Flat**         | Enables global optimization, better timing/area                 | Higher runtime, harder debug, ECOs more complex |

---

## 🧪 Labs: Hierarchical vs Flat (Parts 1–2)

* Synthesize same RTL with both **hierarchical** and **flat** modes.
* Compare:

  * Gate count
  * **WNS/TNS** (Worst/Total Negative Slack)
  * Netlist readability
* Observe:

  * Flat synthesis may reduce redundant logic.
  * Hierarchical keeps structure, easier constraints/ECOs.

---

## 🔹 Why Flop Coding Styles Matter

Coding style impacts:

* **Latch inference** risk.
* **Timing analysis** (setup/hold paths).
* **Synthesis-friendliness**.

**Best Practices:**

* Use **non-blocking (`<=`)** in clocked always blocks.
* Use **blocking (`=`)** with complete assignments in combinational logic.
* Prefer **single-clock synchronous resets** (cleaner timing).

---

## 🧪 Labs: Flop Synthesis & Simulation (Parts 1–2)

* Simulate **DFFs** with sync/async resets and enables.
* Verify **Clock-to-Q behavior** in waveforms.
* Study **metastability handling assumptions**.
* Compare synthesized cells → area vs timing trade-offs.

---

## 🔹 Interesting Optimizations

* **Constant propagation:**

  * Tie-offs and unreachable logic removed.
  * MUXes collapse to simpler gates.
  * ✅ Saves area & power.

* **Register optimizations:**

  * **Retiming**: moves registers to balance paths.
  * **Enable extraction**: merges/moves flops under clock-enable conditions.
  * ✅ Helps timing while preserving cycle accuracy.

---

## ✅ Takeaways

* `.lib` is the **foundation** for timing and power-aware synthesis.
* Synthesis style (hierarchical vs flat) changes **runtime, optimization quality, and ECO flow**.
* RTL coding style directly impacts **latch inference, timing correctness, and synthesis robustness**.
* Flop optimizations and constant propagation enable **cleaner, smaller, and faster designs**.
