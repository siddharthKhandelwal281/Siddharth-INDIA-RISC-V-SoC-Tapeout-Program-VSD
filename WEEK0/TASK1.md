# 📘 Lecture 1: System-on-Chip (SoC) Design Summary

This document summarizes the key concepts from our first lecture on **System-on-Chip (SoC) design**.
Think of it as a **three-step journey** to transform a design idea into a real physical chip.

---

## 📝 Phase 1: Planning and High-Level Design

* 🔹 Begin with a **high-level plan** before building anything.
* 🔹 Use **C programming** to create a simple, working model of the chip.
* 🔹 This acts like a **blueprint** to validate the design idea before hardware construction.

---

## 🛠️ Phase 2: Building with Code

This is where the plan is turned into **hardware code**.

### 🔹 RTL (Register-Transfer Level)

* Use **Verilog** (hardware description language) to describe the chip.
* This serves as the **“soft copy”** of the chip design.

### 🔹 Breaking It Down

The design consists of three main building blocks:

1. **🧠 Processor (The Brain)**

   * Handles computations and controls the overall system.

2. **⚙️ Peripherals (The Helpers)**

   * Perform specific tasks, like communication with external devices.

3. **📦 Macros (Pre-Made Blocks)**

   * Pre-designed components (e.g., memory blocks) that can be directly reused.

---

## 🏗️ Phase 3: The Final Assembly

* 🔹 **Integration:** Combine processor, peripherals, and macros into one complete design.
* 🔹 **Physical Checks:**

  * 📐 **Floorplanning** → Place each component correctly on the chip.
  * 🔗 **Routing** → Connect components with wires.
* 🔹 **Final Blueprint:** Export the design as a **GDS II file** (the standard layout format sent to factories for fabrication).

