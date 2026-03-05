# PLC Palletizing Cell – Conveyor + Cartesian Manipulator (CODESYS / S7-1200)

This repository contains a PLC programming project for an automated palletizing workstation. The system picks cartons from a production conveyor and places them onto a pallet in predefined positions using a simple 2-axis (X/Y) manipulator with a gripper.

## Project goal
Automate the sequence of:
1) detecting a carton on the conveyor,
2) stopping the conveyor at the pickup zone,
3) picking the carton with an open/close gripper,
4) placing cartons one-by-one onto the pallet pattern,
5) pausing production when the pallet is full and waiting for pallet replacement acknowledgement. 
## Functional overview
**Operator controls**
- **S1** – Start conveyor / start production
- **S2** – Stop
- **S3** – Pallet removed / acknowledgement (reset after full pallet)
- **S4** – Emergency stop (safety mushroom) 

**Sensors**
- **B1–B7** – Position detection of the carton / manipulator states (used to recognize pickup/placement zones and pallet position progress). 

**Actuators (outputs)**
- **K1** – Manipulator Y-axis drive
- **K2** – Manipulator X-axis drive
- **K3** – Conveyor motor start (via contactor)
- **K4** – Gripper open/close

## Sequence of operation (high level)
1. When production is enabled, the conveyor runs.
2. When the carton is detected in the pickup area (B6/B7 logic), the manipulator moves down with an open gripper, closes the gripper, and lifts the carton.
3. The first carton is placed at the first pallet target position, then the manipulator follows the defined trajectory for subsequent cartons and fills the pallet until the final target position is reached.
4. After the pallet is full, production stops, the manipulator returns to the home position, and the system waits until the operator replaces the pallet and confirms with **S3**.

## Hardware (example components used)
- PLC: **Siemens SIMATIC S7-1200**
- Capacitive sensor (example): **C18-P**
- Contactor (example): **MC-22b 24VDC**
- Push buttons: **LP9S11R** (S1/S2/S3)
- Emergency stop button (S4)
- Signal lamps: green (H1) and yellow (H2)

## HMI
An operator panel is included to visualize the conveyor/manipulator status, pallet progress, and basic controls (start/stop/emergency/pallet acknowledgement).




