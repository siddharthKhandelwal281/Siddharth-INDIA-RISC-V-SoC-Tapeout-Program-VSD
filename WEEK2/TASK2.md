# 🚀 Week 2 – BabySoC Fundamentals & Functional Modelling

This repository contains my work for **Week 2 / Task 2** of the **VSD BabySoC Project**.
The objective is to perform **functional modelling** of BabySoC using **Icarus Verilog** and **GTKWave**, and to analyze reset, clock, and dataflow signals.

---

## 📂 Repository Structure

```
week2-babysoc/
│── output/
│    ├── pre_synth_sim.out   # Simulation binary (compiled with iverilog)
│    ├── pre_synth_sim.vcd   # Waveform dump (for GTKWave)
│── screenshots/             # GTKWave screenshots for analysis
│── README.md                # Documentation (this file)
```

---

## ⚙️ Tools Used

* **Icarus Verilog (iverilog)** → compile & simulate Verilog design
* **VVP** → run simulation executable (`.out`)
* **GTKWave** → visualize waveforms from `.vcd` file

---

## 🛠️ Workflow

1. **Compile BabySoC design**

   ```bash
   iverilog -o output/pre_synth_sim.out src/*.v
   ```

2. **Run simulation & generate VCD**

   ```bash
   vvp output/pre_synth_sim.out
   ```

3. **Open waveform in GTKWave**

   ```bash
   gtkwave output/pre_synth_sim.vcd
   ```

---

## 🔎 Signal Analysis

### 1️⃣ Reset (`reset`)

* **Observation:**

  * When `reset = 1`, system is idle (DAC and OUT inactive).
  * When `reset = 0`, normal functional activity begins.

📸 Screenshot: <img width="1861" height="1045" alt="Screenshot from 2025-10-04 11-44-18" src="https://github.com/user-attachments/assets/95d8fa16-56f2-4506-880f-b065310a7bf9" />


---

### 2️⃣ Clock (`CLK`)

* **Observation:**

  * Clock toggles continuously.
  * Provides timing reference for sequential logic.

📸 Screenshot: <img width="1581" height="263" alt="Screenshot from 2025-10-04 12-42-22" src="https://github.com/user-attachments/assets/15df1543-1ffd-4d2b-87f7-15e704ed9adb" />


---

### 3️⃣ Dataflow Between Modules (`REF`, `OUT`, `RV_TO_DAC[9:0]`)

* **REF** → Input reference clock for PLL.
* **RV_TO_DAC[9:0]** → Digital values (088, 089, 078 …) showing data transfer from core → DAC.

**Dataflow Path:**

```
Core Logic → DAC → VCO → PLL Output (OUT)
```

📸 Screenshot: <img width="1861" height="1045" alt="Screenshot from 2025-10-04 11-52-50" src="https://github.com/user-attachments/assets/de17a60d-a72d-4cc7-89f7-8c7fd50ab202" />
<img width="1861" height="1045" alt="Screenshot from 2025-10-04 11-53-52" src="https://github.com/user-attachments/assets/c57167fd-06f3-4a53-aba0-a52e5ef10770" />


---

## ✅ Deliverables

* Simulation binary (`pre_synth_sim.out`)
* VCD waveform dump (`pre_synth_sim.vcd`)
* GTKWave screenshots (`screenshots/`)

---

## 📚 References

* [VSDBabySoC Project Labs](https://github.com/hemanthkumardm/SFAL-VSD-SoCJourney/tree/main/12.%20VSDBabySoC%20Project)
* VLSI System Design (VSD) SoC Journey

---
