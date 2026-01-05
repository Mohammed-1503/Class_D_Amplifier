# Recruit_Vicharak
This is a PCB task made for recruitment test at Vicharak India
Design and Implementation of a Class-D Amplifier

1. Introduction
Audio power amplifiers are used to increase the power level of low-amplitude audio signals so that they can drive a loudspeaker. Traditional linear amplifiers like Class-A and Class-AB provide good sound quality but suffer from poor efficiency and high heat loss. To overcome these issues, Class-D amplifiers are widely used in modern systems because of their high efficiency and compact size.
This work focuses on the design of a Class-D audio power amplifier using only basic and commonly available components, without using any dedicated Class-D audio amplifier ICs. The design consists of LM311 comparator, IR2153 gate driver, IRF640 MOSFETs, MJE13005 transistor, passive components, and an LC output filter.

2. Design Objectives
The main objectives of this Task are listed below:
•	To design a Class-D amplifier using discrete and general-purpose components.
•	To design a PCB.
•	Simulate the PCB

3. Overall Working Principle
The working of the designed Class-D amplifier can be summarized as follows:
I.	The audio input signal is fed into a comparator.
II.	The comparator converts the audio signal into a PWM (Pulse Width Modulated) signal.
III.	This PWM signal is conditioned and fed to a MOSFET gate driver.
IV.	The gate driver switches the power MOSFETs at high frequency.
V.	The MOSFET output is filtered using an LC filter.
VI.	The filtered signal drives the speaker.
In this design, the audio signal is not amplified directly. Instead, it controls the duty cycle of a high frequency switching signal, which is later converted back into an amplified audio waveform.

4. Component Selection and Design Logic
4.1 LM311 Comparator
The LM311 is used as the heart of the PWM generation stage.
Reason for selection:
•	It is a fast comparator suitable for high-frequency operation
•	It has an open-collector output, which is useful for level shifting
•	It is more stable for switching applications compared to op-amps
Role in the circuit:
The LM311 compares the audio signal with a high-frequency reference waveform. Based on this comparison, it produces a PWM signal whose duty cycle changes according to the audio amplitude.
Why not an op-amp?
Op-amps are designed for linear operation and tend to saturate when used as comparators. This causes slow recovery and distortion at high switching frequencies. LM311 avoids this issue and produces cleaner PWM edges.

4.2 IR2153 Gate Driver IC
The IR2153 is used to drive the high-side and low-side MOSFETs.
Reason for selection:
•	Built-in dead-time control
•	Supports half-bridge configuration
•	Can drive high-side N-channel MOSFETs using bootstrap method
•	Reliable and commonly used in SMPS circuits
Role in the circuit:
The IR2153 receives the PWM logic signal and converts it into proper gate drive signals for the MOSFETs. It ensures that both MOSFETs never turn ON at the same time.
Why not drive MOSFETs directly?
MOSFETs require fast charging and discharging of their gate capacitance. Logic signals from comparators cannot provide sufficient current or proper voltage levels, especially for high side switching. The IR2153 solves this problem safely.

4.3 IRF640 Power MOSFETs
The IRF640 MOSFETs are used as the main switching elements.
Reason for selection:
•	High voltage rating (200 V)
•	Can handle high current
•	Suitable for high-frequency switching
Role in the circuit:
The MOSFETs act as switches rather than linear devices. They connect the output alternately to the positive and negative supply rails at high speed, creating a high-power PWM waveform.
Why MOSFETs instead of BJTs?
MOSFETs have faster switching speed, lower switching losses, and higher efficiency compared to BJTs at high frequencies. This is critical for Class-D operation.

4.4 MJE13005 Transistor
The MJE13005 is used as a buffer and signal conditioning transistor.
Reason for selection:
•	High voltage handling
•	Good current gain
Role in the circuit:
In this circuit, the MJE13005 transistor is mainly used to derive a regulated +15 V supply for the IR2153 from the −40 V rail.

4.5 LC Output Filter (35 µH Inductor)
The LC filter is a critical part of the Class-D amplifier.
Reason for selecting 35 µH inductor:
•	Suitable cutoff frequency above audio range
•	Can handle high output current
•	Reduces switching ripple effectively
Role in the circuit:
The LC filter removes the high-frequency PWM component and allows only the audio-frequency signal to reach the speaker.
Why not connect speaker directly?
Direct PWM to the speaker causes heating, noise, and poor sound quality. The LC filter is mandatory to reconstruct the analog waveform.

4.6 Capacitors
Different capacitors are used for different purposes:
•	Decoupling capacitors (100 nF): Reduce high-frequency noise
•	Electrolytic capacitors (10 µF – 4.7 µF): Supply stability
•	Filter capacitor: Part of LC output filter
Without proper capacitor placement, the circuit becomes unstable and noisy.

4.7 Zener Diodes
Zener diodes are used for voltage regulation and protection.
Roles:
•	Generate stable ±15 V supply for control circuitry
•	Protect sensitive components from over-voltage
•	Clamp unwanted voltage spikes
Why not use regulators?
Zener are simple, cheap, and sufficient for low-current control circuits in this design.

4.8 Resistors
Resistors are used throughout the circuit for:
•	Biasing
•	Current limiting
•	Gate damping
•	Pull-up and pull-down functions
Each resistor value is selected to maintain stable operation and prevent excessive current flow.

4.9 Screw Terminals
Screw terminals are used for:
•	Power input
•	Speaker output
•	Audio input
They provide strong mechanical connection and are suitable for high-current paths.

5. Step-by-Step Working of the Circuit
I.	Audio signal is applied to the LM311 input
II.	LM311 generates PWM based on audio amplitude
III.	MJE13005 supplies +15v to IR2153
IV.	IR2153 produces complementary gate signals with dead-time
V.	IRF640 MOSFETs switch the supply rails
VI.	LC filter smoothens the output
VII.	Speaker receives amplified audio signal

6. Significance of the Design
•	High efficiency compared to linear amplifiers
•	Lower heat generation
•	Uses commonly available components
•	Easy to understand and troubleshoot

7. PCB Design and Layout Considerations
PCB design plays a very important role in the proper working of a Class-D amplifier. Since this circuit involves high frequency switching and high current, the PCB layout has a direct impact on noise, efficiency, and reliability. Even a small mistake in routing or grounding can cause instability or MOSFET failure.
For this task, a two-layer PCB of size 77x45mm was designed using Altium Designer, keeping manufacturability and debugging in mind.

7.1 PCB Layer Selection
A 2-layer PCB was selected for this design.
•	Top Layer: Signal routing and power traces
•	Bottom Layer: Continuous ground plane
This approach was chosen because it provides a low-impedance ground reference for all signals while keeping the design simple and cost-effective. A four-layer board was not used because the circuit complexity does not justify it, and proper grounding can still be achieved using a two-layer board.

7.2 Ground Plane Strategy
The entire bottom layer is used as a solid ground plane.
This helps in:
•	Reducing ground impedance
•	Providing clean return paths for signals
•	Minimizing EMI caused by high-frequency switching
•	Improving stability of LM311 and IR2153
Care was taken to ensure that:
•	Signal ground and power ground meet at a common point
•	High current return paths do not interfere with sensitive control circuitry
Using a full ground plane is especially important in Class-D amplifiers due to fast switching edges.

7.3 Placement of Power Components
Power components such as IRF640 MOSFETs, LC filter inductor, bulk capacitors, and screw terminals were placed first during PCB design.
Placement decisions were based on:
•	Minimizing high-current loop area
•	Keeping MOSFETs close to the LC filter
•	Reducing trace length for switching paths
The MOSFETs were placed near the output section to ensure that the high-current PWM signal travels the shortest possible distance before filtering.

7.4 Placement of Control and Driver Components
Low-power and sensitive components such as:
•	LM311 comparator
•	IR2153 gate driver
•	MJE13005 transistor
•	Small resistors and capacitors
were grouped together and placed away from the high-power switching section.
This separation helps in:
•	Reducing noise coupling
•	Preventing false triggering
•	Improving overall circuit stability
The control section layout also makes the signal flow easier to understand and debug.

7.5 Routing of High-Current Traces
High-current traces such as:
•	±40 V supply lines
•	MOSFET drain and source paths
•	Speaker output lines
were routed using wide traces wherever possible.
This was done to:
•	Reduce voltage drop
•	Minimize heating
•	Improve current handling capability
Sharp corners were avoided, and smoother trace routing was preferred to reduce EMI.

7.6 Gate Drive Routing Considerations
Gate drive signals from the IR2153 to the IRF640 MOSFETs are high-speed signals and require careful routing.
Steps taken:
•	Gate resistors placed close to MOSFET gate pins
•	Gate traces kept short and direct
•	Gate routing kept away from LC filter and output traces
These steps help in reducing ringing, overshoot, and unwanted oscillations at the MOSFET gates.

7.7 Decoupling and Bypass Capacitor Placement
Decoupling capacitors were placed as close as possible to the power pins of LM311 and IR2153.
Bulk capacitors were placed near the power input and MOSFETs to:
•	Provide instant current during switching
•	Reduce voltage ripple
•	Improve power supply stability
Both ceramic and electrolytic capacitors were used to cover a wide frequency range.

7.8 Thermal Considerations
Power MOSFETs and some resistors generate significant heat during operation.
To handle this:
•	Provision for mounting external heatsinks was kept
•	Component spacing was increased to improve airflow
These measures help in improving long-term reliability of the amplifier.

7.9 EMI and Noise Reduction Measures
Since Class-D amplifiers are prone to EMI, the following steps were taken:
•	Solid ground plane on bottom layer
•	Short switching loops
•	Proper separation between input and output sections
•	LC filter placed close to output
These steps significantly reduce switching noise and prevent interference with the audio signal.

8. PCB Design Summary
The PCB design focuses on:
•	Stable grounding
•	Controlled current flow
•	Minimal switching loop area
•	Safe separation of power and signal paths
The final PCB layout supports reliable Class-D operation while remaining easy to fabricate and debug.

9. Limitations and Scope for Improvement
Some limitations of the current design include:
•	EMI performance depends heavily on PCB layout
•	Discrete regulation consumes some power
•	Further optimization can reduce noise
Future improvements may include:
•	Better shielding
•	Optimized inductor design
•	Improved thermal management

10. Conclusion
In this task, a Class-D audio power amplifier was designed and implemented using commonly available discrete components. The design avoids specialized Class-D audio ICs and focuses on understanding the working principle at component and PCB level. The use of LM311 for PWM generation, IR2153 for gate driving, IRF640 MOSFETs for power switching, and an LC output filter results in an efficient and reliable amplifier.
Proper PCB layout played a major role in achieving stable operation. Overall, the project successfully meets its objectives and provides strong practical learning in power electronics and PCB design.

11. Attachments
Figure 1: Schematic Diagram of the Class-D Amplifier
<img width="940" height="622" alt="image" src="https://github.com/user-attachments/assets/7b12f961-f53a-430c-90bf-6f91a0ed9501" />

 
Figure 2: PCB Layout (Top and Bottom Layers)
<img width="940" height="565" alt="image" src="https://github.com/user-attachments/assets/e8752c49-8fcf-4a0e-afd5-befaa7ae1071" />

 
Figure 3: 3D View of the PCB
<img width="940" height="699" alt="image" src="https://github.com/user-attachments/assets/6dc6558f-0fae-4504-b0bd-57e747f65eb5" />





