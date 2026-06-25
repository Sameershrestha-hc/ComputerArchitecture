# VHDL 4-to-1 Multiplexer (MUX)

## Overview

This project implements a **4-to-1 Multiplexer (MUX)** in VHDL along with a **testbench** for simulation and verification.

A Multiplexer selects one of several input signals and forwards the selected input to a single output line based on the values of the select lines.

---

## Files

### 1. `MUX_4TO1.vhd`

Contains the VHDL description of the 4-to-1 Multiplexer.

### 2. `MUX_TB.vhd`

Contains the testbench used to simulate and verify the functionality of the MUX.

---

## MUX Specifications

### Inputs

| Signal | Type                         | Description      |
| ------ | ---------------------------- | ---------------- |
| D      | std_logic_vector(3 downto 0) | Four Data Inputs |
| S      | std_logic_vector(1 downto 0) | Select Lines     |

### Output

| Signal | Type      | Description        |
| ------ | --------- | ------------------ |
| Y      | std_logic | Multiplexer Output |

---

## Truth Table

| S1 S0 | Selected Input | Output Y |
| ----- | -------------- | -------- |
| 00    | D(0)           | D(0)     |
| 01    | D(1)           | D(1)     |
| 10    | D(2)           | D(2)     |
| 11    | D(3)           | D(3)     |

---

## Working Principle

The design uses a `case` statement inside a process block sensitive to `D` and `S`.

The select lines determine which data input is connected to the output.

* `S = "00"` → `Y = D(0)`
* `S = "01"` → `Y = D(1)`
* `S = "10"` → `Y = D(2)`
* `S = "11"` → `Y = D(3)`

If an invalid select value occurs, the output is assigned `'0'`.

---

## Testbench Description

The testbench initializes:

```text
D = "1010"
```

This means:

| Input | Value |
| ----- | ----- |
| D(3)  | 1     |
| D(2)  | 0     |
| D(1)  | 1     |
| D(0)  | 0     |

The select lines are then changed every 10 ns to verify that the correct input appears at the output.

### Test Cases

| Time (ns) | S  | Selected Input | Expected Y |
| --------- | -- | -------------- | ---------- |
| 0         | 00 | D(0)           | 0          |
| 10        | 01 | D(1)           | 1          |
| 20        | 10 | D(2)           | 0          |
| 30        | 11 | D(3)           | 1          |

---

## Compilation and Simulation (GHDL)

### Analyze the Files

```bash
ghdl -a MUX_4TO1.vhd
ghdl -a MUX_TB.vhd
```

### Elaborate the Testbench

```bash
ghdl -e MUX_TB
```

### Run Simulation and Generate VCD File

```bash
ghdl -r MUX_TB --vcd=mux.vcd
```

### View Waveforms

Open the generated waveform file using:

* GTKWave

```bash
gtkwave mux.vcd
```

---

## Expected Simulation Result

For `D = "1010"`:

```text
S = 00  → Y = 0
S = 01  → Y = 1
S = 10  → Y = 0
S = 11  → Y = 1
```

The waveform should show the output changing according to the selected input, confirming correct Multiplexer operation.

---

## Conclusion

The 4-to-1 Multiplexer was successfully designed and simulated using VHDL. The testbench verified that the output correctly follows the input selected by the control lines. The simulation results matched the expected behavior of a standard 4-to-1 MUX.

---

## Author

**Course:** Computer Architecture / Digital Logic Design
**Experiment:** Design and Simulation of a 4-to-1 Multiplexer using VHDL
**Language:** VHDL
**Simulator:** GHDL and GTKWave
