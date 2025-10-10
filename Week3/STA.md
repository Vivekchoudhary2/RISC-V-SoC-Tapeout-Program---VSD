# Static timing analysis

## What is Static timing analysis?
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations.

### Setup time & Hold time
The ultimate idea behind a *setup time* & *hold time* is that the data signals should remain stable during a clock edge to avoid misinterpretation of data.
- Setup time - The minimum amount of time that the data signal must be stable before active clock edge arrives.
- Hold time - The minimum amount of time that the data signal must remain stable after clock edge has passed.

The failure to meet any one of these constraints leads to timing violation.

The two most fundamental types of timing violations are **Setup time violations** and **Hold time violations**.

---

<div align="center">
 <img width="1054" height="724" alt="image" src="https://github.com/user-attachments/assets/86f10697-30ce-4cd6-aa8b-000c89064f56" />
  </br>
  <br/>
  <em> Transition in data signals after the active clock edge leading to hold time violation </em>
</div>

---

<div align="center">
 <img width="1023" height="708" alt="image" src="https://github.com/user-attachments/assets/eae5d990-3a48-4a03-a40c-95d706360052" />
  </br>
  <br/>
  <em> Transition in data signals prior to active clock edge leading to setup time violation </em>
</div>

---

Ultimately, performing STA means analysing the performance of a circuit by checking all possible paths which can cause timing violations(setup or hold time violation).

**Note -  STA can only check the timing, not the functionality, of a circuit design.**

## Timing path

Now, since we understand what timing violations mean it is essential to understand how STA works. STA identifies every possible route a signal can take through a digital circuit. That route is called *timing path*.

That path has 3 key components:
- Startpoint - This is where the data signal originates. It's typically the clock pin of a sequential element like a flip-flop or an input port of the chip.
- Combinational logic - This is the series of logic gates (like AND, OR, NOT gates) that the signal travels through. 
- Endpoint - This is the final destination of the data signal. It's usually the data input pin of a sequential element or an output port of the chip.

---



<div align="center">
 <img width="927" height="409" alt="image" src="https://github.com/user-attachments/assets/b2745682-98b9-43e6-9e80-058d232b19a1" />
  </br>
  <br/>
  <em> Timing path </em>
</div>

---


<div align="center">
 <img width="927" height="464" alt="image" src="https://github.com/user-attachments/assets/39daa126-7a08-484a-94ef-dea1f5844995" />
  </br>
  <br/>
  <em> Cloud shape substitutes combinational logic with paths having varying delay </em>
</div>

---

To perform timing analysis, the complete circuit is divided into different timing paths (that timing path may include path between *Input to register*, *Register to register* or *Register to output*) followed by calculation of delay across every specific path and finally determining the slowest and the fastest path in the circuit.

## Arrival time

This is the time by which the signal is expected to arrive at a certain point in a design.

## Required time

This is the time by which a signal must arrive at the destination to be correctly captured.

## Slack

Slack is the difference between the *'Required time'* and the  *'Arrival time'*.
They are of two types:
- Setup slack
- Hold slack


## 🧮 Example: Setup and Hold Slack Calculation

Let’s work through an example to solidify the concept.

### Circuit Parameters

| Parameter | Symbol | Value |
|------------|---------|--------|
| Clock Period | – | **1000 ps** |
| Clock-to-Q Delay (FF1) | T<sub>c-q</sub> | **50 ps** |
| Setup Time (FF2) | T<sub>setup</sub> | **70 ps** |
| Hold Time (FF2) | T<sub>hold</sub> | **60 ps** |

---

### 🔹 Part 1: Setup Slack (Longest Path)

Assume the **slowest** logic path has a delay of **800 ps**.

#### Step 1: Calculate Arrival Time (AT)
```
AT = T_c-q + Logic Path Delay
AT = 50 ps + 800 ps = 850 ps
```

#### Step 2: Calculate Required Time (RT)
```
RT = Next Clock Edge - T_setup
RT = 1000 ps - 70 ps = 930 ps
```

#### Step 3: Calculate Setup Slack
```
Setup Slack = RT - AT
Setup Slack = 930 ps - 850 ps = +80 ps
```

✅ **Result:** Positive slack → setup requirement met with **80 ps margin.**

---

### 🔹 Part 2: Hold Slack (Shortest Path)

Assume the **fastest** logic path has a delay of **40 ps**.

#### Step 1: Calculate Arrival Time (AT)
```
AT = T_c-q + Logic Path Delay
AT = 50 ps + 40 ps = 90 ps
```

#### Step 2: Calculate Required Time (RT)
```
RT = Launch Clock Edge + T_hold
RT = 0 ps + 60 ps = 60 ps
```

#### Step 3: Calculate Hold Slack
```
Hold Slack = AT - RT
Hold Slack = 90 ps - 60 ps = +30 ps
```

✅ **Result:** Positive slack → hold requirement met with **30 ps margin.**

---

## ✅ Summary

| Concept | Formula | Description |
|----------|----------|-------------|
| **Setup Slack** | RT - AT | Checks if data arrives **before** next clock edge |
| **Hold Slack** | AT - RT | Checks if data arrives **after** hold window closes |
| **Positive Slack** | – | Timing met |
| **Negative Slack** | – | Timing violation |

---

> 🧠 **Key Insight:**  
> STA is a purely **timing-based verification** process — it checks **when** signals arrive, not **what** values they carry.  
> Hence, STA ensures **timing integrity**, while functional simulations ensure **logical correctness**.

---
