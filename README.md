# 🤖 Robotic M3 Screw-Driving Cell

### Engineering Concept & Feasibility Study

![Status](https://img.shields.io/badge/Status-Engineering%20Concept-blue)
![Robot](https://img.shields.io/badge/Robot-Techman%20TM5--900-orange)
![Vision](https://img.shields.io/badge/Vision-2D%20Camera-purple)
![Torque](https://img.shields.io/badge/Target%20Torque-2.0%20Nm-green)
![ROI](https://img.shields.io/badge/ROI-2.8%20Years-brightgreen)
![License](https://img.shields.io/badge/License-MIT-yellow)

> **Automated collaborative robotic cell for precision M3 screw driving on printed circuit boards (PCBs).**

---

## 📌 Project Overview

This repository contains the engineering concept, technical-economic feasibility study (TEO), control architecture and software concept for an automated robotic cell designed for high-precision M3 screw driving on printed circuit boards.

The system combines:

- 🤖 **Techman TM5-900 collaborative robot**
- 📷 **2D machine vision**
- 🔩 **DEPRAG MINIMAT-E electric screwdriver**
- 🪛 **SANCI CA-150 automatic screw feeder**
- 🧠 **Central robot controller**
- 📐 **Vision-based PCB position compensation**
- 📊 **Cycle monitoring and quality control**

The main objective is to reduce manual operator involvement while improving assembly consistency and screw-driving quality.

---

# 🎯 Project Goals

The robotic cell is designed to:

- automate M3 screw insertion;
- reduce manual operator involvement;
- maintain consistent screw-driving quality;
- detect PCB position deviations;
- reduce torque-related defects;
- improve production scalability;
- provide a documented and reproducible control architecture.

---

# 📊 Key Performance Indicators

| Metric | Manual Process | Automated Cell | Result |
|---|---:|---:|---|
| Cycle Time | 30.0 sec | 33.2 sec | Quality-focused cycle |
| Operator Engagement | 100% | 30% | Reduced involvement |
| Defect Rate | 3.0% | 0.5% | Improved quality |
| Cell / Operator | 1 : 1 | 2–3 : 1 | Higher scalability |
| Target Torque | — | 2.0 Nm | Controlled fastening |
| Estimated ROI | — | 2.8 years | CAPEX ≈ 2.57M ₽ |

> **Note:** The values above represent the engineering concept / feasibility-study assumptions and should be validated against real production data before implementation.

---

# 🏭 Cell Architecture

The proposed cell follows a shared workspace concept where the operator and robotic system perform separate tasks.

```mermaid
flowchart TB

    OP["👤 Operator"]

    subgraph VISION["📷 VISION SYSTEM"]
        CAM["2D Vision Camera"]
        POS["PCB Position Detection"]
    end

    subgraph CONTROL["🧠 CONTROL SYSTEM"]
        CTRL["Techman TM5-900 Controller"]
        FSM["Process State Machine"]
    end

    subgraph ROBOT["🤖 ROBOTIC SYSTEM"]
        ARM["Techman TM5-900"]
        SPINDLE["DEPRAG MINIMAT-E"]
        FEEDER["SANCI CA-150"]
    end

    subgraph WORKPIECE["🔧 WORKPIECE"]
        FIXTURE["PCB Fixture"]
        PCB["Printed Circuit Board"]
    end

    OP --> FIXTURE
    FIXTURE --> PCB

    CAM --> POS
    POS --> CTRL

    CTRL --> FSM
    FSM --> ARM
    FSM --> FEEDER

    ARM --> SPINDLE
    FEEDER --> SPINDLE

    SPINDLE --> PCB
    PCB --> CAM

    CTRL --> OP
