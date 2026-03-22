# Precision Photodiode Analog Front-End (AFE)

![Status: Complete](https://img.shields.io/badge/Status-Complete-success)
![Hardware: KiCad](https://img.shields.io/badge/Hardware-KiCad_9.0-blue)
![License: MIT](https://img.shields.io/badge/License-MIT-green)

## 📌 Project Overview
This repository contains the hardware design files and LTspice simulations for a high-precision, low-noise Photodiode Signal Conditioning Board. 

Designed as a modular Analog Front-End (AFE), this board converts ambient light intensity into a clean, stable analog voltage (0–3.3V) suitable for direct sampling by microcontrollers (e.g., ESP32, STM32, Arduino) using a Transimpedance Amplifier (TIA) architecture.

*(Insert a screenshot of your 3D PCB or Schematic here)*

## ✨ Key Features
* **Transimpedance Amplifier (TIA):** Converts microscopic photodiode currents into a measurable voltage with a calculated gain of 68kΩ.
* **Optimized Stability:** Includes a precisely calculated 20pF feedback capacitor to compensate for the photodiode's junction capacitance and prevent op-amp oscillation.
* **ADC Shock Absorption:** Features an RC low-pass output filter (100Ω + 10nF) to eliminate high-frequency noise and stabilize the signal against MCU ADC sampling glitches.
* **Ultra-Low Leakage:** Utilizes the MCP6001 CMOS operational amplifier with an input bias current of just 1pA to ensure the sensor signal is not degraded.
* **Plug-and-Play Interface:** Standard 3-pin connector (VCC, GND, OUT) for seamless integration into embedded systems.

## 🛠️ Hardware Specifications
| Component | Part / Value | Description |
| :--- | :--- | :--- |
| **Photodiode** | BPW34S | Broadband silicon photodiode. High photocurrent (~50µA at 1000 Lux), low dark current (2nA). |
| **Op-Amp** | MCP6001 | Single-supply, Rail-to-Rail Output (RRO), CMOS input (1pA Bias Current). |
| **Gain Resistor ($R_f$)** | 68 kΩ | Sets the voltage output range (Max 3.3V at ~50µA input). |
| **Compensation Cap ($C_f$)**| 20 pF | Prevents ringing/oscillation caused by the photodiode's 72pF junction capacitance. |
| **Supply Voltage** | 3.3V | Single-supply operation. Decoupled via 0.1µF capacitor. |

## 📐 Circuit Architecture & Theory

### 1. The Sensor Stage
The BPW34S photodiode is operated in photovoltaic/zero-bias mode. This configuration minimizes dark current leakage, resulting in the highest possible precision and lowest noise floor for ambient light detection.

### 2. The Transimpedance Stage
The core of the board is the TIA. The gain is set by the feedback resistor ($R_f$). 
Using Ohm's Law ($V = I \times R$), a peak ambient room light producing $~50 \mu A$ of current is multiplied by $68 k\Omega$ to produce a $~3.4V$ output, perfectly utilizing the 3.3V ADC range of modern microcontrollers.

### 3. Stability & Compensation
Photodiodes with large active areas (like the BPW34S) have high junction capacitance ($C_j \approx 72pF$). Without compensation, this capacitance creates a phase shift in the op-amp's feedback loop, causing severe ringing and instability. A 20pF feedback capacitor ($C_f$) was mathematically calculated and verified via SPICE simulation to critically damp the circuit and provide a smooth transient response.

## 📂 Repository Structure
* `/kicad` - KiCad 9.0 project files (Schematic, PCB Layout, Footprints).
* `/Simulation` - LTspice `.asc` files demonstrating Transient and AC (Frequency Response) analysis.
* `/Docs` - Datasheets for the BPW34S and MCP6001.
* `/Manufacturing` - Gerber files, Drill files, and BOM ready for PCB manufacturing (e.g., JLCPCB).
*  `/Media` - Project media and screenshots.

## 🚀 Getting Started
1. Clone this repository: `git clone https://github.com/shyver/Precision-Light-Sensor-AFE.git`
2. Open the `.pro` or `.kicad_pro` file in **KiCad**.
3. To view the simulations, open the `.asc` files located in the `/Simulation` folder using **LTspice**.

## 📝 License
This project is open-source and available under the [MIT License](LICENSE).
