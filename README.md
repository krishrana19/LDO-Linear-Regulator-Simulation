# Closed-Loop Linear Voltage Regulator (LDO Topology)

## 📌 Project Overview
This repository contains the design and simulation of a continuous-time $12\text{V}$ to $5\text{V}$ linear voltage regulator. The circuit was designed and validated using **TINA-TI** to demonstrate core analog principles including negative feedback, operational amplifier dynamics, and MOSFET continuous-conduction operation.

## ⚙️ Architecture & Theory of Operation
The regulator utilizes an operational amplifier acting as an error amplifier to drive an NMOS pass transistor operating in its saturation region. 
* **The Feedback Loop:** A $10\text{k}\Omega / 10\text{k}\Omega$ resistive voltage divider samples the output voltage and feeds it back to the inverting (-) terminal of the op-amp.
* **Error Correction:** The non-inverting (+) terminal is tied to a stable $2.5\text{V}$ DC reference. Utilizing the virtual ground concept, the op-amp dynamically adjusts the NMOS gate voltage (typically pushing it to $\sim8\text{V}$) to maintain equilibrium, forcing the source output to exactly $5\text{V}$.
* **Steady-State Error:** A minimal $3\text{mV}$ steady-state error was observed ($4.997\text{V}$ output), which accurately reflects the finite open-loop gain limitations of the LM324 op-amp model.

## 🛠️ Component Selection
* **Error Amplifier:** LM324 Operational Amplifier 
* **Pass Element:** IRF540 N-Channel Power MOSFET 
* **Feedback Network:** $10\text{k}\Omega$ / $10\text{k}\Omega$ Resistors
* **Voltage Reference:** $2.5\text{V}$ DC Source

---

## 📊 Simulation Results

### 1. DC Operating Point & Line Regulation
The baseline circuit was tested with a static $50\Omega$ load (drawing $100\text{mA}$). A DC voltage sweep was performed on the main supply rail from $6\text{V}$ to $15\text{V}$.
* **Result:** The control loop successfully rejects supply fluctuations, holding a flat, regulated $5\text{V}$ output across the entire operational range.

![Base Schematic](Images/Base_Schematic.png)
*Figure 1: Regulator Schematic with $50\Omega$ Static Load*

![DC Sweep Plot](Simulation_Plots/DC_Sweep_Line_Reg.png)
*Figure 2: DC Transfer Characteristic showing Line Regulation*

### 2. Transient Response & Load Regulation
To test the speed and stability of the feedback loop, the static load was replaced with a square-wave Current Generator toggling between $100\text{mA}$ and $500\text{mA}$ at $1\text{kHz}$.
* **Result:** The system demonstrated robust load regulation, rapidly correcting the voltage droop caused by the sudden current demand. The feedback loop achieved a highly responsive **$\sim2.5 \mu\text{s}$ recovery time** to return to steady-state $5\text{V}$.

![Transient Schematic](Images/Transient_Test_Schematic.png)
*Figure 3: Regulator Schematic with Square-Wave Current Generator*

![Transient Plot](Simulation_Plots/Transient_Load_Step.png)
*Figure 4: Transient Analysis demonstrating $2.5 \mu\text{s}$ recovery time during load steps*

---
## 📂 Repository Structure
* `/TINA_TI_Schematics/` - Contains the runnable `.TSC` simulation files.
* `/Simulation_Plots/` - Exported Bode/Transient and DC sweep data.
* `/Images/` - High-resolution schematic captures.