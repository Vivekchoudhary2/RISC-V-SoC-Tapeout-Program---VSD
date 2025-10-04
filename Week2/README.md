# 📘 System on Chip (SoC) & VSDBabySoC LAB

---

<details>

<summary>📦 System on Chip (SoC)</summary>
	
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
</details>

---

<details>
<summary>🧪 LAB</summary>

Prerequisite steps for compiling BabySoC verilog modules:
```bash
$ git clone https://github.com/manili/VSDBabySoC.git
$ cd VSDBabySoC/src/module/
$ sandpiper-saas -i rvmyth.tlv -o rvmyth.v        # Convert the rvmyth.tlv file to rvmyth.v file. After this you will have file named 'rvmyth.v'.
$ sed -i '/^`line/d' rvmyth.v
$ sed -i '/^`line/d' rvmyth_gen.v                 # TL-Verilog to Verilog conversion (sandpiper) usually inserts `line directives into the generated .v file so that error messages can trace                                                      back to the original .tlv.
                                                  # Icarus Verilog (iverilog) does not like seeing those directives inside macro expansions, and it chokes on them. It is shown in the image
													below. The error rises when putting modules through iverilog simulator.

                                                  # If still any '`line' directives are left, you can remove them manually by deleting that entire line.

												  # The ultimate goal is to remove all ' `line ' directives.

```

---
<div align="center">
  <img width="1275" height="417" alt="sandpiper" src="https://github.com/user-attachments/assets/32a377c1-1ea5-4f63-b545-5c65730a5f5c" />
  <br/>
  <em>Conversion of .tlv file to .v file with Sandpiper</em>
</div>



---

<div align="center">
 <img width="1518" height="399" alt="line_directive_error" src="https://github.com/user-attachments/assets/8dfd02da-7f7b-46b7-a6a3-59b909ae1d88" />
  <br/>
  <em> `line directive error</em>
</div>

---

Then I used CHATGPT to create a Makefile and saved it in the 'module' folder and looked as shown below:
```Makefile
# Top-level sources
TLV     = rvmyth.tlv
VERILOG = rvmyth.v rvmyth_gen.v
TOP     = testbench.v

# SandPiper binary (adjust path if needed)
SANDPIPER = sandpiper

# Default target
all: sim

# Step 1: Generate Verilog from TLV
$(VERILOG): $(TLV)
	$(SANDPIPER) -i $(TLV) -o rvmyth.v
	@echo "Cleaning TLV debug directives..."
	sed -i '/^`line/d' rvmyth.v
	@if [ -f rvmyth_gen.v ]; then sed -i '/^`line/d' rvmyth_gen.v; fi

# Step 2: Compile with iverilog (SystemVerilog mode)
simv: $(VERILOG) $(TOP)
	iverilog -g2012 -o simv avsddac.v avsdpll.v clk_gate.v rvmyth.v vsdbabysoc.v testbench.v

# Step 3: Run simulation
sim: simv
	vvp simv

# Cleanup
clean:
	rm -f simv *.vcd $(VERILOG)

.PHONY: all sim clean

```
Then I continued with the following commands in the 'module' directory:

```bash
$ make
            # Here, I got a warning saying that 'The delays where mixed and I had to explicitly mention the delays with the help of '`timescale 1ns/ 1ps' line at the top of every verilog                   module. I did the changes in 'vsdbabysoc.v, rvmyth.v, avsddac.v, avsdpll.v, clk_gate.v'.
            # After implementing the changes, I ran the 'make' command again and got 'dump.vcd' file. I viewed the .vcd file.

			# If you continue to view the dump file generated with timescale warning, you won't get the actual waveforms. The warnings must resolved to view actual waveforms.

$ gtkwave dump.vcd
```


---

<div align="center">
 <img width="1308" height="226" alt="image" src="https://github.com/user-attachments/assets/803b1632-2945-4413-8436-1380219997d6" />
  <br/>
  <em> timescale warning during execution of 'make' command </em>
</div>

---


<div align="center">
 <img width="1854" height="1040" alt="waveform_with_warning" src="https://github.com/user-attachments/assets/a770f736-fcab-477b-aba3-0e83d5340b9c" />
  <br/>
  <em> Waveform with warning </em>
</div>

---

<div align="center">
 <img width="1854" height="1040" alt="dac" src="https://github.com/user-attachments/assets/793c2245-869c-4722-ba67-03c2fedf754d" />
  <br/>
  <em> Waveform without warning </em>
</div>

---



# Operation

## Dataflow between modules



<div align="center">
  <img width="1517" height="390" alt="waveforms" src="https://github.com/user-attachments/assets/4e3bcfab-74a4-449b-b89b-2e60d841ad8e" />
  <br/>
  <em>Figure: Waveforms demonstrating dataflow</em>
</div>

---

1.) The OUT signal(datatype - reg) under core gets its value from the 18th bit of *CPU_Xreg_value_a5* register.

2.) The OUT signal then drives input *D* of DAC module with the help of *RV_TO_DAC* signal under uut.
The output from the core is 'OUT' signal which is 10-bits wide. This output signal drives input of 'DAC' module via a top-level signal named 'RV_TO_DAC'. 

3.) The DAC then outputs a real valued signal *OUT*. Its value ranges between 0 & 1 since reference voltages used are 0V(lowest reference voltage) & 1V(highest reference voltage). The DAC module determines the output with help of certain formula as described below:

OUT = VREFL + (D/1023)*(VREFH - VREFL).

4.) The final OUT signal is produced as a digital output signal. The digital nature is induced beacuse of *wire* datatype used.

### Why the Same Signal Looks Different in the Waveform Viewer?

---

<div align="center">
  <img width="1086" height="150" alt="Screenshot from 2025-10-04 20-01-02" src="https://github.com/user-attachments/assets/f401ac67-a3e3-4a6c-bb52-fbb4b6b520db" />
  <br/>
  <em>Same signal but different shape of waveform observed</em>
</div>

---


### Explanation:

In the simulation, the OUT signal from the DAC module(i.e. avsddac.v) is connected to the top-level module (uut). Although it's physically the same net, the waveform viewer displays it differently in each scope because of how the signal is declared in each module.

```verilog
reg real OUT;
```
---
<div align="center">
  <img width="322" height="567" alt="image" src="https://github.com/user-attachments/assets/d903fa69-1d61-45c7-a2ee-f2fda828bed1" />
  <br/>
  <em>Datatype used - real</em>
</div>

---

Here, OUT is declared as a real type. Waveform viewers treat real values like analog signals and plot them as smooth or curved waveforms. Since OUT in this module holds floating-point values, the viewer renders it with analog-like curves.

The same OUT signal is connected to a port that is declared as a wire:
```verilog
output wire OUT;
```

---
<div align="center">
  <img width="322" height="567" alt="image" src="https://github.com/user-attachments/assets/4f77cc20-c397-415d-b74b-39c3f2e07a61" />
  <br/>
  <em>Datatype used - wire</em>
</div>

---

Since this port is interpreted as a logic signal, the waveform viewer displays it as a square wave, snapping to 0 or 1.

## Clocking
A PLL is used to boost frequency to 8 times the current frequency. But, how?

```verilog
initial begin
   lastedge = 0.0;
   period = 25.0; // 25 ns period = 40 MHz
   CLK <= 0;
end
This code block is used for initialization purpose.
```

So at time 0:

- Clock starts at 0

- Initial clock period = 25 ns → 40 MHz



```verilog
if (ENb_VCO == 1'b1) begin
   #(period / 2.0);
   CLK <= (CLK === 1'b0);
end
else if (ENb_VCO == 1'b0) begin
   CLK <= 1'b0;
end

```

So, the first rising edge occurs at 12.5ns because of *(period/2)* delay.

This controls whether PLL emits the clock. This is the actual enable for clock generation.

```verilog
always @(posedge REF) begin
   if (lastedge > 0.0) begin
      refpd = $realtime - lastedge;
      period = (refpd / 8.0);
   end
   lastedge = $realtime;
end

```
On each rising edge of REF, the module measures the time since the last rising edge and adjusts the output clock accordingly.


### Cycle-by-Cycle Explanation of PLL Period Update

We’re analyzing this always block:

```verilog
always @(posedge REF) begin
   if (lastedge > 0.0) begin
      refpd = $realtime - lastedge;
      period = (refpd / 8.0);
   end
   lastedge = $realtime;
end
```

This block updates the PLL output `period` based on the timing between rising edges of the `REF` clock.
Let’s assume `REF` has a 20 ns period (50 MHz). Its rising edges occur at:

```
t = 0 ns, 20 ns, 40 ns, 60 ns, 80 ns, ...
```

 **Cycle 1 — Rising Edge at t = 0 ns**
- `lastedge = 0.0` (initialized)
- Condition `lastedge > 0.0` is false
- No update to `period`
- `lastedge` becomes 0.0

**Cycle 2 — Rising Edge at t = 20 ns**
- `lastedge = 0.0`
- Condition still false
- `lastedge = 20.0`

**Cycle 3 — Rising Edge at t = 40 ns**
- `lastedge = 20.0` → condition true
- `refpd = 40.0 - 20.0 = 20.0 ns`
- `period = 20.0 / 8.0 = 2.5 ns`
- `lastedge = 40.0`

**Cycle 4 — Rising Edge at t = 60 ns**
- `refpd = 60.0 − 40.0 = 20 ns`
- `period = 20 / 8 = 2.5 ns`
- `lastedge = 60.0`

**Cycle 5 — Rising Edge at t = 80 ns**
- `refpd = 80.0 − 60.0 = 20 ns`
- `period = 20 / 8 = 2.5 ns`
- `lastedge = 80.0`

### The 'period' when divided by 2 gives us rising edge.

```verilog
always @(CLK or ENb_VCO) begin
   if (ENb_VCO == 1'b1) begin
      #(period / 2.0);
      CLK <= (CLK === 1'b0);
   end
   else if (ENb_VCO == 1'b0) begin
      CLK <= 1'b0;
   end
   else begin
      CLK <= 1'bx;
   end
end
```

- `period` is the full cycle time
- Dividing by 2 gives a 50% duty cycle
- With `period = 2.5 ns`, the delay is `1.25 ns` between two consectoggles

Example:
```
Time: 40ns, 41.25ns, 42.5ns, 43.75ns, 45ns...
CLK:   0      1        0        1       0   ...
```

The clock's full period remains 2.5 ns, matching the 400 MHz target.
