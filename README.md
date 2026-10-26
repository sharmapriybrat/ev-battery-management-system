# EV Battery Management System (BMS) Simulator

A beginner-to-intermediate Embedded C project that simulates core functions of an Electric Vehicle Battery Management System (BMS). It monitors simulated battery measurements, estimates state of charge (SoC), detects unsafe conditions, and logs results to CSV.

> **Simulation only:** This project uses generated sample values. It is not suitable for controlling or protecting a real battery pack.

## Features

- Simulated battery voltage, current, and temperature measurements
- Simplified coulomb-counting SoC estimation
- Charging and discharging scenarios
- Protection checks for overvoltage, undervoltage, overcurrent, and overtemperature
- CSV data logging for analysis
- Clear separation between measurement simulation, SoC estimation, and safety checks

## Project structure

```text
ev-battery-management-system/
├── src/
│   └── main.c
├── data/
│   └── .gitkeep
├── .gitignore
├── Makefile
└── README.md
```

## Requirements

- GCC or another C compiler
- `make` (optional; you can compile directly)
- VS Code or any text editor (optional)

### Compile with GCC

From the project root:

```bash
gcc -std=c11 -Wall -Wextra -Wpedantic -O2 src/main.c -o bms_simulator
```

### Run

**Windows (PowerShell):**
```powershell
.\bms_simulator.exe
```

**Linux/macOS:**
```bash
./bms_simulator
```

The program writes `bms_log.csv` in the directory where it is run.

### Compile using Make

```bash
make
make run
```

## Example output

```text
EV Battery Management System Simulator
---------------------------------------
Time  Voltage(V) Current(A) Temp(C) SoC(%) Status
   0       355.0      12.0     27.0   70.0 NORMAL
   1       354.8      12.0     27.1   70.0 NORMAL
...
```

The exact output depends on the simulated scenario.

## How it works

1. The simulator starts with a nominal pack voltage, current, temperature, and SoC.
2. Each time step updates the measurements using a simple deterministic scenario.
3. Coulomb counting estimates SoC from current and elapsed time:
   `SoC change (%) = current (A) × time (h) / capacity (Ah) × 100`
4. The protection logic compares the simulated readings with configurable thresholds.
5. Every sample is printed to the terminal and appended to `bms_log.csv`.

In this example, positive current means discharge and negative current means charging.

## Default demonstration thresholds

These values are illustrative software-demo settings, not cell-manufacturer limits:

- Undervoltage: pack voltage below 300 V
- Overvoltage: pack voltage above 420 V
- Overcurrent: absolute current above 100 A
- Overtemperature: temperature above 60 °C

Real BMS limits must be derived from the exact cell chemistry, series/parallel configuration, sensor accuracy, thermal design, and manufacturer specifications.

## Suggested extensions

- Add command-line options for battery capacity and initial SoC
- Read measurements from a CSV input file rather than a built-in scenario
- Add unit tests for SoC and protection logic
- Create a Python script to plot voltage, temperature, and SoC
- Port the measurement and protection modules to an STM32 or Arduino platform
- Add CAN message encoding/decoding for simulated BMS telemetry

## Skills demonstrated

- Embedded C fundamentals
- Structs, functions, file I/O, and control logic
- Battery SoC estimation concepts
- Fault detection and threshold-based protection
- Data logging and reproducible simulation
- Git/GitHub project documentation

## Resume bullet (use only after you have run and understood the code)

**EV Battery Management System Simulator | Embedded C**
- Developed a C-based BMS simulation to track battery voltage, current, temperature, and state of charge.
- Implemented coulomb-counting SoC estimation, threshold-based fault detection, and CSV telemetry logging.
- Tested simulated charging/discharging conditions and documented protection thresholds and limitations.

## License

This project is provided for learning and portfolio demonstration. You may add an MIT license if you want to publish it as an open-source project.
