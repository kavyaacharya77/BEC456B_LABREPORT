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

### Key Features of Current Mirror Circuit
| Feature | Description |
|---|---|
| Stable Current Copying | Ensures that the output current remains identical to the reference current. |
| Independent of load variations | Output current remains constant despite changes in the load. |
| Used in analog ICs | Commonly found in amplifiers, differential pairs and operational amplifier biasing. |
| MOSFET-based design | Uses matches MOSFETs to mirror the reference current. |
| Scalability | Allows multiple copies of the same reference current. |    

### Basic Operation 
A current mirror circuit consists of two or more matched transistors. If two MOSFETs have the same *gate-source voltage(Vgs)* and are operating in the saturation region, they should conduct same drain current.   

For MOSFETs operating in saturation, the drain current is given by:   

$Id$ = $0.5unCox(W/L)(Vgs-Vth)^2$

Where:
- $un$ = Electron mobility
- $Cox$ = Gate oxide capacitance per unit area
- $(W/L)$ = Width to length ratio of the MOSFET
- $Vgs$ = Gate-to-source voltage
- $Vth$ = Threshold voltage




