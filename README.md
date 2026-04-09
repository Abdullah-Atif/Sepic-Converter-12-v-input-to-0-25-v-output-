# 🚀 High-Efficiency SEPIC Converter (12V to 0-30V)

This repository contains the design, simulation, and hardware implementation of a **SEPIC (Single-Ended Primary-Inductor Converter)**. Built as a part of my engineering project at **BUET**, it features an interactive web-based design tool and an Arduino-based $10\text{kHz}$ PWM controller.

---

## 🛠 Component Selection & Technical Specifications

Choosing the right components is critical for a SEPIC converter as it handles both input and output currents simultaneously.

### 1. Switching Element: IRLZ34N MOSFET
* **Drain-Source Voltage ($V_{DS}$):** $55\text{V}$ (Handles $V_{in} + V_{out}$ stress comfortably).
* **Current Rating ($I_D$):** $30\text{A}$ (Low $R_{DS(on)}$ ensures minimal heating).
* **Logic Level:** Optimized for direct $5\text{V}$ gate drive from **Arduino Uno**.

### 2. Power Diode: MBR6045WT (Schottky)
* **Current Rating ($I_F$):** $60\text{A}$ (High reliability under maximum load).
* **Reverse Voltage ($V_{RRM}$):** $45\text{V}$. (In SEPIC, diode stress $\approx V_{in} + V_{out} = 42\text{V}$).
* **Forward Drop ($V_F$):** $\approx 0.5\text{V} - 0.6\text{V}$, boosting overall efficiency.

### 3. Energy Storage: Inductors
* **Primary Inductor ($L_1$):** $70\mu\text{H}$ (Ferrite Core to minimize losses).
* **Secondary Inductor ($L_2$):** $30\mu\text{H}$ (Chosen based on saturation limits).
* **Ripple Formula:** $$\Delta I_L = \frac{V_{in} \cdot D}{L \cdot f_{sw}}$$
🔗 **[Launch inductance Calculator](https://coil32.net/online-calculators.html)**

---

## 🧮 Interactive Design Calculator

I have developed an advanced web-based tool hosted via **GitHub Pages** to calculate:
* **Duty Cycle Mapping:** Based on Arduino's 10-bit PWM.
* **Power Analysis:** Output Power ($P_{out}$) vs Input Power ($P_{in}$).
* **Component Stress:** Peak current ($I_{d,peak}$) and voltage stress.
* **Live Code Generation:** Automatically generates Arduino C++ code.

🔗 **[Launch SEPIC Calculator](https://abdullah-atif.github.io/Sepic-Converter-12-v-input-to-0-25-v-output-/)**

---

## 💻 Arduino PWM Control (10kHz)

Used **Timer 1** of the Arduino Uno to generate a **Fast PWM** to minimize audible noise and inductor ripple.

* **Frequency:** $10\text{kHz}$ (Configured via `ICR1` register).
* **Duty Cycle:** $0\% - 72\%$ (Potentiometer controlled).
* **Resolution:** $$TOP = \frac{F_{CPU}}{N \cdot F_{PWM}} - 1$$

---

## 📊 Performance Summary

* **Input Voltage:** $12\text{V}$ DC.
* **Output Range:** $0\text{V}$ to $30\text{V}$ DC.
* **Max Load:** $33\Omega$ ($\sim 0.77\text{A}$ @ $72\%$ Duty).
* **Efficiency ($\eta$):** $\approx 85\%$.
