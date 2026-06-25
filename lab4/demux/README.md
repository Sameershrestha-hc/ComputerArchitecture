# VHDL 1-to-4 DEMUX

## Overview

This project implements a **1-to-4 Demultiplexer (DEMUX)** in VHDL along with a **testbench** for simulation and verification.

A DEMUX routes a single input signal (`D`) to one of four output lines (`Y(0)` to `Y(3)`) based on the value of the select lines (`S`).

---

## Files

### 1. `DEMUX_1TO4.vhd`

Contains the VHDL description of the 1-to-4 Demultiplexer.

### 2. `DEMUX_TB.vhd`

Contains the testbench used to simulate and verify the functionality of the DEMUX.

---

## DEMUX Specifications

### Inputs

| Signal | Type                         | Description  |
| ------ | ---------------------------- | ------------ |
| D      | std_logic                    | Data Input   |
| S      | std_logic_vector(1 downto 0) | Select Lines |

### Outputs

| Signal | Type                         | Description           |
| ------ | ---------------------------- | --------------------- |
| Y      | std_logic_vector(3 downto 0) | Demultiplexer Outputs |

---

## Truth Table

| S1 S0 | Output   |
| ----- | -------- |
| 00    | Y(0) = D |
| 01    | Y(1) = D |
| 10    | Y(2) = D |
| 11    | Y(3) = D |

When `D = 0`, all outputs remain `0`.

---

## Working Principle

The architecture uses a process block sensitive to `D` and `S`.

1. All outputs are initialized to `"0000"`.
2. The `case` statement checks the select input `S`.
3. Depending on the select value, the input `D` is assigned to the corresponding output bit.

Example:

* `S = "00"` → `Y(0) = D`
* `S = "01"` → `Y(1) = D`
* `S = "10"` → `Y(2) = D`
* `S = "11"` → `Y(3) = D`

---

## Testbench Description

The testbench performs the following operations:

| Time (ns) | D | S  | Expected Y |
| --------- | - | -- | ---------- |
| 0         | 1 | 00 | 0001       |
| 10        | 1 | 01 | 0010       |
| 20        | 1 | 10 | 0100       |
| 30        | 1 | 11 | 1000       |
| 40        | 0 | 10 | 0000       |

The testbench automatically applies these input combinations and allows observation of the output waveform during simulation.

---

## Compilation and Simulation (GHDL)

### Analyze the Files

```bash
ghdl -a DEMUX_1TO4.vhd
ghdl -a DEMUX_TB.vhd
```

### Elaborate the Testbench

```bash
ghdl -e DEMUX_TB
```

### Run Simulation and Generate VCD

```bash
ghdl -r DEMUX_TB --vcd=demux.vcd
```

### View Waveforms

Open the generated VCD file using a waveform viewer such as:

* GTKWave

Example:

```bash
gtkwave demux.vcd
```

---

## Expected Simulation Result

The output should change according to the select lines:

```text
S = 00  → Y = 0001
S = 01  → Y = 0010
S = 10  → Y = 0100
S = 11  → Y = 1000
D = 0   → Y = 0000
```

This confirms that the DEMUX correctly routes the input signal to the selected output line.

---

## Author

**Course:** Computer Architecture / Digital Logic Design
**Experiment:** Design and Simulation of a 1-to-4 Demultiplexer using VHDL
**Language:** VHDL
**Simulator:** GHDL
