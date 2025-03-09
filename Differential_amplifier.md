# Design and Analysis of MOS Differential Amplifier   
### 1. AIM    
To design and analyse the differential amplifier for the following specifications.    
- Vdd = 2.2V
- P <= 2.2mW
- Vicm = 1.2V
- Vocm = 1.25V
- Vp = 0.4V

Perform DC analysis, transient analysis, frequency response and extract the parameters.
### 2. COMPONENTS USED      
The following components are used in the MOS differential amplifier circuit along with their key specifications:  
| Components | Specification | Purpose |
|-------|-----|------|
| MOSFETs(M1,M2,M3) | CMOSN (TSMC 0.18um) | Acts as the active amplifying element in the differential amplifier |     
| Drain Resistors (Rd1,Rd2) | 1.9kohm | Used for converting the drain current to voltage signal |         
| Source Resistor (Rss) | 400ohm | Provides tail current for the MOSFET differential amplifier |   
| DC Voltage source (Vdd1) | 2.2V, stable power supply | Powers the amplifier circuit |
| AC signal source (V1,V2) | 1kHz, 50mV (for input testing ) | Provides the input differential signal for analysis |    
| MOSFET model library | .lib "D:\Documents\tsmc018.lib" | Defines MOSFET characteristics |

### 3. THEORY
A MOS differential amplifier is one of the most important buliding blocks in analog circuits, particularly in operational amplifiers, sensor interfaces and communication systems, designed to amplify the volatge difference between the two input signals while rejecting common mode noise. It consists of two matched MOSFETs(M1 and M2) that shares a common current source, allowing them to operate in a symmetrical fashion. The sources of both transistors are connected together and tied to a current source, which provides a stable tail current (Iss). The drains of M1 and M2 are connected to supply voltage (Vdd) through drain resistors.    
  
![dffamp_image](https://github.com/user-attachments/assets/f616034b-7c2c-4e5a-bcfd-77c0e8b6aa61)   

When a differential input signal is applied, the transitor receiving the higher input voltage conducts more current, while the other transistor conducts less. This causes an imbalance in the drain currents, resulting in a voltage difference across the drain resistors, which forms the amplified output signal. If both input voltages are equal (common-mode signal), the transistors conduct equally, and the output voltage remains unchanged, effectively canceling out noise and interference. The tail current source plays a crucical role in ensuring the stability of the circuit by maintaining a constant total current, preventing unwanted variations in performance. Proper selection of component values ensures an optimal balance between gain, stablility, and frequency response, making the MOS differential amplifier a crucial component in precision analog applications.    

### Key Features of MOS Differntial Amplifier
| Feature | Description |
|-------|------|
| Common-Mode Rejection Ratio (CMRR) | The ability of the amplifier to reject unwanted common-mode signals. A high CMRR ensures that only differential signals are amplified, improving signal integrity. |      
| Differential Gain | The amplifier enchances the difference between two input signals while suppressing common-mode noise, making it useful for precision applications like sensor circuits and ADCs. |     
| Low Power Consumption | The MOS differentail amplifier is highly efficient and consumes low power, making it suitable for battery-powered applications suc as wearable electronics and biomedical sensors. |     
| High Input Impedance | The amplifier provides a high input impedance, which means it does not significantly load the previous circuit stage, preserving signal strength. |    
| High Linearity | The differential pair ensures that the output is proportional to the input signal difference, reducing harmonic distortion and improving accuracy. |
| Scalability | The design can be modified to include active current sources and cascode configurations to further enhance performance in high-precision applications. |     

### Basic Operation Of a MOS Differential Amplifier    
- When a differentail input signal is applied, one transistor in the pair turns **ON** more while the other turns **OFF** slightly, creating a **voltage difference** at the drains.
- If the **same signal** is applied to both inputs, the circuit **rejects it**, producing no differential output.
- The **drain resistors** convert the drain currents into voltage signals, which are then used as the differential output.
- The **tail current source** ( a resistor or an active current source) ensures that the total current through both MOSFETs remains **constant**, improving gain stability and performance.

This fundamental working principle makes MOS differential amplifiers an essential pert of modern analog circuit design.    

### 4. CIRCUIT DESIGN AND CALCULATIONS 
### Circuit 1: Basic Differential Pair with a Resistor as a Tail current Source 

![ckt3_1](https://github.com/user-attachments/assets/a36bf977-7be2-4171-80f9-7189f2d6fb0a)

#### <ins> Design Calculations </ins>   
1. Determine the source current (Iss):
   
   Iss = $P/Vdd$ = $2.2mW/2.2$ = 1mA
   
3. Calculate the drain resistance (Rd1,Rd2):

   Id = $Iss/2$ = $1mA/2$ = 0.5mA
   
   Rd1 = Rd2 = $Vdd - Vocm/Id$ = $2.2 - 1.25/0.5m$ = 1.9kohm
   
5. Calculate source resistance (Rss):
   
   Rss = $Vp/Iss$ = $o.4/1m$ = 400ohm

6. Calculate gain of the circuit:

   gm = 2.51m

   Av = gm * Rd = 2.51m * 1.9k = 4.77V/V

### 5. SIMULATION AND ANALYSIS    
### <ins> 5.11 DC Analysis 
DC analysis helps to determine the operating point of the circuit, which defines the steady-state voltages and currents. In a MOS differential amplifiier, this is crcucial for ensuring that both the transistors operate in the **saturation region**. By running DC operating point analysis in LTspice, we can measure the drain current(Id), gate-source voltage(Vgs), and drain-source voltage(Vds) of both MOSFETs. A well set Q point ensures low distortion and proper amplification, making this step essential before performing transient and AC analysis.     

### <ins> Procedure </ins>   
1. Set up the circuit in LTspice
2. Apply the supply voltage and ensure the tail current source is correctly defined.
3. Run a DC operating point analysis
   - Go to **simulate** > **Edit Simulation Cmd** > **DC op pnt** and select **.op**
4. Observe the key parameters like drain currents, common-mode voltage, gate-source voltage etc. If the values doesn't match with the design specifications, vary the widths of the MOSFETs(M1 and M2) while keeping its length constant i.e 0.18um.

![ckt3_1dcop](https://github.com/user-attachments/assets/a9c4ec13-af9b-4fbe-87c3-d2f74e3181ae)

5. Next select **view** > **command goto** > **SPICE errorlog** option to check Vgs, Vth , Vds etc.
 
![ckt3_spiceerror](https://github.com/user-attachments/assets/2f824825-ae10-49a4-9002-a06b89764d1d) 

From the above image we check whether the MOSFET operates in saturation region.     
- Vgs = 0.8V, Vds = 0.85V, Vth = 0.495V      
- 0.8V > 0.495V therfore, Vgs > Vth.
- And 0.85V > (0.8-0.495)V = 0.85V > 0.305V therefore Vds>Vov.
- This implies that both the MOSFETs operate in saturation region.    

Vicm(min) = Vth + Vp = 0.366 + 0.4 = 0.766V.     

Vicm(max) = Vdd - (Id * Rd) + Vth = 2.2 - (0.5m * 1.9k) + 0.366 = 1.616V. 

Vocm(min) = Vov1 + Vov3 = 0.434 + 0.4 = 0.834V.

Vocm(max) = Vdd - (Id * Rd) = 2.2 - (o.5m * 1.9k) = 1.25V.

### <ins> 5.21 Transient Analysis 
Transient analysis evaluates the circuit's time-domain response to varying input signals. This analysis helps to visualise how the differential amplifier processes fast-changing signals. By applying a small AC input voltage at both gate terminals, we can observe the amplifier's **differential gain, phase shift, and transient behaviour** over time. The output waveforms reveal how well the amplifier responds to dynamic inputs, helping us understand signal amplification, delay, and stability.   

### <ins> Procedure </ins>   
1. Apply a sinusoidal input ac signal.
2. Go to **simulate** > **Edit Simulation Cmd** > **Transient**.Choose a suitable time step let' say 3m.
3. Run the transient analysis and observe the input and output waveforms, the phase shift between the input and output and calculate the gain.

#### INPUT AND OUTPUT WAVEFORMS

![ckt3_1vin1vout1](https://github.com/user-attachments/assets/11655056-ef88-43da-b41d-6a1fae010671)

![Screenshot 2025-03-05 211631](https://github.com/user-attachments/assets/558f2ea2-6f74-4485-8a8a-7531668af0a4)

![ckt3_1_vin12](https://github.com/user-attachments/assets/4fb5c788-321d-45db-8227-d10378827a29)

![ckt3_1vout12](https://github.com/user-attachments/assets/823f475a-859d-48e4-8a6c-78fd1b5741b2)

- Gain Av = $Vout1 - Vout2/Vin1 - Vin2$ = $398.69m/99.348m$ = 4.013V/V.

- In dB scale Av = 20log(4.013) = 12.07dB.

### <ins> 5.31 AC Analysis
AC analysis exmaines the frequency response of the amplifier, determining its gain, bandwidth, and phase characteristics. By sweeping the input signal frequency from low (0.1Hz) to high (1THz) in LTspice, we can observe how the amplifier responds across different frequencies. This helps determine the gain bandwidth product(GBW), -3dB cutoff frequency, and phase shift behaviour. The results include how effectively the amplifier reatins signal integrity while fitering out unwanted noise. A well designed MOS differential amplifier shpuld maintain a constant gain within its operating frequency range before gradually attenuating signals at higher frequencies.   

### <ins> Procedure </ins>   
1. Apply a small AC signal at the input.
2. Set AC amplitude to 1V in the input voltage source properties.
3.  Go to **simulate** > **Edit Simulation Cmd** > **AC Analysis**. Select decade sweep with the frequency range of 0.1Hz to 1THz.
4.  Run the simualation and observe the Gain(Vout/Vin) vs. frequency plot, Phase shift vs.frequency and 3dB cutoff frequency (bandwidth).

 ![ckt3_1acanaysis](https://github.com/user-attachments/assets/8a27e914-b48b-41f8-9499-24a5b5e4ecca)

From the frequency response graph, we observe the gain in dB scale is 12.128dB and the dB cutoff frequency (bandwidth) is 21.8GHz.

| Gain | Theoretical value | Practical value |
|------|--------|------|
| Av(V/V) | 4.77 | 4.013 |
| Av(dB) | 12.07 | 12.128 |     

### 6. CIRCUIT MODIFICATIONS AND ENHANCEMENTS
### Circuit 2: Using an Ideal Current Source Instead of Resistor

![ckt3_2](https://github.com/user-attachments/assets/c9db2f1f-8a1a-42ba-8e48-6e6cbdd80c21)   

#### Why? 
- A resistor based tail current depends o supply variations.
- Increases input impedance.
- Using an ideal current source improves biasing stability.

### <ins> 5.12 DC Analysis
(Follow the same procedure as mentioned in circuit 1)

![ckt3_2dcop](https://github.com/user-attachments/assets/4eb9d5e5-dce4-46dc-9df9-096cf3c42057) 

![ckt3_spiceerror](https://github.com/user-attachments/assets/2f824825-ae10-49a4-9002-a06b89764d1d) 

From the DC analysis, It is proved that the MOSFETs operate in saturation region.

### <ins> 5.22 Transient Analysis 
(Follow the same procedure as mentioned in circuit 1)

![ckt3_2vin12](https://github.com/user-attachments/assets/f69c6366-1f79-497a-b0c0-ab4848fdd234)

![ckt3_2vout12](https://github.com/user-attachments/assets/b682d986-11bc-4cd2-bdaa-6f5a32d0f12c)


- Gain Av = $Vout1 - Vout2/Vin1 - Vin2$ = $398.53m/99.169m$ = 4.0186V/V.

- In dB scale Av = 20log(4.0186) = 12.0815dB.

- Better common-mode rejection.

### <ins> 5.32 AC Analysis
(Follow the same procedure as mentioned in circuit 1)

![ckt3_2acana](https://github.com/user-attachments/assets/4ab27fb0-5328-43ea-9bf2-f70f3c3e706c)

From the frequency response graph, we observe the gain in dB scale is 12.131dB and the dB cutoff frequency (bandwidth) is 22.187GHz.

| Gain | Theoretical value | Practical value |
|------|--------|------|
| Av(V/V) | 4.77 | 4.0186 |
| Av(dB) | 12.0815 | 12.131 |    

### Circuit 3: Active Current Source (NMOS) Instead of Resistor  

![ckt3_3](https://github.com/user-attachments/assets/251892ba-a895-4350-904a-9833a4459fc7)

#### Why? 
- More stable tail current - less affeted by supply fluctuations.
- Improved biasing - Ensures better transistor matching.

### <ins> 5.13 DC Analysis
(Follow the same procedure as mentioned in circuit 1)
By varying the width of the NMOS M3, we set the DC operating point. Here we have kept the width as W = 15.1366um and length L = 180nm for all the three MOSFETs (M1,M2 and M3).

![ckt3_3oppnt](https://github.com/user-attachments/assets/89c414bd-35d4-4062-8f3a-4a688ecebb6b)

![ckt3_3spice](https://github.com/user-attachments/assets/46cde0d5-85c6-4914-9d15-95f4fbcc91bf)

We need to check whether the MOSFETs M1, M2 and M3 are in saturation mode.
#### For NMOS M1 and M2 
- Vgs = 0.68V, Vds = 0.73V, Vth = 0.497V      
- 0.68V > 0.497V therfore, Vgs > Vth.
- And 0.73V > (0.68-0.497)V = 0.73V > 0.183V therefore Vds>Vov.
- This implies that both the MOSFETs operate in saturation region. 

#### For NMOS M3
- Vb = Vp + Vth = 0.4 + 0.366 = 0.766V
- Vgs = 0.766V, Vds = 0.52V, Vth = 0.476V      
- 0.766V > 0.476V therfore, Vgs > Vth.
- And 0.52V > (0.766-0.476)V = 0.85V > 0.29V therefore Vds>Vov.
- This implies that the MOSFET M3 operates in saturation region.

### <ins> 5.23 Transient Analysis 
(Follow the same procedure as mentioned in circuit 1)

#### INPUT AND OUTPUT WAVEFORMS

![ckt3_3vin1vout1](https://github.com/user-attachments/assets/e9bdc4ec-69fd-4b1a-83cd-b6f9f16b62a8)

![ckt3_3vin2vout2](https://github.com/user-attachments/assets/6741d9bb-6c0e-41d6-abca-b111eb23eb78)

![ckt3_3vot12](https://github.com/user-attachments/assets/884fa520-c57d-4cd6-851b-c8eaa87abfd8)

- Gain Av = $Vout1 - Vout2/Vin1 - Vin2$ = $657.64m/99.356m$ = 6.619V/V.

- In dB scale Av = 20log(6.619) = 16.4158dB.

- Better stability and noise immunity.

### <ins> 5.33 AC Analysis
(Follow the same procedure as mentioned in circuit 1)

![ckt3_3acan](https://github.com/user-attachments/assets/e207ef4e-5d9d-48b6-ac1a-819115248557)

From the frequency response graph, we observe the gain in dB scale is 16.69dB and the dB cutoff frequency (bandwidth) is 19.0688GHz.

| Gain | Theoretical value | Practical value |
|------|--------|------|
| Av(V/V) | 4.77 | 6.619 |
| Av(dB) | 16.4158 | 16.69 |   

### Circuit 4: Active Current Source (PMOS) Instead of Drain Resistors 

![ckt3_4](https://github.com/user-attachments/assets/1901c0e9-3332-425d-b0fa-8697bd8ebbcb)

### <ins> 5.14 DC Analysis
(Follow the same procedure as mentioned in circuit 1)
By varying the width of the MOSFETs, we set the DC operating point. Here we have kept the width of NMOS (M1 and M2) and PMOS (M4 and M5) as W1 = 10.668um and NMOS M3 as W2 = 15.377um and length L = 180nm for all the fuve MOSFETs (M1,M2,M3,M4 and M5).

![ckt3_4oppnt](https://github.com/user-attachments/assets/5943e7f5-1307-4837-807c-d2a6e8e14003)

![ckt3_4spice](https://github.com/user-attachments/assets/bf958fd6-9d0c-46ff-bf39-67ee2a59032d)

We need to check whether the MOSFETs M1, M2 M3, M4 and M5 are in saturation mode.
#### For NMOS M1 and M2 
- Vgs = 0.721V, Vds = 0.771V, Vth = 0.496V      
- 0.721V > 0.496V therfore, Vgs > Vth.
- And 0.771V > (0.721-0.496)V = 0.771V > 0.225V therefore Vds>Vov.
- This implies that both the MOSFETs operate in saturation region. 

#### For NMOS M3
- Vgs = 0.766V, Vds = 0.479V, Vth = 0.477V      
- 0.766V > 0.477V therfore, Vgs > Vth.
- And 0.479V > (0.766-0.477)V = 0.479V > 0.29V therefore Vds>Vov.
- This implies that the MOSFET M3 operates in saturation region.
  
#### For PMOS M4 and M5
- Vgs = 0V, Vds = 0.95V, Vth = -0.506V      
- 0V > -0.506V therfore, Vgs > Vth.
- And 0.95V > (0-0.506)V = 0.95V > 0.506V therefore Vds>Vov.
- This implies that the MOSFETs M4 and M5 operate in saturation region.

### <ins> 5.24 Transient Analysis 
(Follow the same procedure as mentioned in circuit 1)

#### INPUT AND OUTPUT WAVEFORMS

![ckt3_4vin1vout1](https://github.com/user-attachments/assets/e1594890-6a5d-4367-a554-e80596f64fd6)

![ckt3_4vin2vout2](https://github.com/user-attachments/assets/df96ab07-6310-48c5-bbb8-c5d6ce17767d)

![ckt3_4vin12](https://github.com/user-attachments/assets/d608f814-d7e4-4af8-8e3a-169a72fa90c2)

![ckt3_4vout12](https://github.com/user-attachments/assets/af460f98-e515-4827-a264-d84f8a61bbcd)


- Gain Av = $Vout1 - Vout2/Vin1 - Vin2$ = $179.24m/99.534m$ = 1.8V/V.

- In dB scale Av = 20log(1.8) = 5.105dB.

### <ins> 5.34 AC Analysis
(Follow the same procedure as mentioned in circuit 1)

![ckt3_4acan](https://github.com/user-attachments/assets/4966a650-9516-4819-a38e-84a73da6642d)

From the frequency response graph, we observe the gain in dB scale is 5.141dB and the dB cutoff frequency (bandwidth) is 17.11GHz.

| Gain | Theoretical value | Practical value |
|------|--------|------|
| Av(V/V) | 4.77 | 1.8 |
| Av(dB) | 5.105 | 5.141 |   

### 7. COMPARISON OF DIFFERENT CIRCUITS

| Feature | Circuit 1: Resistor Tail | Circuit 2: Ideal current source | Circuit 3: Active NMOS source |      
|--------|--------|----|-----|     
| Gain | 12.128dB | 12.131dB | 16.4158dB |      
| CMRR | Low | Moderate | High |      
| Power Efficiency | Low | Moderate | High |     
| Stability | Poor(supply dependent) | Better | Best |     
| Practical Implementation | Simple | Theoretical | Most practical |      
| Noise Immunity | Low | Moderate | High |

### 8. INFERENCE AND ANALYSIS OF MOS DIFFERENTIAL AMPLIFIER     
### 1. Importance of Replacing Tail Resistor(Rss) with a Current Source
- Larger Rss reduces gain, the transistors find it difficult to amplify small signals.
- A constant current source ensures a stable tail current which improves gain and circuit performance.
-  Even though there is current variations, the current source provides a stable output.
-  A current source improves **common-mode rejection ratio(CMRR)** by stabilizing the tail current.

### 2. Input Common-Mode Voltage(Vicm)
- Vicm must be within a specific range to keep transistors in ON state.
- As we increase the amplitude, we can observe early distortion as the MOSFET enters saturation or cutoff faster.
- **Maximum input swing** is the maximum voltage before distortion begins.

### 3. Effects of Signal Amplitude and Distortion
- At **50mV** input, the circuit remains linear.
- At **100mV** input, the circuit becomes non-linear and limits amplification.
- Higher amplitude causes early saturation or cutoff, reducing the operational range.

### 4. Threshold Voltage(Vth) and W/L Ratio Adjustments
- It is important to set the W/L ratio properly in order to get correct Vout and gain.
- Vout is not directly dependent on circuit parameters, so it is difficult to make variations.

### 5. AC Analysis and Phase Shift Effect 
- In order to achieve a significantly higher gain we need to set the AC phase of one of the input voltage to 180deg.
- Because differential signals with opposite phase improve gain and stability.

### 9. CIRCUIT-SPECIFIC OBSERVATIONS  
### Circuit 1: Resistor-Based Source
- It is a simple circuit, but it cannot handle variations in supply voltage.
- Tail current is not stable which leads to fluctuations in gain.
- Lower gain compared to other current source circuits

### Circuit 2: Ideal current Source
- Best used in theoretical analysis but not practical.
- It provides a constant tail current but cannot be used in real circuits.

### Circuit 3: Active Current Source(NMOS)
- Instead of resistor if we use a active current source NMOS, we can achieve a stable tail current.
- Improves common-mode rejection ratio(CMRR).
- Provides Higher gain and stability compared to circuit 1.












