# eYANTRA 2025 — Maze Solver Bot (MB) Theme Tasks

This repository contains implementations of the eYRC 2025 Maze Solver Bot (MB) theme tasks. All tasks are implemented in Verilog HDL and prepared for synthesis with Quartus Prime and RTL simulation with ModelSim. The projects are organized per task and include Verilog sources, testbenches, Quartus project files, and simulation resources.

Status: Simulation-focused, tested locally. Hardware deployment (FPGA) optional.

---

## Team Members

- Ridhi Shakkar
- Naman V Shetty
- Sreehari J
- Nainsi Kushwaha

---

## Table of Contents

- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Repository Structure](#repository-structure)
- [Tasks Overview](#tasks-overview)
  - [Task 1A — Frequency Scaling & PWM Generator](#task-1a---frequency-scaling--pwm-generator)
  - [Task 1B — Ultrasonic Distance Measurement](#task-1b---ultrasonic-distance-measurement)
  - [Task 1C — RISC-V CPU (RV32I) Implementation](#task-1c---risc-v-cpu-rv32i-implementation)
  - [Task 2A — DHT11 Temperature & Humidity](#task-2a---dht11-temperature--humidity)
  - [Task 2B — UART Transmitter & Receiver](#task-2b---uart-transmitter--receiver)
  - [Task 2C — Maze-Solving Robot](#task-2c---maze-solving-robot)
- [Contributing](#contributing)
- [License](#license)

---

## Overview

These projects demonstrate digital design and embedded systems concepts using Verilog, with focus on FSM design, sensor interfacing, simple CPU design, and UART/communication protocols. Each task is designed to be modular and simulation-friendly.

---

## Prerequisites

- Quartus Prime (compatible version; Lite is fine).
- ModelSim (for RTL simulation; recommended integration via NativeLink).
- Python 3 and pip (for optional evaluation utilities).
- Optional hardware: FPGA development board (if you plan to program and test on hardware).

Optional (for Task 2B automated evaluation):
```
pip install eyantra-autoeval
```

---

## Repository Structure

Root layout:
- task1a_fs_pwm/          — Quartus project for Task 1A
- task1b_ultrasonic/      — Quartus project for Task 1B
- task1c_riscv_cpu/       — Quartus project for Task 1C
- task2a_dht/             — Quartus project for Task 2A
- task2b_uart/            — Quartus project for Task 2C
  - uart_tx/              — UART transmitter project
  - uart_rx/              — UART receiver project
- task2c_maze_solver/     — Quartus project for Task 2C
- docs/                   — diagrams, waveforms, or supporting documents
- README.md               — this file

Each task directory typically contains:
- .qpf and .qsf Quartus project files
- Verilog source files (e.g., *.v)
- Block diagram files (.bdf) when used
- Testbenches (tb_*.v)
- Simulation waveforms/logs

---

## Tasks Overview

### Task 1A — Frequency Scaling & PWM Generator
- Objective: Scale a 50 MHz clock to 3.125 MHz and 195 kHz; implement a PWM generator supporting a 4-bit duty cycle.
- Key files: `frequency_scaling.v`, `pwm_generator.v`
- Notes: PWM output at 195 kHz; duty cycle via 4-bit input.

### Task 1B — Ultrasonic Distance Measurement
- Objective: Interface with HC-SR04 to measure distance in mm and detect obstacles.
- Key files: `t1b_ultrasonic.v`
- Notes: FSM implements 10 µs trigger, measures echo pulse, outputs 8-bit distance and obstacle flag for <70 mm.

### Task 1C — RISC-V CPU (RV32I) Implementation
- Objective: Single-cycle RISC-V CPU supporting RV32I base ISA.
- Key files: `riscv_cpu.v` and modular submodules (ALU, register file, control, memory).
- Notes: Designed for simulation and easy modular testing; testbench provided.

### Task 2A — DHT11 Temperature & Humidity
- Objective: Read temperature and humidity bytes from DHT11 using its timing protocol.
- Key files: `t2a_dht.v`
- Notes: FSM decodes the 40-bit frame, validates checksum, outputs RH/T and data_valid.

### Task 2B — UART Transmitter & Receiver
- Objective: UART TX/RX at 115200 baud, 8 data bits, 1 parity bit (configurable), 1 stop bit.
- Key files: `uart_tx/uart_tx.v`, `uart_rx/uart_rx.v`
- Notes:
  - TX: FSM for start, data, parity, stop bits; supports sending custom strings.
  - RX: Bit-sampling FSM, parity check; replaces errored characters with '?'.
  - Use `eyantra-autoeval` for automated input generation in WSL if needed.

### Task 2C — Maze-Solving Robot
- Objective: Navigate a 9x9 wall-based maze using three ultrasonic sensors (left, front, right).
- Key files: top-level maze module and `tb.v`
- Notes: Implements exploration FSM (left-hand or mixed strategy), outputs movement commands (STOP, FORWARD, LEFT, RIGHT, U-TURN). Debug mode prints position logs in testbench.

---

## Contributing

This is primarily a group repository- **Ridhi Shakkar**, **Sreehari**, **Naman V Shetty** and **Nainsi Kushwaha** for the eYRC tasks. If you'd like to suggest improvements or report issues:
- Open an issue describing the change or bug.
- For code contributions, create a branch and send a pull request with clear description and testbench evidence.


---

## License

This project is intended to be licensed under the MIT License. If a LICENSE file is missing, add one with the standard MIT text. Example notice:
```
MIT License
Copyright (c) 2025 Your Name
Permission is hereby granted...
```

