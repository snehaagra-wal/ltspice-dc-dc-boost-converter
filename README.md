LTspice DC-DC Boost Converter Project Documentation
Project Overview
This repository contains the complete simulation and troubleshooting files for a DC-DC Boost Converter built in LTspice. The objective of this project was to step up a lower DC input voltage (12V) to a higher regulated output voltage using power electronics principles and iterative circuit debugging.

Key Components Used & Their Functions
Input DC Source (V1): Set to 12V to supply the initial input power to the circuit.

Inductor (L1): Set to 1mH to store electrical energy magnetically when the switching element is closed and release it to boost the voltage.

Switching Control Source (V2): Configured as a high-frequency Pulse generator (0V to 5V) to drive the control terminal of the electronic switch.

Voltage-Controlled Switch (SW): Replaced the generic MOSFET halfway through the troubleshooting process to cleanly toggle internal resistance (R 
on
​
 =0.01Ω, R 
off
​
 =10MΩ) based on the control signal.

Diode (D1): Directs current flow toward the output load and prevents reverse current flow during the switch-on state.

Output Filter Capacitor (C1) & Resistor (R1): Set to 100μF and 50Ω respectively to smooth out the stepped-up voltage and supply a steady DC load.

Troubleshooting & The MOSFET Decision
Initial Approach with Generic MOSFET: We initially attempted to use a standard generic N-channel MOSFET as the switching element.

Why it Failed: Generic library MOSFETs in LTspice require precise internal gate-threshold parameters, spice models, and parasitic values. Without a specific vendor part number or pre-loaded library, the generic MOSFET failed to switch cleanly—acting like a linear or open resistor instead of a hard digital switch—which caused the output voltage to remain stuck at the baseline 12V.

The Breakthrough Fix: We replaced the generic MOSFET with an ideal Voltage-Controlled Switch (SW) paired with the SPICE directive .model SW SW(Ron=0.01 Roff=10Meg Vt=2.5). This eliminated undefined model errors and enabled clean, lossless switching behavior.

Simulation Results & Output Analysis
Transient Response: Running a transient analysis over 20ms (.tran 20ms) allowed the large 100μF output capacitor to complete its transient charging phase.

Voltage Boost: The output waveform transitioned from a gradual upward charging ramp to a stable steady state, successfully stepping up the primary 12V input to a boosted output of approximately 16V–17V.
<img width="1280" height="963" alt="image" src="https://github.com/user-attachments/assets/f9050427-4f0b-4e4b-8ef9-968d43ce02be" />
