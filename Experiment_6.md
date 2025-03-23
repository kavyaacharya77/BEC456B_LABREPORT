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

### 4.1 CIRCUIT DESIGN AND CALCULATIONS
### Circuit A: 
### Case 1: For mirror ratio 1:1
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

In order to get the correct current value , W/L for M1 and M2 is 10um/180nm and W/L for M3 is 32.4256um/180nm. And we have set the bias voltage(V2) as 0.566V.

![ckt6_Aoppnt](https://github.com/user-attachments/assets/8e23114f-3a12-4fde-af9f-a1b4590fe992)

5. Next select **view** > **command goto** > **SPICE error log** option to check the Vgs, Vth, Vds etc.

![ckt6_Aspiceerror](https://github.com/user-attachments/assets/270b4b9c-9d4a-4025-a4e4-241b7e954ae9)

From the above image we check whether the MOSFET operates in saturation region.

### 5.21 <ins> Transient Analysis
Transient analysis examines how the circuit responds over time by applying a time-varying input. It helps observe the dynamic behaviour of the current mirror, including startup transients and settling time.

### <ins> Procedure </ins>   
1. Apply a sinusoidal input ac signal.
2. Go to **simulate** > **Edit Simulation Cmd** > **Transient**. Choose a suitable time step let's say 3m.
3. Run the transient analysis and observe the input and output waveforms, the phase shift between the input and output and calculate the gain.

### INPUT AND OUTPUT WAVEFORMS

![Screenshot 2025-03-23 125308](https://github.com/user-attachments/assets/2a79a44c-bee0-421c-ad96-90b0d4a859d3)

![Screenshot 2025-03-23 125237](https://github.com/user-attachments/assets/81eff22f-bb13-4281-9236-303eb39bf2a3)

- The expected gain of the circuit is 10V/V.
- The obtained gain from transient analysis is Av = 14.78V/V

### 5.31 <ins> AC Analysis 
AC analysis determines the frequency response of the current mirror, helping analyse its small-signal behaviour and gain characteristics over a range of frequencies.

### <ins> Procedure </ins>   
1. Apply a small AC signal at the input.
2. Set AC amplitude to 1V in the input voltage source properties.
3.  Go to **simulate** > **Edit Simulation Cmd** > **AC Analysis**. Select decade sweep with the frequency range of 0.1Hz to 1THz.
4.  Run the simualation and observe the Gain(Vout/Vin) vs. frequency plot, Phase shift vs.frequency and 3dB cutoff frequency (bandwidth).

![ckt6_A11ACanal](https://github.com/user-attachments/assets/a12fe97b-fd38-4243-a09c-c322cef93a68)

- Gain Av = 29.02dB.
- -3dB bandwidth frequency = 652.698M Hz.

| Gain | Theoretical Value | Practical Value |
|---|----|---|
| Av (V/V) | 10 | 14.78 |
| Av (dB) | 20 | 29.02 |    

### For length (L) = 500nm
### <ins> DC Analysis
Here let the length of all these MOSFETs be 500nm. Width of M3 be 67.646um.

![Screenshot 2025-03-23 144736](https://github.com/user-attachments/assets/8ad46a11-e25c-4e5e-b106-023e13dcb838)
 
### <ins> AC Analysis

![Screenshot 2025-03-23 150738](https://github.com/user-attachments/assets/f9ba8551-07d6-4ead-9b18-99e9518910cd)

- Gain Av (in dB) = 37.962dB.
- -3dB bandwith frequency = 116.66M Hz.

### For length (L) = 1um
### <ins> DC Analysis
Here let the length of all these MOSFETs be 1um. Width of M3 be 96.472um.

![Screenshot 2025-03-23 145328](https://github.com/user-attachments/assets/72b1b842-2661-474f-965d-273d77a27ff2)

### <ins> AC Analysis

![Screenshot 2025-03-23 150119](https://github.com/user-attachments/assets/26a8fbe2-43ad-498f-82d3-f78c36b670c7)

- Gain Av (in dB) = 37.188dB.
- -3dB bandwith frequency = 78.40M Hz.

### Comparison Table

| Length (L) | Width (W1) | Width (W2) | Width (W3) | Iref | Iout | Vout |
|-----|----|----|----|----|----|-----|
| 180nm | 10um | 10um | 32.4256um | 0.278mA | 0.278mA | 1.00553V |
| 500nm | 10um | 10um | 67.646um | 0.278mA | 0.2776mA | 0.707924V |
| 1um | 10um | 10um | 96.472um | 0.278mA | 0.278mA | 0.337052V |

### Case 2: For mirror ratio 1:2
![Screenshot 2025-03-23 143634](https://github.com/user-attachments/assets/0842279b-3ac5-4bad-b843-e8ef57a5d728)

### <ins> DC Analysis 
While keeping length of M1 and M2 MOSFET as 180nm, set the width of M1 as 10um and M2 as 20um. And Width W of MOSFET M3 is set as 42.833um. Here the current (Id) in the MOSFET M2 must be double of Iref. 

1. Determine the drain current (Id)

   Id = $P/Vdd$ = $1m/1.8$ = 0.556mA

2. Determine the reference current (Iref) for 1:2 ratio

   Iref = $Id/3$ = $0.556m/3$ = 0.185mA

3.  current Id(M2) = $Iref/2$ = 0.37mA

![Screenshot 2025-03-23 132946](https://github.com/user-attachments/assets/11d7dcfb-9b36-454c-a8d5-3c987692489c)

### <ins> Transient Analysis

### INPUT AND OUTPUT WAVEFORMS

![Screenshot 2025-03-23 135327](https://github.com/user-attachments/assets/f7a74cf3-e410-4769-a381-8f42396b3b28)

![Screenshot 2025-03-23 135527](https://github.com/user-attachments/assets/a8a8a5f4-23f9-42c7-9b6f-8d15505d4847)

- The obtained gain from transient analysis is Av = 25.79V/V.

### <ins> AC Analysis

![Screenshot 2025-03-23 140507](https://github.com/user-attachments/assets/b14a05d8-7995-4303-ae47-9ea53990f8a4)

- Gain Av = 29.25dB.
- -3dB bandwidth frequency = 431.475M Hz.

### For length (L) = 500nm
### <ins> DC Analysis
Here let the length of all these MOSFETs be 500nm. Width of M3 be 89.342um.

![Screenshot 2025-03-23 141822](https://github.com/user-attachments/assets/b285bff2-07ab-45fe-b44a-b93caa309d33)

### <ins> AC Analysis

![Screenshot 2025-03-23 151040](https://github.com/user-attachments/assets/ba75d1bd-94e9-459a-88fa-254bd690e0cb)

- Gain Av (in dB) = 38.027dB.
- -3dB bandwith frequency = 94.07M Hz.

### For length (L) = 1um
### <ins> DC Analysis
Here let the length of all these MOSFETs be 1um. Width of M3 be 126.357um.

![Screenshot 2025-03-23 142637](https://github.com/user-attachments/assets/0655812b-7322-43bc-8177-7cddbb6ffb9b)

### <ins> AC Analysis

![Screenshot 2025-03-23 151331](https://github.com/user-attachments/assets/647bb416-558a-4869-872b-e00a0cd5b808)

- Gain Av (in dB) = 39.553dB.
- -3dB bandwith frequency = 52.6977M Hz.

### Comparison Table

| Length (L) | Width (W1) | Width (W2) | Width (W3) | Iref | Iout | Vout |
|-----|----|----|----|----|----|-----|
| 180nm | 10um | 20um | 42.833um | 0.185mA | 0.370666mA | 1.03657V |
| 500nm | 10um | 20um | 89.342um | 0.185mA | 0.37066mA | 0.802448V |
| 1um | 10um | 20um | 126.357um | 0.185mA | 0.3706mA | 0.493025V |

### Case 3: For mirror ratio 2:1
![Screenshot 2025-03-23 202746](https://github.com/user-attachments/assets/a3577ac5-cfc7-45e5-8e20-f931db99f605)

### <ins> DC Analysis 
While keeping length of M1 and M2 MOSFET as 180nm, set the width of M1 as 20um and M2 as 10um. And Width W of MOSFET M3 is set as 20.75um. Here the current (Id) in the MOSFET M2 must be 1/2 times the Iref. 

#### <ins> Design Calculations </ins>
1. Determine the drain current (Id)

   Id = $P/Vdd$ = $1m/1.8$ = 0.556mA

2. Determine the reference current (Iref)

   Itotal = Id + 1/2Iref = 3/2Iref
   
   Iref = $2Id/3$ = $2*0.556m/3$ = 0.3706mA

![Screenshot 2025-03-23 205305](https://github.com/user-attachments/assets/97159ea4-0869-405d-adab-fb39c030b9fa)

### <ins> Transient Analysis

### INPUT AND OUTPUT WAVEFORMS

![Screenshot 2025-03-23 205614](https://github.com/user-attachments/assets/b2f1d6b9-0f1e-4bfe-be13-8754ba75b331)

- The obtained gain from transient analysis is Av = 25.641V/V.

### <ins> AC Analysis

![Screenshot 2025-03-23 210018](https://github.com/user-attachments/assets/5fdd4388-6bb4-45f7-a314-b35d7249a3cb)

- Gain Av = 28.98dB.
- -3dB bandwidth frequency = 641.98M Hz.

### For length (L) = 500nm
### <ins> DC Analysis
Here let the length of all these MOSFETs be 500nm. Width of M3 be 44.508um.

![Screenshot 2025-03-23 210549](https://github.com/user-attachments/assets/b88c866c-93a8-4991-a0ef-88c1ef599f44)

### <ins> AC Analysis

![Screenshot 2025-03-23 210827](https://github.com/user-attachments/assets/98e1cca8-d319-41d9-a732-7018970085ee)

- Gain Av (in dB) = 37.95dB.
- -3dB bandwith frequency = 116.66M Hz.

### For length (L) = 1um
### <ins> DC Analysis
Here let the length of all these MOSFETs be 1um. Width of M3 be 62.383um.

![Screenshot 2025-03-23 211433](https://github.com/user-attachments/assets/5177c925-d4c6-4e85-b92d-5a9450c95733)

### <ins> AC Analysis

![Screenshot 2025-03-23 211706](https://github.com/user-attachments/assets/d67012c4-e6c6-425e-9720-ee176e34cfdb)

- Gain Av (in dB) = 40dB.
- -3dB bandwith frequency = 59.17M Hz.

### Comparison Table

| Length (L) | Width (W1) | Width (W2) | Width (W3) | Iref | Iout | Vout |
|-----|----|----|----|----|----|-----|
| 180nm | 20um | 10um | 20.75um | 0.1854mA | 0.278mA | 1.0927V |
| 500nm | 20um | 10um | 44.508um | 0.1854mA | 0.2776mA | 0.828632V |
| 1um | 20um | 10um | 62.383um | 0.185mA | 0.278mA | 0.613212V |

### Case 4: For mirror ratio 1:3
![image](https://github.com/user-attachments/assets/29178065-fcab-4c85-89e0-9e86af486a31)

### <ins> DC Analysis 
While keeping length of M1 and M2 MOSFET as 180nm, set the width of M1 as 10um and M2 as 30um. And Width W of MOSFET M3 is set as 47.5885um. Here the current (Id) in the MOSFET M2 must be 3 times the Iref. 

#### <ins> Design Calculations </ins>
1. Determine the drain current (Id)

   Id = $P/Vdd$ = $1m/1.8$ = 0.556mA

2. Determine the reference current (Iref)

   Itotal = Id + 3Iref = 4Iref
   
   Iref = $Id/4$ = $0.556m/4$ = 0.139mA

![Screenshot 2025-03-23 212600](https://github.com/user-attachments/assets/cfd80bd2-6d1a-4d7e-913a-3807f556687e)

### <ins> Transient Analysis

### INPUT AND OUTPUT WAVEFORMS

![Screenshot 2025-03-23 212847](https://github.com/user-attachments/assets/486d8c6e-e983-4ff2-bbc4-5c964f2fe423)

- The obtained gain from transient analysis is Av = 16.688V/V.

### <ins> AC Analysis

![Screenshot 2025-03-23 213101](https://github.com/user-attachments/assets/91e7b3cf-64cb-44f0-b6bb-70d8210bc7ae)

- Gain Av = 29.16dB.
- -3dB bandwidth frequency = 315.02M Hz.

### For length (L) = 500nm
### <ins> DC Analysis
Here let the length of all these MOSFETs be 500nm. Width of M3 be 99.26um.

![Screenshot 2025-03-23 213419](https://github.com/user-attachments/assets/e37af6ba-0b8d-4f51-82b7-60ac6a7ab05a)

### <ins> AC Analysis


![Screenshot 2025-03-23 213704](https://github.com/user-attachments/assets/64744866-dd88-4d26-8eef-ea5dc35b8db0)

- Gain Av (in dB) = 37.811dB.
- -3dB bandwith frequency = 74.60M Hz.

### For length (L) = 1um
### <ins> DC Analysis
Here let the length of all these MOSFETs be 1um. Width of M3 be 139.553um.

![Screenshot 2025-03-23 214112](https://github.com/user-attachments/assets/f81dcb76-ee9c-4190-a8ea-a79df2f13873)

### <ins> AC Analysis

![Screenshot 2025-03-23 214357](https://github.com/user-attachments/assets/4ba12b76-8f19-4b7c-8303-039d51ded139)

- Gain Av (in dB) = 40.157dB.
- -3dB bandwith frequency = 39.77M Hz.

### Comparison Table

| Length (L) | Width (W1) | Width (W2) | Width (W3) | Iref | Iout | Vout |
|-----|----|----|----|----|----|-----|
| 180nm | 10um | 30um | 47.5885um | 0.139mA | 0.417mA | 1.07078V |
| 500nm | 10um | 30um | 99.26um | 0.139mA | 0.417mA | 0.913457V |
| 1um | 10um | 30um | 139.553um | 0.139mA | 0.4166mA | 0.694508V |

### 6. INFERENCE
- The current mirror circuit effectively replicates the reference current with minimal deviation, ensuring consistent performance across various W/L ratios.
- Even when the W/L ratio is scaled proportionally, the drain current (Id) remains stable, demonstrating the circuit's effectiveness.
- A slightly increase in amplifier gain was observed, which is likely due to small variations in transistor characteristics or simulation-related factors.
- As expected when the mirror ratio was adjusted from 1:1 to 1:2, the gain increased accordingly, confirming theoretical expectations.
- Overall, the results align well with theoretical predictions, indicating that both the simulation and circuit design function correctly under different conditions.

### 4.2 CIRCUIT DESIGN AND CALCULATIONS
### Circuit B: 
### Case 1: For mirror ratio 1:1
![Screenshot 2025-03-22 213539](https://github.com/user-attachments/assets/8a8def4b-4b4c-4547-9c10-34a563b384f6)

#### <ins> Design Calculations </ins>
1. Determine the drain current (Id)

   Id = $P/Vdd$ = $1m/1.8$ = 0.556mA

2. Determine the reference current (Iref)

   Iref = $Id/2$ = $0.556m/2$ = 0.278mA
