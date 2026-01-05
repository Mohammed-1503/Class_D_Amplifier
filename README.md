Recruit_Vicharak

Class-D Amplifier PCB Design

This is a PCB task made for a recruitment test at Vicharak India involving the design and implementation of a Class-D Audio Power Amplifier.

⸻

Introduction

Audio power amplifiers are used to increase the power level of low-amplitude audio signals so that they can drive a loudspeaker.

Traditional linear amplifiers like Class-A and Class-AB provide good sound quality but suffer from:
	•	Poor efficiency
	•	High heat loss

To overcome these issues, Class-D amplifiers are widely used in modern systems because of:
	•	High efficiency
	•	Compact size

This work focuses on the design of a Class-D audio power amplifier using only basic and commonly available components, without using any dedicated Class-D audio amplifier ICs.

Major Components Used
	•	LM311 Comparator
	•	IR2153 Gate Driver
	•	IRF640 MOSFETs
	•	MJE13005 Transistor
	•	Passive components
	•	LC Output Filter

⸻

Design Objectives

The main objectives of this task are:
	•	Design a Class-D amplifier using discrete, general-purpose components
	•	Design a PCB
	•	Simulate the PCB

⸻

Overall Working Principle

The working of the designed Class-D amplifier can be summarized as follows:
	1.	The audio input signal is fed into a comparator
	2.	The comparator converts the audio signal into a PWM (Pulse Width Modulated) signal
	3.	The PWM signal is conditioned and fed to a MOSFET gate driver
	4.	The gate driver switches the power MOSFETs at high frequency
	5.	The MOSFET output is filtered using an LC filter
	6.	The filtered signal drives the speaker

The audio signal is not amplified directly.
Instead, it controls the duty cycle of a high-frequency switching signal, which is later reconstructed into an amplified audio waveform.

⸻

Component Selection and Design Logic

4.1 LM311 Comparator

Reason for selection:
	•	Fast comparator suitable for high-frequency operation
	•	Open-collector output useful for level shifting
	•	More stable for switching than op-amps

Role in the circuit:
	•	Compares the audio signal with a high-frequency reference
	•	Generates a PWM signal whose duty cycle follows audio amplitude

Why not an op-amp?
	•	Op-amps saturate in comparator applications
	•	Cause slow recovery and distortion at high frequency
	•	LM311 produces clean PWM edges

⸻

4.2 IR2153 Gate Driver IC

Reason for selection:
	•	Built-in dead-time control
	•	Supports half-bridge configuration
	•	Bootstrap high-side drive capability
	•	Reliable and widely used in SMPS

Role in the circuit:
	•	Converts PWM logic into proper gate drive signals
	•	Prevents both MOSFETs from turning ON simultaneously

Why not drive MOSFETs directly?
	•	MOSFET gates need high current for fast switching
	•	Comparator outputs are insufficient
	•	IR2153 ensures safe and reliable switching

⸻

4.3 IRF640 Power MOSFETs

Reason for selection:
	•	High voltage rating (200 V)
	•	High current handling
	•	Suitable for high-frequency switching

Role in the circuit:
	•	Act as switches (not linear devices)
	•	Generate high-power PWM waveform

Why MOSFETs instead of BJTs?
	•	Faster switching
	•	Lower switching losses
	•	Higher efficiency at high frequency

⸻

4.4 MJE13005 Transistor

Reason for selection:
	•	High voltage handling
	•	Good current gain

Role in the circuit:
	•	Used to derive a regulated +15 V supply for IR2153 from the −40 V rail

⸻

4.5 LC Output Filter (35 µH Inductor)

Reason for selection:
	•	Cutoff frequency above audio range
	•	High current handling
	•	Effective ripple reduction

Role in the circuit:
	•	Removes high-frequency PWM
	•	Passes only audio-frequency signal to speaker

Why not connect speaker directly?
	•	Causes heating and noise
	•	Poor sound quality
	•	LC filter is mandatory

⸻

4.6 Capacitors

Used for:
	•	Decoupling (100 nF): High-frequency noise reduction
	•	Electrolytic (4.7 µF – 10 µF): Supply stability
	•	Filter capacitor: LC output filter

⸻

4.7 Zener Diodes

Roles:
	•	Generate stable ±15 V supplies
	•	Protect sensitive components
	•	Clamp voltage spikes

Why not regulators?
	•	Zeners are simple, cheap, and sufficient for low-current control sections
