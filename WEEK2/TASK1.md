# Week 2 Task – BabySoC Fundamentals & Functional Modelling  

## 🎯 Objective  
The objective of this task is to build a solid understanding of **System-on-Chip (SoC)** fundamentals and practice **functional modelling** of the BabySoC using **Icarus Verilog** and **GTKWave**.  

---

## 📘 Part 1 – Theory (Conceptual Understanding)  

### 🔹 What is a System-on-Chip (SoC)?  
A **System-on-Chip (SoC)** is a single integrated circuit that combines all essential components of a computer system into one chip.  
- Unlike traditional systems that use multiple ICs, SoCs integrate everything together.  
- They are widely used in **smartphones, IoT devices, embedded systems, and consumer electronics** because of their **compact size, low power consumption, and cost efficiency**.  

---

### 🔹 Components of a Typical SoC  
A typical SoC consists of:  
- **CPU (Processor Core):** Executes instructions and manages computations.  
- **Memory:** Includes on-chip **RAM** (temporary storage) and **ROM** (boot/program storage).  
- **Peripherals:** Interfaces like **UART, GPIO, I2C, SPI, timers** that enable communication with external devices.  
- **Interconnect (Bus):** The backbone that connects CPU, memory, and peripherals for efficient data transfer (e.g., AMBA, Wishbone).  

---

### 🔹 Why BabySoC?  
**BabySoC** is a simplified model of a System-on-Chip created for **educational learning**:  
- Removes unnecessary complexity while keeping the **core SoC principles**.  
- Provides hands-on exposure to:  
  - CPU–Memory interaction  
  - Peripheral integration  
  - Data communication via interconnects  
- Helps learners **grasp fundamentals first** before moving to large, real-world SoC designs.  

---

### 🔹 Role of Functional Modelling  
Functional modelling is the **first stage of verification** in SoC design:  
- Focuses on whether the design **behaves correctly** as per specifications.  
- Occurs **before RTL coding and physical design** stages.  
- Advantages:  
  - Detects logical/functional issues early.  
  - Allows simulation of interactions between CPU, memory, and peripherals.  
  - Saves time and effort in debugging later design stages.  

**Tools Used:**  
- **Icarus Verilog** → For compiling and simulating the design.  
- **GTKWave** → For analyzing simulation waveforms and verifying functionality.  

---

## ✅ Deliverable  
This document summarizes:  
- Fundamentals of SoC design  
- BabySoC as a learning platform  
- Importance of functional modelling in SoC design flow  

This forms the foundation for upcoming tasks where BabySoC will be simulated and analyzed.  

