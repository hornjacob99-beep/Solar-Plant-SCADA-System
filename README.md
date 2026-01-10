# Solar Plant SCADA System (CODESYS)

For Chapter 8 validation slide deck see file named "Chapter_8_Validation_Slide_Deck".
This project is a simulated utility-scale **solar power plant SCADA and Power Plant Controller (PPC)** implemented in **CODESYS**.  
It models dispatch-following behavior for a hybrid plant consisting of **Solar PV, Battery Energy Storage (BESS), and Flywheel Energy Storage (FESS)**, including ramp-rate enforcement, asset prioritization, charging logic, and operator-facing SCADA signals.

The project is intended as a **controls / power systems portfolio project** demonstrating realistic plant-level logic and HMI-ready data structures.

---

## Key Features

- Plant-level **dispatch tracking with ramp limiting** (10 MW/min at POI)
- Day/Night operating modes with solar availability logic
- Priority-based power allocation:
  - Solar → Battery → Flywheel for discharge
  - Flywheel → Battery → Curtailment for charging
- Energy-constrained storage models (SOC / MWh)
- No simultaneous charge and discharge per asset
- Realistic **plant saturation and tracking logic**
- SCADA-ready **status bits and alarm flags**
- Operator-adjustable dispatch and day/night toggle

---

## Plant Configuration

| Asset | Power | Energy |
|------|------|--------|
| Solar PV | 100 MW | N/A |
| Battery (BESS) | ±50 MW | 200 MWh (10–90% SOC window) |
| Flywheel (FESS) | ±10 MW | 2 MWh |

- Dispatch command range: **0–160 MW**
- Night operation: **storage only (no charging)**
- Ramp limit enforced at POI: **10 MW/min**

---

## Project Structure (CODESYS)

- **PlantControl**
  - `PRG_PPC` – Power Plant Controller (main logic)
  - `FB_PowerAllocator` – Dispatch allocation & charging logic
  - `FB_RampLimiter` – Plant-level ramp enforcement
- **Simulation**
  - `SIM_DispatchSource` – Operator / simulated dispatch input
  - `SIM_SolarModel` – Solar availability & curtailment
  - `SIM_BatteryModel` – Battery SOC & power limits
  - `SIM_FlywheelModel` – Flywheel energy model
  - `SIM_POI_Measurement` – POI power aggregation
- **Types**
  - `GVL_Constants` – Plant constants & timing
  - `GVL_Dispatch` – Operator dispatch input
  - `GVL_PlantState` – Central SCADA/state database
- **Visualization**
  - `VISU_Main` – SCADA/HMI display

---

## Opening the Project

The repository contains the CODESYS project file:
## Solar Plant SCADA take2.project

To run the project:

1. Open **CODESYS**
2. Select **File → Open Project**
3. Open `Solar Plant SCADA take2.project`
4. Login and run the application

All logic, task configuration, and visualizations are contained within this file.

> **Note:** A screenshot in the repository shows the local file path layout used during development.  
> This is provided for reference only—CODESYS will load the project correctly regardless of local directory structure.
<img width="299" height="588" alt="image" src="https://github.com/user-attachments/assets/81e409bd-ec55-4c0b-9738-59dad09cb425" />

---

## How to Operate (SCADA)

Operator-adjustable inputs:
- `GVL_Dispatch.Dispatch_Command_MW` – Dispatch setpoint (MW)
- `GVL_PlantState.IsDay` – Day / Night toggle

Key SCADA indicators:
- Dispatch Requested vs Delivered (POI)
- Plant Available MW
- Solar: Available / Used / Curtailed
- Battery: SOC, MW, Mode
- Flywheel: Energy, MW, Mode
- Alarm banner:
  - Dispatch Not Tracked
  - Plant Saturated
  - Battery Low SOC
  - Flywheel Empty
  - Solar Curtailed

---

## Purpose

This project was built to demonstrate:
- Realistic **power plant control architecture**
- Clear separation between control, simulation, and SCADA layers
- Operator-focused visibility and alarm logic
- Practical CODESYS implementation suitable for utility-scale systems

It is intended for **controls engineering, power systems, and SCADA-focused roles**.

---

## Author

Developed as a personal engineering project for professional portfolio use.
