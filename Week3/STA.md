# Static timing analysis

## What is Static timing analysis?
Static timing analysis (STA) is a method of validating the timing performance of a design by checking all possible paths for timing violations.

**Note -  STA can only check the timing, not the functionality, of a circuit design.**

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

## Timing path
