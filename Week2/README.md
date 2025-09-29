What is a System-on-Chip (SoC)?

Components of a typical SoC (CPU, memory, peripherals, interconnect).

Why BabySoC is a simplified model for learning SoC concepts.

The role of functional modelling before RTL and physical design stages. 



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

Each of this part performs different functions but, are all integrated onto a single chip. 

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

## 🔹 Types of SoCs

1. **Microcontroller-based SoC**  
   - Designed for simple control tasks in everyday devices.  
   - Known for **low power consumption** and **high efficiency**.  

2. **Microprocessor-based SoC**  
   - Oriented towards **data-intensive tasks** and capable of running full operating systems.  
   - Commonly used in smartphones, tablets, and embedded computers.  

3. **Application-Specific SoC (ASIC-SoC)**  
   - Custom hardware designed to **excel in specific performance areas**, such as graphics processing, AI, or multimedia applications.  
   - Optimized for **speed, efficiency, and dedicated functionality**.  

## 🔹 Why BabySoC is a simplified model for learning SoC concepts?
VSDBabySoC is a compact SoC and based on the RISC-V architecture. It incorporates RVMYTH microprocessor, an 8x phase-locked loop(PLL) and a 10-bit digital-to-analog converter(DAC).

It is a complex system simplified down to its three most essential functions: processing, timing, and real-world communication.

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



## 🧠 1. The Brain: RVMYTH (The RISC-V CPU)
RVMYTH is the **central processing unit (CPU)** or the "brain" of the BabySoC. Its main function is to **execute instructions** and **manage the flow of data** through the system by communicating with the other components.


## ⏱️ 2. The Pacemaker: The Phase-Locked Loop (PLL)

### 2.1 What is the PLL's Primary Job?
The **Phase-Locked Loop (PLL)** acts as the system’s **pacemaker**. It generates a **stable, synchronized clock signal**, ensuring all components (CPU, DAC, etc.) work in harmony and avoid timing errors.

### 2.2 Why an On-Chip Clock is Essential

| Problem with Off-Chip Clocks | How the On-Chip PLL Solves It |
|-------------------------------|-------------------------------|
| **Clock Distribution Delays**: Signals weaken and get delayed over long wires. | Generates the clock locally, right where it’s needed. |
| **Clock Jitter**: Random timing variations cause synchronization errors. | Produces a stable, locked signal with minimal jitter. |
| **Different Frequency Needs**: Components may require different speeds. | Can multiply frequencies (e.g., 8x PLL generates 8× reference input). |
| **Crystal Frequency Deviations**: External crystals drift with age/temperature. | Provides an internal stable reference, correcting deviations. |

### 2.3 Inside the PLL
A typical PLL consists of three main parts working in a feedback loop:  
- **Phase Detector**: Compares input and output signals to generate an error signal.  
- **Loop Filter**: Processes the error signal into a stable control voltage.  
- **Voltage-Controlled Oscillator (VCO)**: Adjusts its output to match the reference signal.  

### ⏱️ Phase-Locked Loop (PLL) Operation

The basic concept of a **Phase-Locked Loop (PLL)** is simple: it synchronizes the output frequency of an oscillator with a reference signal by continuously comparing their phases and adjusting accordingly.  

---

#### 🔑 Key Components
- **Phase Detector (PD)** – Outputs a voltage proportional to the phase difference between the reference signal and the oscillator signal.  
- **Voltage-Controlled Oscillator (VCO)** – Adjusts its frequency (increases or decreases) based on the applied control voltage in a nearly linear fashion.  
- **Loop Filter (LF)** – A low-pass filter that smooths the error signal from the phase detector, removing unwanted high-frequency components.  

---

#### ⚙️ How It Works
1. A **reference signal** and the **VCO output** are provided to the **phase detector**.  
2. The **phase detector** produces an **error voltage** proportional to the phase difference between these two signals.  
3. This **error voltage** passes through a **low-pass filter**, which removes high-frequency noise.  
4. The filtered control voltage is then applied to the **VCO**, adjusting its frequency.  
5. The **VCO output** gradually aligns with the reference signal, ensuring both signals stay synchronized in phase and frequency.  

---

<div align="center">
  <img width="531" height="502" alt="Phase Detector Block Diagram" src="https://github.com/user-attachments/assets/2258636d-0d8a-4bec-ba52-ba090d8de9fc" />
  <br/>
  <em>Figure: Basic operation of a Phase Detector within a PLL system</em>
</div>

---

Within a phase detector, the phase of input signal and reference signal is compared and a resulting difference or error voltage is produced. This error signal passes through a low-pass filter which removes any high frequency elements of signal. Once through the filter, ther error signal is applied to VCO as its tuning voltage.

So, when the output from phase detector is passed to loop filter and when that filtered signal is applied to VCO, the VCO generates an corresponding error signal to match the phase of input signal to reference signal by either increasing/decreasing the frequency of input signal.


## 🎵 3. The Translator: The Digital-to-Analog Converter (DAC)

### 3.1 What is the DAC's Primary Job?
The **Digital-to-Analog Converter (DAC)** translates **digital values** (0s and 1s) into **analog signals** that real-world devices (like speakers, displays, or sensors) can use.

### 3.2 The DAC in VSDBabySoC
- **Type**: A **10-bit DAC**, capable of representing 1,024 distinct voltage levels.  
- **Function**: Receives digital data from **RVMYTH’s r17 register** and outputs the corresponding analog signal.  
- **Application**: The output is stored in a file named `OUT` and can be used by devices like **TVs, mobile phones, or speakers**.  

### 3.3 How DACs are Built
DACs are commonly implemented using:  
- **Weighted Resistor DAC**  
- **R-2R Ladder DAC**  

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
