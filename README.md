# LTSpice simulation of a CMOS circuit 
### 1. INTRODUCTION
 In this experiment, a CMOS-based circuit is simulated using LTSpice to analyze its DC operating point, transient response, and AC characteristics. The circuit consists of a MOSFET, resistor and a volage source. The DC analysis helps to determine the biasing conditions, the transient analysis observe the circuit's time-domain response and the AC analysis evaluates its frequency-dependent behaviour. This simulation provides insight into the circuits's functionality, whether it acts as an amplifier,swtich or filter.    

 ### 2. CIRCUIT DIAGRAM
 ![sim_ckt1](https://github.com/user-attachments/assets/73aa5b78-3681-47bb-9081-1c72c7b12502)     
 
 ### 3. COMPONENTS USED
 | Components | Value/Model | Purpose |
 |------------|-------------|---------|
 |MOSFET (M1) | CMOSN (TSMC 0.18um) | Main active element |
 | Resistor (R1) | 1kohm | Load Resistance |
 | Voltage source (V1) | 1.8V | Supply voltage |
 | Voltage source (V2) | SINE(0.9 50m 1k) | AC input signal(1kHz, 50mV AC + 0.9V DC) |
 | MOSFET model library | .lib "D:\Documents\tsmc018.lib" | Defines MOSFET characteristics |    

 ### 4. SIMULATION PROCEDURE
 ### <ins>DC operating point analysis</ins>
 In this simulation , a DC supply volatge(VDD) of 1.8V is given and 1kohm resistor is used. Here as the power rating is 100mW ,we have considered drain current(Id) as 55uA (from the equation P = VDD*I) by setting length(L) as 180nm and width(W) as 203nm. The gate terminal of the MOSFET is biased at 0.9V DC, while the source terminal is grounded(0V). The drain volatge(Vd) is determined by the circuit components and the MOSFETS's characteristics. Since the threshold voltage (Vth) is 0.37V , the applied Vgs = 0.9V ensures that the MOSFET is turned ON.               
 
 After running the .op simulation , the DC volatges at key nodes are observed. The MOSFET's drain current(Id) and the volatge drop across R1 are also obtained. Based on these values, we determine whether the MOSFET operates in Saturation(for amplification), Triode( for switching) or Cutoff( if OFF). If the drain volatge is significantly lower than VDD, the MOSFET is conducting and likely in saturation mode, which essential for amplification purposes.

 ### <ins>Transient response</ins> 
 An AC signal is apllied to the circuit using sine wave input volatge source parameters:   
 
 - Amplitude: 50mV(peak)
 - Frequency: 1kHz
 - DC offset: 0.9V
The simulation runs for 3 milliseconds(.trans 3m), capturing multiple cycles of the input waveform. The output waveform is observed at the drain of the MOSFET. If there's a phase shift of 180 degree than the circuit is functioning as an amplifier.

### <ins>AC analysis</ins>
An AC signal sweep is applied to the circuit over a wide range of frequencies, from 0.1 Hz to 1T Hz, using a logarithmic scale. The AC input is a small signal sine wave, and the gain is measured as the ratio of output voltage to input voltage in decibels. The simulation uses the following command:    
(.ac dec 20 0.1 1T)  

Here,
- dec 20: Takes 20 data points per decade for a smooth response curve.
- 0.1 Hz to 1T Hz: Defines the frequency sweep range.





 

 
