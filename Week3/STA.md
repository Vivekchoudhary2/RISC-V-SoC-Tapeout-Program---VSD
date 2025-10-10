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

Slack is the difference between the *'Required time'* and the *'Arrival time'*.
They are of two types:
- Setup slack
- Hold slack

<details>
<summary><h2>🧮 Example: Setup and Hold Slack Calculation</h2></summary>

Let’s work through an example to solidify the concept.

### Circuit and timing parameters

| Parameter | Symbol | Value |
|------------|---------|--------|
| Clock Period | – | **1000 ps** |
| Clock-to-Q Delay (FF1) | T<sub>c-q</sub> | **50 ps** |
| Setup Time (FF2) | T<sub>setup</sub> | **70 ps** |
| Hold Time (FF2) | T<sub>hold</sub> | **60 ps** |
| Logic path delay(longest) | - | **800ps** |
| Logic path delay(shortest) | - | **40ps** |

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
RT = 1000 ps - 70 ps = 930 ps        // The data is required to be at FF2 no later than 930 ps.
```

#### Step 3: Calculate Setup Slack
```
Setup Slack = RT - AT
Setup Slack = 930 ps - 850 ps = +80 ps
```

✅ **Result:** The signal arrived 80 ps earlier than it needed to.

---

### 🔹 Part 2: Hold Slack (Shortest Path)


#### Step 1: Calculate Arrival Time (AT)
```
AT = T_c-q + Logic Path Delay(shortest)
AT = 50 ps + 40 ps = 90 ps
```

#### Step 2: Calculate Required Time (RT)
```
RT = Launch Clock Edge + T_hold
RT = 0 ps + 60 ps = 60 ps           // The old data must not be changed before 60 ps.
```

#### Step 3: Calculate Hold Slack
```
Hold Slack = AT - RT
Hold Slack = 90 ps - 60 ps = +30 ps
```

✅ **Result:** The new data arrived 30 ps after the hold window for the old data closed, which is safe.

---

</details>


### Setup check
The setup check ensures that the data is available at the input of the FF2 before the active edge of the clock. Because at the next clock edge the FF2 will capture whatever is at it's input and produce output. Therefore, before the arrival of clock we must know for sure that the next data is ready at the input of FF2.

Also,
 - The data should be stable for a certain amount of time, namely the setup time of the flip-flop, before the active edge of the clock arrives at the flip-flops, so that the data is captured reliably into the flip-flop.
 - The setup check ensures that the data launched from the previous clock cycle is ready to be captured after one cycle.


<details>
<summary><h4> Example of setup check </h4></summary>

Let's analyze a simple circuit where a signal is launched from flip-flop FF1 and captured by flip-flop FF2.

---

<div align="center">
 <img width="773" height="346" alt="image" src="https://github.com/user-attachments/assets/8f929d9b-a2dd-484d-af24-2e7a7a033539" />
  </br>
  <br/>
  <em> Demonstrating setup check with two back to back flip-flops </em>
</div>

---

Timing Parameters:

- Clock Period: 10 nanoseconds (ns). The first clock edge is at 0 ns, and the next is at 10 ns.

- Clock-to-Q Delay (T_c-q) of FF1: 1 ns. The time it takes for data to appear at FF1's output after a clock edge.

- Combinational Logic Delay: 7 ns. The delay through the logic gates between the two flip-flops. This is our longest path.

- Setup Time (T_setup) of FF2: 2 ns. FF2 requires the data to be stable at its input for at least 2 ns before the 10 ns clock edge.

---

#### Step 1: Calculate the Data Arrival Time (AT) ⏱️
This is the actual time it takes for the data to travel from FF1 to FF2 after the 0 ns clock edge.
```
Data Arrival Time = T_c-q + Combinational Logic Delay
AT = 1 ns + 7 ns = 8 ns
```
So, the data arrives at FF2's input at 8 ns.

---

#### Step 2: Calculate the Data Required Time (RT) 📅
This is the deadline the data must meet. It must be stable at FF2's input one setup time before the next clock edge.

```
Data Required Time = Next Clock Edge - T_setup
RT = 10 ns - 2 ns = 8 ns
```
The data is required to arrive no later than 8 ns.

---

#### Step 3: Compare
Now we compare the arrival time to the required time.

Since both are equal, the signal arrives exactly when it is needed. The **setup check passes**, but with zero slack.

If the logic delay had been 7.1 ns, the arrival time would have been 8.1 ns, which is later than the required time of 8 ns. This would result in a setup violation.

The new data signal arrived 0.1 ns too late, missing its deadline before the clock edge. This means FF2 was not guaranteed to capture the new, correct value and might have captured the old data or an unstable signal. To fix this, an engineer would need to optimize the logic path to reduce its delay. This is often done by swapping in faster logic cells, re-arranging the logic, or improving the physical layout.

</details>

---

### Hold check
A hold check ensures that the data signal at the input remains stable for a minimum required time **after the clock edge has passed**.

The data should be stable for a certain amount of time, namely the hold time of FF, after the active edge of clock so that the data is captured reliably.

The data which has already been captured by FF2 must be stable at the input for atleast the hold time of the FF immediately after the current clock edge has passed.


<details>
<summary><h4> Example of hold check </h4></summary>

Let's use the same circuit as before, but this time we will analyze the shortest (fastest) possible path for the signal.

---

<div align="center">
 <img width="773" height="346" alt="image" src="https://github.com/user-attachments/assets/8f929d9b-a2dd-484d-af24-2e7a7a033539" />
  </br>
  <br/>
  <em> Demonstrating hold check with two back to back flip-flops </em>
</div>

---

Timing Parameters:

- Clock Period: 10 nanoseconds (ns). The analysis happens relative to a single clock edge (let's say at 0 ns).

- Clock-to-Q Delay (T_c-q) of FF1: 1 ns.

- Combinational Logic Delay: 0.5 ns.  This is a very fast path, which is where hold violations are most likely to occur.

- Setup Time (T_setup) of FF2: 2 ns. FF2 requires its input data to remain stable for at least 2 ns after the clock edge.

---

#### Step 1: Calculate the Data Arrival Time (AT) ⏱️
This is the actual time it takes for the data to travel from FF1 to FF2 after the 0 ns clock edge.
```
Data Arrival Time = T_c-q + Combinational Logic Delay
AT = 1 ns + 0.5 ns = 1.5 ns
```
The new data arrives at FF2's input at 1.5 ns.

---

#### Step 2: Calculate the Data Required Time (RT) 📅
This is the time window during which the old data must remain stable. It must be held steady for one hold time after the launching clock edge.

```
Data Required Time = Launch Clock Edge - T_hold
RT = 0 ns + 2 ns = 2 ns
```
The old data must not change before 2 ns.

---

#### Step 3: Compare
Now, we compare when the new data arrives versus how long the old data needed to be held.
- Arrival Time (New Data): 1.5 ns
- Required Time (Old Data Stable Until): 2 ns

The new data arrives at 1.5 ns, but the old data was required to stay stable until 2 ns. The arrival time is less than the required time.


This is a **hold violation**. The new data signal arrived 0.5 ns too early, overwriting the previous value before FF2 had enough time to reliably capture it. To fix this, an engineer would need to add delay (usually by inserting buffers) into the logic path to slow the signal down.

</details>

---
