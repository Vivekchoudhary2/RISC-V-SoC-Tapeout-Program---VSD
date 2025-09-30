# 📘 System on Chip (SoC)

## 🔹 What is a System on Chip (SoC)?
A **System on Chip (SoC)** is the integration of complex functionalities onto a **single silicon chip**.  

Instead of using discrete multiple chips for CPU, memory, I/O, specialized processors and connecting them onto a PCB, a SoC consolidates them into one compact package.

---

## 🔹 Example: Snapdragon 835 Mobile Platform
To better understand SoC, let’s look at the **Snapdragon 835 Mobile Platform**.  

This single silicon chip consists of various modules/parts that perform specialized functions:  

1. **Wi-Fi Module** – Enables wireless connectivity to networks.  
2. **Hexagon DSP** – Provides faster processing of audio and video signals.  
3. **Qualcomm Haven Security Module** – Enhances device security through advanced encryption and secure data handling.  
4. **Other Integrated Components** – CPU, GPU, modem, memory controllers, and more.  

Each of these parts performs different functions but, are all integrated onto a single chip.  

It is an entire system on a chip.

<div align="center">
  <img width="625" height="478" alt="Snapdragon 835 Example" src="https://github.com/user-attachments/assets/1aa702ad-c09a-45b1-9d0f-81a836feecd1" />
  <br/>
  <em>Figure: Dissection of Snapdragon 835 SoC showing integrated modules</em>
</div>

---

## 🔹 Components of a Typical SoC
A typical SoC incorporates several functional units as shown earlier:

1. **Central Processing Unit (CPU)**  
   - The key component that handles data processing, computations, and decision-making.  

2. **Memory**  
   - Includes both **RAM** (for temporary data generated while code is running) and **ROM** (for permanent storage such as the operating system code).  

3. **Peripheral Devices and Interfaces**  
   - Connect the SoC to external devices and the real world.  
   - Examples: USB, PCIe, UART, SPI, I²C.  

4. **Accelerated Functional Units**  
   - Specialized units that boost performance for specific tasks.  
   - Examples: Encryption/Decryption accelerators, audio/video signal processors.  

5. **Graphics Processing Unit (GPU)**  
   - Responsible for producing visuals on the screen.  
   - Also leveraged for highly parallel tasks such as matrix multiplications in **robotics, AI, and animation frameworks**.  

6. **Power Management Unit (PMU)**  
   - Regulates power usage within the SoC.  
   - Ensures efficient operation and extends battery life in portable devices.  

7. **Mixed-Technology Units**  
   - Combines **analog** and **digital** components to achieve required functionality.  
   - Examples: **MEMS** (Micro-Electro-Mechanical Systems) and **RF** (Radio Frequency) components.  

---

<details>
<summary>🔹 Types of SoCs</summary>

1. **Microcontroller-based SoC**  
   - Designed for simple control tasks in everyday devices.  
   - Known for **low power consumption** and **high efficiency**.  

2. **Microprocessor-based SoC**  
   - Oriented towards **data-intensive tasks** and capable of running full operating systems.  
   - Commonly used in smartphones, tablets, and embedded computers.  

3. **Application-Specific SoC (ASIC-SoC)**  
   - Custom hardware designed to **excel in specific performance areas**, such as graphics processing, AI, or multimedia applications.  
   - Optimized for **speed, efficiency, and dedicated functionality**.  

</details>

---

## 🔹 Why BabySoC is a Simplified Model for Learning SoC Concepts?
VSDBabySoC is a compact SoC and based on the RISC-V architecture. It incorporates RVMYTH microprocessor, an 8x phase-locked loop (PLL), and a 10-bit digital-to-analog converter (DAC).  

It is a complex system simplified down to its three most essential functions: processing, timing, and real-world communication.

---

# 🍼 Understanding VSDBabySoC: A Beginner's Guide to its Core Components

## 📖 Introduction: Your First Step into System on Chip (SoC) Design
The **VSDBabySoC** serves as a perfect starting point for learning **System on Chip (SoC) design** because it simplifies a complex system down to its three most essential functions:  
- **Processing**  
- **Timing**  
- **Real-world communication**  

It integrates three fundamental, open-source components into a compact SoC, allowing learners to see how essential **digital and analog parts** work together.

This document will break down each of these three building blocks:  
- **The Brain (RVMYTH)**  
- **The Pacemaker (PLL)**  
- **The Translator (DAC)**  

to reveal how they collaborate to create a functioning system.

---

## 🧠 1. The Brain: RVMYTH (The RISC-V CPU)
RVMYTH is the **central processing unit (CPU)** or the "brain" of the BabySoC. Its main function is to **execute instructions** and **manage the flow of data** through the system by communicating with the other components.

---

## ⏱️ 2. The Pacemaker: The Phase-Locked Loop (PLL)

### 2.1 What is the PLL's Primary Job?
The **Phase-Locked Loop (PLL)** acts as the system’s **pacemaker**. It generates a **stable, synchronized clock signal**, ensuring all components (CPU, DAC, etc.) work in harmony and avoid timing errors.

---

<details>
<summary>🔹 Why an On-Chip Clock is Essential</summary>

| Problem with Off-Chip Clocks | How the On-Chip PLL Solves It |
|-------------------------------|-------------------------------|
| **Clock Distribution Delays**: Signals weaken and get delayed over long wires. | Generates the clock locally, right where it’s needed. |
| **Clock Jitter**: Random timing variations cause synchronization errors. | Produces a stable, locked signal with minimal jitter. |
| **Different Frequency Needs**: Components may require different speeds. | Can multiply frequencies (e.g., 8x PLL generates 8× reference input). |
| **Crystal Frequency Deviations**: External crystals drift with age/temperature. | Provides an internal stable reference, correcting deviations. |

</details>

---

<details>
<summary>🔹 Inside the PLL</summary>

A typical PLL consists of three main parts working in a feedback loop:  
- **Phase Detector**: Compares input and output signals to generate an error signal.  
- **Loop Filter**: Processes the error signal into a stable control voltage.  
- **Voltage-Controlled Oscillator (VCO)**: Adjusts its output to match the reference signal.  

</details>

---

<details>
<summary>🔹 Phase-Locked Loop (PLL) Operation</summary>

The basic concept of a **Phase-Locked Loop (PLL)** is simple: it synchronizes the output frequency of an oscillator with the frequency of a reference signal by continuously comparing their phases and adjusting accordingly.

---

#### 🔑 Key Components
- **Phase Detector (PD)** – Outputs a voltage proportional to the phase difference between the reference signal and the oscillator signal.  
- **Voltage-Controlled Oscillator (VCO)** – Adjusts its frequency (increases or decreases) based on the applied control voltage in a nearly linear fashion.  
- **Loop Filter (LF)** – A low-pass filter that smooths the error signal from the phase detector, removing unwanted high-frequency components.  

---

<div align="center">
  <img width="754" height="416" alt="pll_bd" src="https://github.com/user-attachments/assets/f82c43ec-b572-4650-9a38-da05811691b8" />
  <br/>
  <em>Figure: Basic block diagram of a working PLL</em>
</div>

---

<div align="center">
  <img width="531" height="502" alt="Phase Detector Block Diagram" src="https://github.com/user-attachments/assets/2258636d-0d8a-4bec-ba52-ba090d8de9fc" />
  <br/>
  <em>Figure: Phase difference</em>
</div>

---

Within a phase detector, the phase of the input signal and reference signal is compared and a resulting difference or error voltage is produced. This error signal passes through a low-pass filter which removes any high-frequency elements of the signal. Once through the filter, the error signal is applied to the VCO as its tuning voltage.

So, when the output from the phase detector is passed to the loop filter and when that filtered signal is applied to the VCO, the VCO generates a corresponding error signal (voltage signal) trying to match the phase of the input signal to the reference signal by either increasing or decreasing the frequency of the input signal.

Initially, there will be some difference in phase between the two signals or in other words, the loop will be out of lock and the error voltage will pull the frequency of the VCO towards that of the reference, until it cannot reduce the error any further and the loop is locked.

A steady error voltage is produced indicating a constant phase difference between the input and reference signal. As the phase between these two signals is not changing, it means that the two signals are on exactly the same frequency.

</details>

---

## 🎵 3. The Translator: The Digital-to-Analog Converter (DAC)

### 3.1 What is the DAC's Primary Job?
The **Digital-to-Analog Converter (DAC)** converts **digital values** (0s and 1s) into **analog signals** that real-world devices (like speakers, displays, or sensors) can use.  
It does this by recognizing that each digit, or **bit**, in a binary number has a specific *weight* based on its position.  
This bit weight is calculated using powers of 2 (**2ⁿ**), where **n** is counted from right to left starting at 0:

- **Bit 0 (rightmost):** Weight = 2⁰ = 1  
- **Bit 1:** Weight = 2¹ = 2  
- **Bit 2:** Weight = 2² = 4  
- **Bit 3:** Weight = 2³ = 8  

---

### 3.2 The DAC in VSDBabySoC
In the VSDBabySoC design, we are utilizing a 10-bit DAC, which means it can take a digital input represented by 10 bits and convert it into an analog output. 

---

### 3.3 How DACs are Built
DACs are commonly implemented using two methods:

<details>
<summary>🔹 Weighted Resistor DAC</summary>

The weighted resistor method utilizes the summing operational amplifier circuit. The summing amplifier adds the input signals with different gains corresponding to their resistors.  

---

<div align="center">
  <img src="https://github.com/user-attachments/assets/5472ec80-6602-4be3-b860-fc3dd0273889" alt="Summing-Amplifier-for-DAC" />
  <br/>
  <em>Basic summing operational amplifier circuit</em>
</div>

---

<div align="center">
  <img src="https://github.com/user-attachments/assets/e86d383d-a74b-4ad5-a8f9-65bb14e0957c" alt="Weighted-Resistor-DAC" />
  <br/>
  <em>Modified summing operational amplifier circuit including switches for taking inputs</em>
</div>

---

</details>

<details>
<summary>🔹 R-2R Ladder DAC</summary>

- Uses only **two resistor values**: **R** and **2R**.  
- Much simpler, easier to manufacture, and scalable to higher bit counts.  

---

<div align="center">
  <img src="https://github.com/user-attachments/assets/ae169487-a2aa-4912-bbf7-b1c6a56e9209" alt="4-bit-R-2R-Ladder-DAC" />
  <br/>
  <em>4-bit R-2R Ladder DAC circuit</em>
</div>

---

</details>

For detailed and comprehensive example on how conversion actually takes place:  
🔗 https://www.electricaltechnology.org/2020/04/digital-to-analog-converter-dac.html 

---

### 🔄 Comparison of DAC Methods

| Feature                | Weighted Resistor Method                         | R-2R Ladder Method                       |
|-------------------------|-------------------------------------------------|------------------------------------------|
| **Resistor Values**     | Many unique, precisely scaled values            | Only two values (R and 2R)                |
| **Precision**           | Decreases with more bits                        | High precision, scalable to many bits     |
| **Practicality**        | Hard to implement for large binary numbers      | Easy to design and manufacture            |

---

## 🔗 4. The Big Picture: How They Work Together
The VSDBabySoC operates as a simple but complete data pipeline:  

1. **Clock Generation** – The **PLL (Pacemaker)** generates a stable clock signal.  
2. **Data Processing** – The **RVMYTH CPU (Brain)** uses the clock to update its register with digital data.  
3. **Analog Conversion** – The **DAC (Translator)** converts this digital data into an analog signal for external devices.  

---

## 🏁 5. Conclusion: A Perfect Model for Learning
The **VSDBabySoC** is an excellent educational tool because it clearly demonstrates the **three fundamental roles of an SoC**:  

- **Processing** → RVMYTH  
- **Timing** → PLL  
- **Interfacing** → DAC  

Its modularity highlights a core truth of SoC design:  
➡️ Individual components, each with a clear role, must work in **perfect synchrony** to bridge the **digital world** with our **analog reality**.
