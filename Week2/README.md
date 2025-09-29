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
