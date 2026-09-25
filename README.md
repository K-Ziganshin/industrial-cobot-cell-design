# 🤖 Robotic M3 Screw-Driving Cell (Engineering Concept & Feasibility Study)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Standards: ISO](https://img.shields.io/badge/Standards-ISO_10218--2_%7C_ISO%2FTS_15066-blue.svg)](#safety--standards)
[![Robot: Techman TM5-900](https://img.shields.io/badge/Robot-Techman_TM5--900-orange.svg)](https://www.tm-robot.com/)
[![ROI: 2.8 Years](https://img.shields.io/badge/ROI-2.8_Years-brightgreen.svg)](#economic-efficiency--roi)
[![Location: St. Petersburg](https://img.shields.io/badge/Developed_for-Semargl_(St._Petersburg)-0284c7.svg)](#project-overview)

---

## 📌 Project Overview

This repository contains the engineering concept, technical-economic feasibility study (TEO), and control architecture for an automated collaborative robotic cell designed for **Semargl (Saint Petersburg, Russia)**. 

The cell is engineered to automate high-precision M3 screw driving on printed circuit boards (PCBs) using a **Techman TM5-900** cobot integrated with 2D vision, a DEPRAG electric spindle, and a SANCI automatic screw feeder.

---

## 📊 Key Performance Indicators & ROI Impact

| Metric | Manual Process (Before) | Automated Cell (After) | Gain / Benefit |
| :--- | :---: | :---: | :---: |
| **Cycle Time (1 PCB / 4 Screws)** | 30.0 sec | 33.2 sec | Quality-focused cycle |
| **Operator Engagement per Cycle** | 100% (30 sec) | **30% (10 sec)** | **+70% Operator Free Time** 🚀 |
| **Defect Rate (Torque/Stripping)** | 3.0% | **0.5%** | **6x Quality Improvement** 🎯 |
| **Cell-to-Operator Ratio** | 1 cell / operator | **2–3 cells / operator** | **Labor Efficiency Scaling** |
| **Payback Period (ROI)** | — | — | **2.8 Years (CAPEX 2.57M ₽)** 💰 |

---

## 🏗️ Cell Layout & Components

The cell is designed following a **shared workspace layout** (5.5 m² total footprint), ensuring safe co-existence and task separation between the human operator and the cobot.

![Cell Layout and Control Architecture](assets/portfolio_slide1.svg)

### Hardware Specification:
* **Collaborative Robot:** `Techman TM5-900` (900 mm reach, 4 kg payload, ±0.05 mm repeatability, built-in 2D camera).
* **Electric Screw-Driving Spindle:** `DEPRAG MINIMAT-E` (2.0 Nm target torque, ±5% accuracy, DI/DO & AI/AO integration).
* **Screw Feeding System:** `SANCI CA-150` vibratory bowl feeder with optical screw-presence sensing.
* **Computer Vision (CV):** Integrated TM Vision camera for real-time PCB fixture position compensation ($\Delta X, \Delta Y, \Delta \theta$).

---

## ⚡ Control Architecture & I/O Interfaces

The **Techman TM5-900** cobot controller acts as the central cell controller managing execution logic and sensor feedback.

```mermaid
graph TD
    MES[Factory MES / Upper-Level System] <-->|Ethernet / TCP/IP| TM[Techman TM5-900 Controller]
    
    subgraph Cell Automation
        TM <-->|DI/DO: Start/Stop/Status| DEPRAG[DEPRAG Spindle]
        TM <-->|AI/AO: Torque Monitoring| DEPRAG
        TM <-->|DI/DO: Request/Screw Ready| SANCI[SANCI Feeder]
        TM <-->|TM Vision API| CAM[Built-in 2D Camera]
    end
    
    subgraph Safety Circuit
        E_STOP[E-Stop Buttons] -->|Safety I/O| TM
        BARRIER[Safety Doors / Barriers] -->|Safety I/O| TM
        LIGHT[3-Color Signal Tower] <--|DO| TM
    end
