# Design and Analysis of Current Mirror Circuit
### 1. AIM    
### Design question A
Design and analyse the current mirror circuit for the following specifications.
- Av > -10V/V
- Vdd = 1.8V
- P <= 1mW

Perform the DC analysis, Transient analysis and AC analysis while maintaining (W/L) same for different values of Length(L). ALso find the maximum output swing and bandwidth.

### Design Question B
Design the differential amplifier using the same design specification as Experiment_3. 
- Vdd = 2.2V
- P <= 2.2mW
- Vicm = 1.2V
- Vocm = 1.25V
- Vp = 0.4V

Perform the DC analysis, transient analysis, AC analysis and extract the parameters.
### 2. COMPONENTS USED
The following components are used in the current mirror circuit along with their key specifications
| Components | Specification | Purpose |
|-----|-----|-----|
| MOSFETs(M1,M2) | CMOSP (TSMC 0.18um) | Acts as an active element in the differential amplifier |
| MOSFET(M3) | CMOSN (TSMC 0.18um) | Acts as an active element |
| DC Voltage source(V1) | 1.8V Stable power supply | Powers the amplifier circuit |
| AC Voltage Source(V2) | DC offset 0.566V, 1k Hz, 20mV amplitude | Provides the input AC signal for analysis |
| Current souce(Iref) | Stable and Precise reference current | Defines the reference current that gets mirrored |  

### 3. THEORY 
A current mirror circuit is designed to replicate a reference current(Iref) to one or more output branches while maintaining a stable current regardless of variations in the load.     

![image](https://github.com/user-attachments/assets/59fc7f4d-74b0-4257-aa40-af025154484a)

### Key Features of Current Mirror Circuit
| Feature | Description |
|---|---|
| Stable Current Copying | Ensures that the output current remains identical to the reference current. |
| Independent of load variations | Output current remains constant despite changes in the load. |
| Used in analog ICs | Commonly found in amplifiers, differential pairs and operational amplifier biasing. |
| MOSFET-based design | Uses matches MOSFETs to mirror the reference current. |
| Scalability | Allows multiple copies of the same reference current. |    

### Basic Operation 
A current mirror circuit consists of two or more matched transistors. If two MOSFETs have the same **gate-source voltage(Vgs)** and are operating in the saturation region, they should conduct same drain current.   

For MOSFETs operating in saturation, the drain current is given by:   

$Id$ = $0.5unCox(W/L)(Vgs-Vth)^2$

Where:
- $un$ = Electron mobility
- $Cox$ = Gate oxide capacitance per unit area
- $(W/L)$ = Width to length ratio of the MOSFET
- $Vgs$ = Gate-to-source voltage
- $Vth$ = Threshold voltage

By ensuring the identical MOSFETs with the same (W/L) ratio, the circuit achieves accurate current mirroring.

### Effect of Channel Length Modulation
In real-world circuits, the drain current of a MOSFET is affected by **channel length modulation**. As the **drain-to-source voltage(Vds)** increases, the drain current slightly increases, reducing the accuracy of the current mirror.

#### To counteract this affect:
- Use longer channel lengths to reduce modulation effects.
- Use cascode current mirrors for better output resistance and stability.
- Optimize MOSFET design for minimal variations.

This makes the current mirror circuit more reliable and precise in integrated curcuit applications.

### 4. CIRCUIT DESIGN AND CALCULATIONS
### Circuit A: 

![Screenshot 2025-03-22 213539](https://github.com/user-attachments/assets/8a8def4b-4b4c-4547-9c10-34a563b384f6)

#### <ins> Design Calculations </ins>
1. Determine the drain current (Id)

   Id = $P/Vdd$ = $1m/1.8$ = 0.556mA

2. Determine the reference current (Iref)

   Iref = $Id/2$ = $0.556m/2$ = 0.278mA

### 5. SIMULATION AND ANALYSIS 
### <ins> 5.11 DC Analysis
DC analysis ensures the current mirror operates in saturation, accurately copying the reference current. It helps determine steady-state conditions for stable circuit performance

### <ins> Procedure 
1. Set up the circuit in LTspice.
2.  Apply the supply voltage as 1.8V and bias voltage(V2) as 0.566V. Ensure that the current source is correctly defined.
3.  Run a DC operating point analysis
   - Go to **simulate** > **Edit simulation** >> **DC op pnt** > and select **.op**
4. Observe the key parameters like drain currents, output voltage etc. If the values doesn't match the design specifications, vary the widths of the MOSFETs(M1,M2,M3).

![ckt6_Aoppnt](https://github.com/user-attachments/assets/8e23114f-3a12-4fde-af9f-a1b4590fe992)

5. Next select **view** > **command goto** > **SPICE error log** option to check the Vgs, Vth, Vds etc.

![ckt6_Aspiceerror](https://github.com/user-attachments/assets/270b4b9c-9d4a-4025-a4e4-241b7e954ae9)

From the above image we check whether the MOSFET operates in saturation region.

### 5.21 Transient Analysis
Transient analysis examines how the circuit responds over time by applying a time-varying input. It helps observe the dynamic behaviour of the current mirror, including startup transients and settling time.

### <ins> Procedure </ins>   
1. Apply a sinusoidal input ac signal.
2. Go to **simulate** > **Edit Simulation Cmd** > **Transient**. Choose a suitable time step let's say 3m.
3. Run the transient analysis and observe the input and output waveforms, the phase shift between the input and output and calculate the gain.

### INPUT AND OUTPUT WAVEFORMS

### 5.31 AC Analysis 
AC analysis determines the frequency response of the current mirror, helping analyse its small-signal behaviour and gain characteristics over a range of frequencies.

### <ins> Procedure </ins>   
1. Apply a small AC signal at the input.
2. Set AC amplitude to 1V in the input voltage source properties.
3.  Go to **simulate** > **Edit Simulation Cmd** > **AC Analysis**. Select decade sweep with the frequency range of 0.1Hz to 1THz.
4.  Run the simualation and observe the Gain(Vout/Vin) vs. frequency plot, Phase shift vs.frequency and 3dB cutoff frequency (bandwidth).


