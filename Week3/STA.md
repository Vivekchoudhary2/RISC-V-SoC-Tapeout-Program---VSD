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
