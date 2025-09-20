# Week 0: Tools Installation & Setup

## Task 2: Installing VLSI Tools

This week's task was to set up our virtual machine with all the necessary open-source VLSI tools as per the course guidelines.
This is a crucial step that prepares our environment for the rest of the course projects.

---

## 🖥️ System Configuration

* **Operating System:** Ubuntu 20.04+
* **RAM:** 6GB
* **HDD:** 50GB
* **vCPU:** 4

---

## 🔧 Tool Installation & Verification

| Tool         | Description                               | Status      |
| ------------ | ----------------------------------------- | ----------- |
| **Yosys**    | A framework for RTL synthesis             | ✅ Completed |
| **Icarus**   | Verilog compiler and simulator            | ✅ Completed |
| **GTKWave**  | Waveform viewer for digital logic sims    | ✅ Completed |
| **NGSpice**  | Circuit simulator (analog & mixed-signal) | ✅ Completed |
| **Magic**    | VLSI circuit layout tool                  | ✅ Completed |

---

## 📜 Installation Commands

### 1. Yosys

```bash
sudo apt-get update
git clone https://github.com/YosysHQ/yosys.git
cd yosys
sudo apt install make   # (If not already installed)
sudo apt-get install build-essential clang bison flex \
libreadline-dev gawk tcl-dev libffi-dev git \
graphviz xdot pkg-config python3 libboost-system-dev \
libboost-python-dev libboost-filesystem-dev zlib1g-dev

make config-gcc
make
sudo make install
```
## ✅ Verification
<img width="1916" height="680" alt="Screenshot from 2025-09-20 20-06-01" src="https://github.com/user-attachments/assets/d6037719-74f2-4a27-9b15-4f2195d4f790" />

### 2. Icarus Verilog

```bash
sudo apt-get update
sudo apt-get install iverilog
```
## ✅ Verification
<img width="1919" height="814" alt="Screenshot from 2025-09-20 20-06-54" src="https://github.com/user-attachments/assets/021806d9-4504-4d3d-97da-94967eddbf98" />

### 3. GTKWave

```bash
sudo apt-get update
sudo apt install gtkwave
```
## ✅ Verification
<img width="1919" height="854" alt="Screenshot from 2025-09-20 20-07-59" src="https://github.com/user-attachments/assets/17f46a93-eec1-421f-898c-14eeb0e76ec8" />

### 4. NGSpice

```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure --with-x --with-readline=yes --disable-debug
make
sudo make install
```
## ✅ Verification
<img width="1919" height="710" alt="Screenshot from 2025-09-20 20-09-40" src="https://github.com/user-attachments/assets/025392e7-7261-4449-acc9-42b163731c54" />

### 5. Magic

```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev

git clone https://github.com/RTimothyEdwards/magic
cd magic
./configure
make
make install
```
## ✅ Verification
<img width="1919" height="1046" alt="Screenshot from 2025-09-20 20-10-20" src="https://github.com/user-attachments/assets/6c264d4e-248c-4c34-b766-565fdb385986" />

---
## ✅ Conclusion  

Each tool was verified by running version checks and confirming successful execution in the terminal.  
Snapshots of terminal outputs were recorded during installation.
