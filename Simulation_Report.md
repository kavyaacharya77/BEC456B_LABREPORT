# Design and Analysis of Fully Differential Folded Cascode OTA Circuit using 180nm Technology
### 1. ABSTRACT
This paper presents the simulation and analysis of a fully differential folded cascode amplifier using 180nm CMOS technology. The design focuses on achieving high gain and improved bandwidth. Using LTSpice, the amplifier's frequency response was evaluated. Results show a mid-band gain of approximately 37 dB and a −3 dB bandwidth near 1 11.58 kHz, demonstrating the amplifier’s suitability for high gain, moderate-bandwidth analog applications.

**Keywords** — CMOS analog design,differential amplifier, cascode topology, AC analysis, gain-bandwidth.

### 2. INTRODUCTION
Differential amplifiers are fundamental building blocks in analog and mixed-signal integrated circuits, widely used in operational amplifiers, analog-to-digital converters (ADCs), and communication systems. Their inherent ability to reject common-mode signals and noise makes them essential for high-precision and low-noise applications. To enhance the performance of differential amplifiers, cascode configurations are often employed. The cascode structure combines a common-source stage with a  common-gate stage to significantly increase output resistance and reduce parasitic capacitance effects such as the Miller effect. This leads to improved voltage gain, wider bandwidth, and better frequency response. 

### 3. OTA STRUCTURE
The  structure of folded cascade OTA is shown in Fig. 1. NMOS is used as input differential pair due to their higher electron mobility, which provides greater transconductance and improved speed 

![image](https://github.com/user-attachments/assets/710c3ff6-ef76-40c7-8ede-1085c8a89b49)

A fully differential architecture of folded cascade OTA effectively separates the signal and biasing paths, minimizing voltage headroom limitations and improving overall frequency response. Implemented in 180nm CMOS technology, the folded cascode OTA demonstrates superior performance in terms of gain-bandwidth product and power efficiency, making it ideal for high-speed and low-power analog applications.

### 4. SIMULATION RESULTS

![Screenshot 2025-05-09 183041](https://github.com/user-attachments/assets/729adcd7-a980-4ba9-be13-ac4f88b5b82e)

The DC gain is 37.049dB with phase margin of 89.32° and unity gain bandwidth (UGBW) is 7.87 MHz. The power dissipation of the circuit is 588.9µW which is suitable for low power applications. The OTA parameters and the aspect ratios of the transistors are shown in the tables below.

#### TABLE 1. DIFFERENT OTA PARAMETERS

| PARAMETERS | VALUES |
| ----- | ----- |
| Technology | 180nm |
| Supply Voltage | 1.8V | 
| Gain | 37.049dB |
| Phase Margin | 89.32° |
| UGBW | 7.87 MHz |
| CMRR | 296.5dB |
| PSRR | 262.3dB |
| Power Dissipation | 588.9µW |

#### TABLE 2. ASPECT RATIOS FOR OTA TRANSISTORS

| TRANSISTORS | W/L RATIOS |
| ----- | ------ |
| M1,M2 | 20µ/180n | 
| M3,M4 | 8µ/180n |
| M5,M6 | 6µ/180n | 
| M7,M8 | 10µ/180n |
| M9,M10 | 8µ/180n |
| M11 | 6.15645µ/180n | 

### 5. TAIL CURRENT AND CURRENT ANALYSIS

![Screenshot 2025-05-09 200613](https://github.com/user-attachments/assets/7ee3e881-1014-4b39-9143-b104c45691a9)

In differential amplifier topologies such as the fully 
differential folded cascode OTA, the tail current is the 
current that flows through the tail transistor, usually an 
NMOS device connected to the common source node of the 
differential input pair. This current sets the operating point 
of the differential pair and determines its transconductance. 
In this design, transistors M1 and M2 form the differential 
pair, with the tail transistor biasing both. According to 
simulation data, the drain current of M1 is +50.0002 μA, 
while that of M2 is −50.0002 μA, resulting in a tail current 
of approximately 100.0004 μA, which flows through the tail 
transistor. This symmetry indicates proper differential 
operation and confirms that the biasing is well-balanced. 

The 
OTA utilizes several current mirror 
configurations to replicate bias currents and route them 
appropriately within the circuit. The first mirror pair, M3
M4, mirrors a current of 163.584 μA, with M3 sinking and 
M4 sourcing the same current magnitude, thereby 
demonstrating ideal mirroring behavior. A similar function 
is carried out by the second pair, M5–M6, where both 
transistors mirror 113.583 μA of current. These mirrors 
effectively distribute bias currents to the folded cascode 
branches. 

Additionally, current mirrors in the output stage, 
formed by transistor pairs M7–M8 and M9–M10, replicate 
and steer the output current symmetrically. Each pair 
mirrors a current of 113.583 μA, ensuring that the output 
branches remain balanced and that current steering into the 
load or subsequent stages is stable. 

#### TABLE 3. CURRENT VALUES IN KEY TRANSISTORS

| Transistor | Current (μA) | Description | 
| ----- | ----- | ------ |
| M1 | +50.0002 | Input differential pair (source) | 
| M2 | −50.0002 | Input differential pair (sink) |
| M11(Tail Current) | 100.0004 | Through tail NMOS |
| M3 | −163.584 | Current mirror input | 
| M4 | +163.584 | Current mirror output | 
| M5 | −113.583 | Current mirror input |
| M6 | +113.583 | Current mirror output |
| M7 | −113.583 | Output stage mirror input |
| M8 | +113.583 | Output stage mirror output |
| M9 | −113.583 | Output stage mirror input |
| M10 | +113.583 | Output stage mirror output | 

### 6. CONCLUSION
The design and simulation of the fully differential 
folded cascode OTA using 180nm CMOS technology have 
been successfully carried out in LTSpice. The amplifier 
demonstrates a high DC gain of 37.049 dB, excellent phase 
margin of 89.32°, and a unity gain bandwidth of 7.87 MHz, 
indicating strong performance for high-gain and moderate
bandwidth applications. The low power dissipation of 588.9 
µW further confirms its suitability for low-power analog 
systems. Although ideal simulation conditions yielded high 
CMRR and PSRR values, practical implementation may 
present challenges due to non-ideal factors such as 
mismatch and layout parasitics. Nonetheless, the 
architecture proves to be a viable solution for precision 
analog front-end circuits where gain, bandwidth, and power 
efficiency are critical.

### 7. REFERENCES
[1] B. Razavi, Design of Analog CMOS Integrated Circuits, 
2nd ed., New York, NY, USA: McGraw-Hill, 2016. 

[2] P. E. Allen and D. R. Holberg, CMOS Analog Circuit 
Design, 3rd ed., New York, NY, USA: Oxford Univ. Press, 
2012.

[3] R. J. Baker, CMOS: Circuit Design, Layout, and 
Simulation, 3rd ed., Hoboken, NJ, USA: Wiley-IEEE Press, 
2010. 

[4] Y. Tsividis and C. McAndrew, Operation and Modeling 
of the MOS Transistor, 3rd ed., New York, NY, USA: 
Oxford Univ. Press, 2011. 

[5] N. Wang, X. Liu, and W. Wu, "Design of Low Power 
Folded Cascode OTA in 180nm CMOS Process," in Proc. 
IEEE Int. Conf. ASIC (ASICON), Chongqing, China, 2019, 
pp. 1–4, doi: 10.1109/ASICON47005.2019.8983665. 
