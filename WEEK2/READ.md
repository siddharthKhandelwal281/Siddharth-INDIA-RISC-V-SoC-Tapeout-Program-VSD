# 🧠 Week 2 Task – BabySoC Fundamentals & Functional Modelling  

## 🎯 Objective  
To build a solid understanding of **System-on-Chip (SoC)** fundamentals and perform **functional modelling** of the BabySoC using simulation tools — **Icarus Verilog (iverilog)** and **GTKWave**.

---

## 🧩 Part 1 – Theory (Conceptual Understanding)

### 🔹 What is a System-on-Chip (SoC)?  
A **System-on-Chip (SoC)** integrates all essential components of a complete computing system onto a single silicon chip.  
It combines the **processor**, **memory**, **peripherals**, and **interconnect** in one compact, power-efficient design.  
SoCs are used in smartphones, IoT devices, embedded systems, and consumer electronics.

---

### 🔹 Components of a Typical SoC  
- **CPU (Processor Core):** Executes instructions and performs computation.  
- **Memory:** Includes on-chip RAM (for temporary storage) and ROM (for program/boot code).  
- **Peripherals:** Interfaces such as **UART**, **SPI**, **I²C**, **GPIO**, **Timers**, etc.  
- **Interconnect (Bus):** Connects CPU, memory, and peripherals (e.g., AMBA or Wishbone).  

---

### 🔹 Why BabySoC?  
**BabySoC** is a simplified learning model that demonstrates the structure and functionality of a real SoC without unnecessary complexity.  
It helps beginners visualize:  
- CPU–Memory interaction  
- Dataflow via bus/interconnect  
- Peripheral integration  
By experimenting with BabySoC, learners can understand fundamental SoC behavior before moving on to advanced RTL and physical design.

---

### 🔹 Role of Functional Modelling  
Functional modelling verifies **behavioral correctness** of the design before RTL and physical design stages.  
It ensures that all modules communicate and respond correctly using simulation tools.  
**Advantages:**  
- Detects functional/logic errors early.  
- Saves time before hardware implementation.  
- Provides visibility into signal timing and dataflow.  

**Tools Used:**  
- **Icarus Verilog** → Compiles & simulates Verilog code.  
- **GTKWave** → Displays .vcd waveform files for analysis.

---

## ⚙️ Part 2 – Labs (Hands-on Functional Modelling)

### 🛠️ Tools Required  
- **Icarus Verilog (iverilog)**  
- **GTKWave**

---

### 🧾 Steps Performed  

#### 1️⃣ Clone the BabySoC Repository  
```bash
git clone https://github.com/hemanthkumardm/SFAL-VSD-SoCJourney.git
cd SFAL-VSD-SoCJourney/12. VSDBabySoC Project

```
#### 2️⃣ Compile Verilog Modules
```bash

iverilog -o baby_soc_tb.out baby_soc_tb.v
```

#### 3️⃣ Run Simulation and Generate Waveform
```bash
./baby_soc_tb.out
```
#### 4️⃣ View Waveform in GTKWave
```bash
gtkwave dump.vcd
```
#### 5️⃣ Analyze Key Operations
✅ Reset Operation: Check all signals initialize properly.

✅ Clocking: Ensure the clock toggles and drives all sequential logic.

✅ Dataflow: Observe signal transfer between CPU, memory, and peripherals.
