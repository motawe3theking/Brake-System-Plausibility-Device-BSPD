# Brake System Plausibility Device (BSPD)

## Overview
This project implements a standalone, non-programmable **Brake System Plausibility Device (BSPD)** designed for Formula Student Electric Vehicles (EVs). The BSPD monitors the brake system pressure and power delivery to ensure safe isolation of the tractive system during hard braking, complying with Formula Student rules.

## Features
- **Non-Programmable Design:** Implemented using analog components, comparators, and RC-Comparator delay circuits for increased safety and compliance.
- **Hall Effect Current Sensor:** Utilizes the **L06P S05 TAMURA** current sensor to detect power delivery ≥ 5kW.
- **Brake Pressure Sensor:** Ensures accurate detection of hard braking conditions without causing wheel lockup (<= 30 bar).
- **Fault Latching and Reset:** Fault state is latched and maintained until a 10s timer elapses or the LVMS is power-cycled.
- **Simulation and Prototyping:** Designed and tested using LTspice, with multiple prototype iterations for optimal performance.

## Technology and Components Used
- **Current Sensor:** Hall Effect Sensor (L06P S05 TAMURA)
- **Comparators and Logic ICs:** LM358 Op-Amps, SN74HCS4075 OR Gate
- **Timer and Relay:** NE555 Timer, T90 Relay (SLA-12VDC-SL-A)
- **Voltage Regulation:** LM7805CT Voltage Regulator
- **PCB Design:** Designed using Altium
- **Simulation Tool:** LTspice for circuit simulation and testing

## Formula Student Rule Compliance
The BSPD complies with the following rules:
- **T11.6.1:** Opens the shutdown circuit when hard braking occurs while delivering ≥ 5kW power to the motors.
- **T11.6.5:** Uses a brake system pressure sensor to detect hard braking.
- **T11.6.6:** Measures power delivery using a DC circuit current sensor equivalent to 5kW.
- **T11.6.9:** The function is provable during technical inspection with appropriate signal simulation.
- **T11.6.10:** BSPD is designed to be installed outside the TSAC.
- **T11.9.2:** Ensures safe or error states during single failures in the SCS.


## How It Works
1. **Power Cycling:** The BSPD is initialized upon power cycling the LVMS.
2. **Sensor Check:** Sensors are validated within 0.5s using comparators connected to the negative terminal.
3. **Fault Detection and Latching:**
   - If a fault is detected:
     - The state is latched (low logic) and the BSPD LED is triggered.
     - A 10s timer (using NE555) is activated.
     - The shutdown circuit remains open until the timer finishes or the LVMS is power-cycled.
   - If no fault is detected:
     - The BSPD relay is energized.
     - The state is latched (high logic) to maintain normal operation.
4. **Safety and Reset:** The system safely latches errors and resets only when the fault condition is cleared for more than 10s.
![image](https://github.com/user-attachments/assets/d22829d7-84b2-4cf8-bbcb-4e01a2519c38)

## Design and Prototyping
### First Prototype
![image](https://github.com/user-attachments/assets/986cb41e-f3ae-42bd-9769-df6ce873ccaa)

- Implemented basic RC-Comparator delay circuits and fault latching.

### Second Prototype
![image](https://github.com/user-attachments/assets/5f7289c9-5e7d-4b8f-ac06-a4c3182d1d7c)

- Enhanced with sensor short-circuit detection.
- Reduced the number of transistors by using **SN74HCS4075 OR Gate** from Texas Instruments.
- Replaced standard op-amp with **LM358 Comparator**.

### Third Prototype
![image](https://github.com/user-attachments/assets/e2b447da-2e8a-4fb8-90b2-8f7c7b125666)
![image](https://github.com/user-attachments/assets/ac2a18f6-f83e-4a2b-a2ea-45e3429239fe)

- Added a CMOS NOT gate and replaced the buck converter with an **LM7805CT Voltage Regulator**.
- Improved reliability and reduced space usage on the PCB.

## PCB Design and BOM
- PCB designed with compact layout and mounting holes.
- ![image](https://github.com/user-attachments/assets/4d305256-7967-4dd4-935c-3da3fc635130)

- **Bill of Materials (BOM):**
  - T90 Relay (SLA-12VDC-SL-A)
  - OR Gate (SN74HCS4075)
  - Op-Amps (LM358)
  - NE555 Timer
  - 4 NPN Transistors
  - LM7805CT Voltage Regulator

## Future Improvements
- Replace the CMOS NOT gate with a more efficient logic solution.
- Finalize BOM with Egyptian currency for local sourcing.

## Installation and Usage
1. **Clone the Repository:**
   ```bash
   git clone https://github.com/motawe3theking/Brake-System-Plausibility-Device-BSPD.git
   cd Brake-System-Plausibility-Device-BSPD
