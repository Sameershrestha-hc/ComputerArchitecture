# 2-Bit Comparator using VHDL

## Overview

This project implements a **2-bit Digital Comparator** in VHDL. A comparator is a combinational logic circuit used to compare two binary numbers and determine whether one number is **equal to**, **greater than**, or **less than** the other.

The project consists of:

1. **Comparator Design (`COMPARATOR_2BIT`)**
2. **Testbench (`tb_and_gate`)** for simulation and verification.

---

# Objectives

* Design a 2-bit comparator using VHDL.
* Compare two 2-bit binary inputs.
* Generate outputs indicating:

  * Equality (`EQ`)
  * Greater Than (`GT`)
  * Less Than (`LT`)
* Verify the functionality using a testbench.


# THEORY
   A magnitude comparator compares two binary numbers and produces three output signals:
• EQ (Equal): HIGH when A = B
• GT (Greater Than): HIGH when A > B
• LT (Less Than): HIGH when A < B
For a 2-bit comparator with inputs A = A1A0 and B = B1B0:
EQ = A1 ⊕ B1 · A0 ⊕ B0
GT = A1B1 + A1 ⊕ B1 · A0B0
LT = A1B1 + A1 ⊕ B1 · A0B0

---

# Files Included

| File Name             | Description                                           |
| --------------------- | ----------------------------------------------------- |
| `COMPARATOR_2BIT.vhd` | Main VHDL code implementing the 2-bit comparator      |
| `tb_and_gate.vhd`     | Testbench used to verify the comparator functionality |

---

# Comparator Description

## Inputs

| Signal | Size   | Description          |
| ------ | ------ | -------------------- |
| A      | 2 bits | First binary number  |
| B      | 2 bits | Second binary number |

---

## Outputs

| Signal | Description           |
| ------ | --------------------- |
| EQ     | High ('1') when A = B |
| GT     | High ('1') when A > B |
| LT     | High ('1') when A < B |

---

# Working Principle

The comparator checks the two input values bit by bit.

### Equality (EQ)

The equality output becomes HIGH only when both bits of A are identical to the corresponding bits of B.

Logic Expression:

```
EQ = (A1 XNOR B1) AND (A0 XNOR B0)
```

---

### Greater Than (GT)

The output becomes HIGH when:

* The Most Significant Bit (MSB) of A is greater than the MSB of B.

OR

* MSBs are equal and the Least Significant Bit (LSB) of A is greater than the LSB of B.

Logic Expression:

```
GT = (A1 AND NOT B1)
   OR ((A1 XNOR B1) AND A0 AND NOT B0)
```

---

### Less Than (LT)

The output becomes HIGH when:

* The MSB of A is smaller than the MSB of B.

OR

* MSBs are equal and the LSB of A is smaller than the LSB of B.

Logic Expression:

```
LT = (NOT A1 AND B1)
   OR ((A1 XNOR B1) AND NOT A0 AND B0)
```

---

# Testbench Description

The testbench instantiates the comparator and applies several input combinations to verify all comparison conditions.

### Test Cases

| A  | B  | Expected EQ | Expected GT | Expected LT |
| -- | -- | ----------- | ----------- | ----------- |
| 00 | 00 | 1           | 0           | 0           |
| 01 | 00 | 0           | 1           | 0           |
| 00 | 01 | 0           | 0           | 1           |
| 10 | 11 | 0           | 0           | 1           |
| 11 | 10 | 0           | 1           | 0           |
| 11 | 11 | 1           | 0           | 0           |

Each test vector is applied for **10 ns** before moving to the next one.

---

# Simulation Procedure

1. Create a new VHDL project.
2. Add `COMPARATOR_2BIT.vhd`.
3. Add `tb_and_gate.vhd`.
4. Set the testbench as the top-level simulation file.
5. Compile both files.
6. Run the simulation.
7. Observe the waveform for inputs and outputs.

---

# Expected Results

The simulation should satisfy the following conditions:

* `EQ = 1` only when A and B are equal.
* `GT = 1` only when A is greater than B.
* `LT = 1` only when A is less than B.
* At any instant, only one of the outputs (`EQ`, `GT`, or `LT`) should be HIGH.

---

# Applications

* Arithmetic Logic Units (ALUs)
* Digital Processors
* Sorting Circuits
* Decision-Making Logic
* Address Comparison
* Digital Control Systems

---

# Conclusion

The project successfully demonstrates the implementation of a **2-bit comparator** using VHDL. The comparator correctly identifies whether input A is equal to, greater than, or less than input B. The accompanying testbench validates the design through multiple test cases, confirming the correctness of the implemented logic.

---

**Language:** VHDL

**Library Used:**

* IEEE.STD_LOGIC_1164.ALL
* IEEE.NUMERIC_STD.ALL

**Design Type:** Combinational Logic Circuit

**Simulation Time per Test Case:** 10 ns
