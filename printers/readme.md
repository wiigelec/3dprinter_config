# 📄 Project README.md: The Klipper Fleet

## Project Title: Distributed Klipper Fleet

**Overview:** This document details the hardware, specialized roles, and management stack for a high-performance, 6-machine Klipper-native 3D printer fleet. The architecture utilizes decentralized SBCs (Manta/CB1) for maximum performance, controlled by a single open-source management host. The focus is on **high-speed throughput** and **advanced material handling** (PC, Nylon-CF, MMU).

---

## 1. ⚙️ Fleet Architecture & Management Stack

The fleet operates on a **Distributed Klipper Architecture** with zero recurring cost, ensuring redundancy and speed by isolating video processing and motion control.

### 1.1. Core Architecture

| Component | Hardware | Function |
| :--- | :--- | :--- |
| **Central Host** | Mini-PC (Linux Server) | Runs all centralized software (Mainsail, Obico, Timelapse, Queue). |
| **Printer Hosts** | BTT Manta M4P/M5P/M8P + **CB1/CM4** | Runs individual Klipper/Moonraker instances (high resilience). |
| **Communication** | LAN/Ethernet | All printer SBCs connect to the network; the Mini-PC controls them via their Moonraker API. |
| **Camera System** | Centralized Crowsnest | All 6 webcams are plugged into the Mini-PC, offloading CPU-intensive video encoding from the printer SBCs. |

### 1.2. Central Management Stack (Mini-PC)

| Software | Status | Primary Function |
| :--- | :--- | :--- |
| **Mainsail / Fluidd** | Open-Source | **Unified Control Interface.** Provides a single dashboard view of all 6 printers with dedicated control tabs. |
| **Obico Server** | Self-Hosted | **AI Failure Detection.** Monitors the Voron 2.4 camera stream for spaghetti/warping, automatically pausing the print. |
| **Moonraker Timelapse** | Open-Source | **Content Generation.** Centralized processing of webcam streams for YouTube-ready timelapse videos. |
| **Klipper-Backup** | Open-Source | **Configuration Safety.** Automatically backs up and version-controls all 6 printer configs and shared macros to a private Git repository. |
| **Ansible / rsync** | Linux Utility | **Deployment Tool.** Used to push standardized configuration files and updates from the Mini-PC to the 6 individual printer SBCs. |

---

## 2. 💎 Fleet Printer Details (6 Machines)

The fleet is categorized by role, from hybrid multi-material production to low-maintenance general use.

### 2.1. Hybrid Multi-Material & Engineering

| Printer | Voron 2.4 (300mm) | Voron Switchwire |
| :--- | :--- | :--- |
| **Core Role** | Flagship Hybrid Production (High-Temp) | High-Speed MMU Center (PLA/PETG) |
| **Control Board**| Manta M8P + CM4 | Manta M4P + CB1 |
| **Toolhead** | Custom Dual-Dock StealthChanger | **Jabberwocky Toolhead** (w/ NH36) |
| **MMU System** | **ERCF** (External MMU) | **Box Turtle MMU** (A1 Clone) |
| **Key Hardware**| HF/UHF (Rapido/Dragon), SiC Nozzles | Nitehawk 36 Toolhead MCU. |
| **Function** | Prints large **Nylon-CF/PC** parts on Tool 1, or complex multi-color/support jobs via **ERCF** on Tool 2. | Dedicated to high-volume, multi-color **PLA/PETG** production. Jabberwocky is engineered for high-reliability filament changes. |

### 2.2. Dedicated Workhorses & Specialties

| Printer | RepRap2025 (Custom i3) | Tiny-T (150mm) | Tri-0 (120mm) | Ender 3 V1 |
| :--- | :--- | :--- | :--- | :--- |
| **Core Role** | Rigid General Purpose | Small-Batch ABS/ASA | Micro-Production Reliability | Legacy/Test Bench |
| **Control Board**| Manta M4P + CB1 | Standard Voron SBC | Standard Voron SBC | BTT SKR Mini E3 + SBC |
| **Key Hardware**| **Vesconite Bushings, Beacon Probe** | Enclosed, High-Speed CoreXY | **Triple-Belted Z** | Klipper Conversion Complete |
| **Function** | Low-maintenance, high-speed **PLA/PETG** production. The **Beacon Probe** ensures sub-micron Z-accuracy. | Fast turnover of small, enclosed, high-temp parts in **ABS/ASA**. | Ultra-reliable Z-axis (via Klipper Z-tilt) for the most critical small components. | Used for filament calibration and experimental testing; Klipperized for stack uniformity. |

---

## 3. 🛠️ Critical Klipper Configuration & Maintenance Notes

### 3.1. Toolhead Standardization

* **Extruders:** Standardized on **Mini Sherpa / G2SA** for lightweight, high-force direct drive across all Vorons/Switchwire/RepRap2025.
* **Nozzles:** Stock of **Dragon/Rapido HF/UHF** and **SiC** nozzles available to match job flow rate and material abrasion requirements.

### 3.2. Safety and Deployment

* **Configuration Safety:** All configurations are protected by the **Klipper-Backup** tool, which automatically commits and pushes changes to a private Git repository.
* **Deployment:** The **Ansible / rsync** workflow is used to push standardized shared macros (e.g., `START_PRINT`, `TIMELAPSE_TAKE_FRAME`) from the Mini-PC to the local filesystem of all 6 SBCs, maintaining fleet consistency.
