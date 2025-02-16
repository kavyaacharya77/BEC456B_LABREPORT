# LTSpice simulation of a CMOS circuit #1
### 1. INTRODUCTION
 In this experiment, a CMOS-based circuit is simulated using LTSpice to analyze its DC operating point, transient response, and AC characteristics. The circuit consists of a MOSFET, resistor and a volage source. The DC analysis helps to determine the biasing conditions, the transient analysis observe the circuit's time-domain response and the AC analysis evaluates its frequency-dependent behaviour. This simulation provides insight into the circuits's functionality, whether it acts as an amplifier, swtich or filter.    

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
 ### <ins>4.1 DC operating point analysis</ins>
 In this simulation , a DC supply volatge(VDD) of 1.8V is given and 1kohm resistor is used. Here as the power rating is 100mW ,we have considered drain current(Id) as 55uA (from the equation P = VDD*I) by setting length(L) as 180nm and width(W) as 203nm. The gate terminal of the MOSFET is biased at 0.9V DC, while the source terminal is grounded(0V). The drain volatge(Vd) is determined by the circuit components and the MOSFETS's characteristics. Since the threshold voltage (Vth) is 0.37V , the applied Vgs = 0.9V ensures that the MOSFET is turned ON.               
 
 After running the .op simulation , the DC volatges at key nodes are observed. The MOSFET's drain current(Id) and the volatge drop across R1 are also obtained. Based on these values, we determine whether the MOSFET operates in Saturation(for amplification), Triode( for switching) or Cutoff( if OFF). If the drain volatge is significantly lower than VDD, the MOSFET is conducting and likely in saturation mode, which essential for amplification purposes.

 ### <ins>4.2 Transient response</ins> 
 An AC signal is apllied to the circuit using sine wave input volatge source parameters:   
 
 - Amplitude: 50mV(peak)
 - Frequency: 1kHz
 - DC offset: 0.9V
The simulation runs for 3 milliseconds(.trans 3m), capturing multiple cycles of the input waveform. The output waveform is observed at the drain of the MOSFET. If there's a phase shift than the circuit is functioning as an amplifier.

### <ins>4.3 AC analysis</ins>
An AC signal sweep is applied to the circuit over a wide range of frequencies, from 0.1 Hz to 1T Hz, using a logarithmic scale. The AC input is a small signal sine wave, and the gain is measured as the ratio of output voltage to input voltage in decibels. The simulation uses the following command:    
(.ac dec 20 0.1 1T)  

Here,
- dec 20: Takes 20 data points per decade for a smooth response curve.
- 0.1 Hz to 1T Hz: Defines the frequency sweep range.

### 5. OBSERVATION
### <ins>5.1 DC operation point analysis</ins>    
![simdc_op](https://github.com/user-attachments/assets/dbb5e6d9-492b-4f27-b6a0-66575ea7bcc6)   
- Gate Voltage(Vg): 0.9V
- Source Voltage(Vs): 0V
- Drain Voltage or Vout: 1.74445V
- Drain current: 55uA
  
This confirms that the MOSFET is in the saturation region, which is necessary for proper amplification.

### <ins>5.2 Transient analysis</ins>
![transient_analysis](https://github.com/user-attachments/assets/593131db-addb-4908-b0e1-acb3bb5df2d7)    
- Input signal charcteristics: A 1kHz sine wave and 50mV peak amplitude and 0.9V DC offset was applied.
- Observed Output voltage(Vout): The output peak voltage was measured as 1.74445V, indicating a successful amplification.
- Waveform integrity: The amplified signal retainsits shape without significant distortion, confirming proper circuit operation.

### <ins>5.3 AC analysis</ins>       
![ac_analysis](https://github.com/user-attachments/assets/abca7e64-b1b7-433d-bfde-f3e8f029c4ba)
- Voltage Gain: The circuit shows a gain of 30.85dB, which corresponds to a linear gain of 34.89. This indicates significant amplification of the input signal.
- Output peak voltage: The measured output voltage is 1.74445V, which aligns with the expected amplification based on the gain.
- Phase shift: At 1k Hz, the output waveform lags the input by approximately 120 degree, as calculated from the transient response graph. This suggests a frequency-dependent phase delay.

### 6. INFERENCE 
The LTSpice simulation of the CMOS circuit provides insights into its operational behaviour in different domains:    
- DC operating point analysis cofirmed that the MOSFET operates in saturation region. The observed drain voltage (1.74445V) and the drain current(55uA) align with theoretical values.
- Transient analysis verified that the circuit amplifies the input 1k Hz sine wave with minimal distortion. The output peak voltage of 1.74445V suggests successful signal amplification. A phase shift in output indicates that the circuit introduces delay, which is typical in amplifiers.
- AC analysis showed a voltage gain of 30.85dB indicating strong signal amplification. The phase shift of ~120 degree at 1k Hz suggests that the frequency-dependent behaviour must be considered for applications requiring precise phase allignment.

### 7. CONCLUSION
The CMOS circuit simulated in LTSpice functions as an amplifier, operating in the saturation region with stable gain, pjase shift amd transient response. The observed voltage gain and output characteristics validate its use in low-power amplification applications. Further analysis, such as determining cutoff frequency and bandwidth, will help optimize the circuit for specific design requirements.





 

 
