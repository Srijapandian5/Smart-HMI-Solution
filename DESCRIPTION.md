# Deterministic LVGL Industrial HMI with RTAL (Real-Time Abstraction Layer)

A high-performance, hardened Human-Machine Interface (HMI) built for the Raspberry Pi 5. This project bridges standard Linux scheduling and deterministic execution using LVGL, POSIX `SCHED_FIFO` real-time priorities, memory locking (`mlockall`), and CPU core pinning.

## Architecture & Features
* **Headless GUI Engine:** LVGL (`lvglsim`) optimized for Linux frame buffer environments.
* **Real-Time Abstraction Layer (RTAL):** A lightweight C wrapper (`rtal.c` / `rtal.h`) enforcing memory locking and core affinity at startup.
* **Hard Real-Time Scheduling:** Runs under `SCHED_FIFO` (Priority 50) pinned to an isolated CPU core (Core 3).
* **Systemd Integration:** Managed via a robust background service configuration with automatic restart policies.
* **Resilience & Telemetry:** Verified under heavy quad-core CPU saturation (`stress-ng`) and dynamic memory allocation pressure (`fallocate`).

## Project Structure
```text
├── rtal.h          # Real-Time Abstraction Layer header
├── rtal.c          # Real-Time implementation (mlockall, core pinning, SCHED_FIFO)
├── main.c          # Application entry point & LVGL loop initialization
├── rt_status.sh    # Live telemetry audit script for process/scheduling inspection
└── CMakeLists.txt  # Build configuration
