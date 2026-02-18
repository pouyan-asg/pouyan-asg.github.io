---
layout: page
title: Series-Parallel Auto-Regulated Rectifier circuit
description: Simulation of an LED Driver in MATLAB Simulink
img: assets/img/projects/led1.png
importance: 6
category: ""
date: 2015-06-29
---

### Summary

This project focuses on the development and simulation of a series-parallel auto-regulated rectifier circuit designed to power multiple LED strings at the output. By combining this rectifier topology with a multi-winding transformer, the circuit enables precise current sharing among LED strings, even when they operate at different voltage levels. This approach increases circuit flexibility and expands its potential applications.

The work was conducted as a simulation-based study in **MATLAB Simulink** as part of a course during my Master’s degree.

### Introduction

Lighting accounts for about 25% of global electrical energy consumption, driving a focus on energy-saving lighting innovations. Light Emitting Diodes (LEDs) possess desirable characteristics for "green energy" lighting, such as high efficiency, energy conservation, no pollution, and closeness to natural light. LEDs are fundamentally diodes that emit light when current passes through their p-n junction. Key advantages of LEDs over incandescent and fluorescent lamps include higher efficiency, more focused light intensity, greater versatility, high reliability, a very long useful life (30,000 to 50,000 hours), and the absence of harmful UV and IR radiation.567

LEDs require a DC voltage, typically 2-4 volts for a single LED, and their light output is proportional to the applied current. High-power or multiple-string LED applications require an LED driver to convert AC input power to the required low-voltage DC with regulated current. Drivers are essential for protecting LEDs from voltage fluctuations which can affect current and reduce lifespan. They can be constant voltage (e.g., 10V, 12V, 24V) or, preferably, constant current (e.g., 350mA, 700mA).

### Key Features and Principles

- LED Strings: Each output string is composed of multiple LEDs connected in series, and these strings are connected in parallel.
- LED Driver Requirement: LEDs require a DC voltage for operation, and the emitted light is proportional to the applied current. A driver is needed to convert the AC input power to the required low DC voltage and regulated current.
- Proposed Circuit: The circuit uses a multi-winding transformer with three secondary windings (*N_S1*, *N_S2*, *N_S3*) of equal turns and three blocking capacitors (*C_B1*, *C_B2*, *C_B3*) connected in series with the secondary windings.
Current Balancing: The core mechanism for current balancing relies on the charge-discharge principle of the blocking capacitors. The average current of the different LED strings is shown to be similar and equal, even with varying output voltages.
- Output Current: Based on theoretical analysis and simulation, the expected output current for each LED string is approximately 350 mA. The simulated output voltages for the four strings were V_O1 = 120V, V_O2 = 105V, V_O3 = 80V, and V_O4 = 65V.
- Fault Tolerance: In the event of an open circuit in one LED string, the protection circuit will bypass the fault, and the remaining strings will return to their normal operating current.
- Advantages: The design is structurally simple and low-loss due to the absence of additional independent magnetic elements. The theoretical and analytical results are consistent with the practical results.

### Modeling

After an introductory explanation of the presented model, the context is now prepared for describing and elaborating on the simulation results and relationships. It is worth noting that the simulations were performed using MATLAB software, version 7.12.0. Figure (1) shows our rectifier circuit with four outputs.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led1.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The outputs are strings (rows) of LEDs, but they are shown as a single LED in the circuit schematic. The input is an alternating current (AC) voltage source, which is essentially the utility power. The main circuit is the DC and switching source. The source enters the primary of a transformer and induces voltage in its secondary. The transformer secondary has three windings, labeled *Ns1*, *Ns2*, and *Ns3*, where *Ns1* = *Ns2* = *Ns3*. Three capacitors are connected in series with the transformer secondary windings, known as blocking capacitors.

We have applied assumptions to the circuit to simplify the analysis without affecting the results. It is assumed that the input source current (*i_p*) is a perfect sinusoidal source. Also, since the output capacitors are sufficiently large, *Vo1*, *Vo2*, *Vo3*, *Vo4* can be considered as voltage sources used to drive the LED strings. The capacitance of the blocking capacitors (*CB1*, *CB2*, *CB3*) has also been chosen to be large, and it is assumed that the voltage across them remains constant during each switching cycle (of the main circuit). Thus, it can be assumed that the blocking capacitors *CB1*, *CB2*, and *CB3* act like voltage sources *VCB1*, *VCB2*, and *VCB3*. Furthermore, the forward voltage drop of the diodes is negligible.

The simulated circuit is shown in Figure below. To avoid unintentional and visual errors, the outputs of each parameter and circuit elements are drawn in different, harmonized colors. The simulation was performed in the discrete mode with a sample time of one microsecond (*10^-6*). It is notable that the connection method of the transformer secondary has been observed. In MATLAB software and among the Simpower Systems elements, an LED element does not exist. For this reason, to prevent modeling disruption, the LED was replaced with a regular diode, and similar results were obtained. Here, the diodes also represent the LED strings. The most important output parameters are DC voltage and low ripple in the output voltage and current.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led2.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="80%" %}
    </div>
</div>
<div class="caption">
   Simulation in Simulink.
</div>

Based on each time interval, three general circuit states can be considered, as shown in Figure below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led3.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
    </div>
</div>

### Results

This section is dedicated to simulation results. The value of the output capacitors *C1*, *C2*, *C3*, and *C4* is 47 mu F, and the blocking capacitors *CB1*, *CB2*, and *CB3* are 1 mu F. Diodes *D1* to *D10* have a forward turn-on voltage of 0.8 Volts, an internal resistance of 1 mOmega, an internal inductance of zero Henry, and a Snubber circuit with 500 Omega resistance and 250 nF capacitance.

The output diodes, which represent the LED strings, have similar characteristics to diodes *D1* to *D10*. However, since different voltages are required at the output due to the number of LEDs, different forward turn-on voltages were considered for them. We set the forward voltage for Diode 1 to 120 Volts, for Diode 2 to 105 Volts, for Diode 3 to 80 Volts, and finally, for Diode 4 to 65 Volts. These values correspond to *Vo* values: *Vo1*=120V, *Vo2*=105V, *Vo3*=80V, and *Vo4*=65V.

The transformer has one primary and three secondary windings. The most important parameters of this transformer are as follows: It has no taps, and its nominal frequency is equal to the grid frequency, 50 Hz. According to the real values, the transformer primary has 33 turns, and the secondary windings have 13 turns. However, because we applied assumptions in the simulation circuit, the output current with the mentioned secondary turns will not be accurate or correct. If we consider 43 turns for the secondary windings, we reach the accurate current value in both theory and simulation. The winding resistance is 5 p.u., and the leakage inductance is 0.02 p.u.. The magnetic reluctance (*R_m*) is 50, and the magnetic inductance (*L_m*) is 100 p.u.

The input voltage source is an ideal sinusoidal source. The input voltage is 565.685 Volts, which represents the peak voltage. The effective value (RMS) of the input voltage is 400 Volts (the actual DC value). The input frequency is 50Hz, which is the grid frequency.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led4.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="75%" %}
    </div>
</div>
<div class="caption">
    Transformer primary and secondary voltages.
</div>

Based on the actual results, with an effective input of 400 Volts, the outputs will be between 70-140V and 350mA. The maximum output difference reaches 70 Volts. Figure 7 shows the primary and secondary voltages of the transformer. As shown in the figure and according to calculations, the maximum input value is 565.685 Volts. The outputs will be V_1=V_2=V_3 = 43 x 565.685/33 = 737.1 based on the transformer ratio *V_1*/*V_2* = *N_1*/N_2*.

<div class="row">
  <div class="col-md-6">
    {% include figure.html path="assets/img/projects/led5.png" title="Image 1" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
  </div>
  <div class="col-md-6">
    {% include figure.html path="assets/img/projects/led6.png" title="Image 2" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
  </div>
</div>
<div class="caption">
    Output voltages.
</div>

As expected, the output voltage should be DC to drive the LEDs. The output voltage has a very small ripple, which is negligible and will not affect the outputs or light intensity. As can be seen in Figures, the output voltage begins to increase until the first 0.1 seconds, after which it becomes DC at V_o values: V_o1=120V, V_o2=105V, V_o3=80V, and V_o4=65V, which is our expectation for driving the LED strings.

Based on the current output from the actual circuit, 350mA is expected. If we rely only on calculations, we will reach this value.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led7.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="75%" %}
    </div>
</div>
<div class="caption">
    Input current.
</div>

Figure below shows the output current, which is close to 350 mA. Note the pulsed nature of the output current, which overall creates a low-ripple DC shape at the output. Also, note that the outputs turn on in order of DC voltage, and the currents turn on earlier the lower the forward voltage is.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/led8.png" title="led driver" class="img-fluid rounded z-depth-1 mx-auto d-block" width="75%" %}
    </div>
</div>
<div class="caption">
    Output current.
</div>

Finally, two curves are displayed: One shows the efficiency based on different output powers P_o, and the other shows the efficiency based on different output voltages V_o. To avoid long and strenuous calculations, we only display the final curves. 

<div class="row">
  <div class="col-md-6">
    {% include figure.html path="assets/img/projects/led9.png" title="Image 1" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
  </div>
  <div class="col-md-6">
    {% include figure.html path="assets/img/projects/led10.png" title="Image 2" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
  </div>
</div>

### References

[1] X. Wu and Chen Hu and J. Zhang and Chen Zhao, “Series-Parallel Auto regulated
Charge-Balancing Rectifier for Multioutput Light-Emitting Diode Driver,” August 2013
IEEE.

[2] S. M. Baddela and D. S. Zinger, “Parallel connected LEDs operated at high
frequency to improve current sharing,” in Conf. Rec. 39th IEEE IAS Annu. Meeting, Oct.
2004, vol. 3, pp. 1677–1681.

[3] W. Thomas and J. Pforr, “A novel low-cost current-sharing method for automotive
LED-lighting systems,” in Proc. 13th EPE, 2009, pp. 1–10.

[4] K. I Hwu and S. C Chou, “A simple current-balancing converter for LED lighting,” in
Proc. IEEE Appl. Power Electron. Conf., 2009,pp. 587–590.

[5] Z. Wang, X. Wu, M. Chen, and J. Zhang, “Optimal design methodology for the
current-sharing transformer in a quasi-resonant (QR) flyback LED driver,” in Proc. 27th
Annu. IEEE APEC, Feb. 2012,pp. 2372–2378.

<!-- [6] S. Choi and T. Kim, “Symmetric current-balancing circuit for LED backlight with
dimming,” IEEE Trans. Ind. Electron., vol. 59, no. 4, pp. 1698–1707, Apr. 2012.

[7] X. Wu, J. Zhang, and Z. Qian, “A simple two-channel LED driver with automatic
precise current sharing,” IEEE Trans. Ind. Electron., vol. 58, no. 10, pp. 4783–4788,
Oct. 2011.

[8] S. Zhang, Q. Chen, J. Sun, M. Xu, and Y. Qiu, “High-accuracy passive current
balancing schemes for large-scale LED backlight system,” in Proc. 26th Annu. IEEE
APEC, 2011, pp. 723–727.

[9] J. Zhang, L. Xu, X.Wu, and Z. Qian, “A precise passive current balancing method for
multi-output LED drivers,” IEEE Trans. Power Electron., vol. 26, no. 8, pp. 2149–2159,
Aug. 2011.

[13] J. Zhang, J. Wang, and X. Wu, “A capacitor-isolated LED driver with inherent
current balance capability,” IEEE Trans. Ind. Electron., vol. 59, no. 4, pp. 1708–1716,
Apr. 2012.

[11] C. Chen, C. Wu, Y. Chen, and T. Wu, “Sequential color LED backlight driving
system for LCD panels,” IEEE Trans. Power Electron., vol. 22, no. 3, pp. 919–925, May
2007.

[12] W. Chen and S. Y. R Hui, “A dimmable light-emitting diode (LED) driver with mag-
amp post-regulators for multistring applications,” IEEE Trans. Power Electron., vol. 26,
no. 6, pp. 1714–1722, Jun. 2011.

[13] H. Chiu, Y. Lo, J. Chen, S. Cheng, C. Lin, and S. Mou, “A high-efficiency dimmable
LED driver for low-power lig.

[14] Q. C. Hu and Z. Rane, “LED driver circuit with series-input-connected converter
cells operating in continuous conduction mode,” IEEE Trans. Power Electron., vol. 25,
no. 3, pp. 574–582, Mar. 2010.

[15] W. Yu, J.-S. Lai, H. Ma, and C. Zheng, “High-efficiency dc–dc converter with twin
bus for dimmable LED lighting,” IEEE Trans. Power Electron., vol. 26, no. 8, pp. 2095–
2100, Aug. 2011.

[16] Y. Hu and M. M. Jovanovic, “A new current-balancing method for paralleled LED
strings,” in Proc. 26th Annu. IEEE APEC, Mar. 2011,pp. 705–712.

[17] H. Chiu and S. Cheng, “LED backlight driving system for large-scale LCD panels,”
IEEE Trans. Ind. Electron., vol. 54, no. 5, pp. 2751–2760, Oct. 2007.

[18] S. K. Ng, K. H. Loo, S. K. Ip, Y. M. Lai, C. K. Tse, and K. T. Mok, “Sequential variable
bilevel driving approach suitable for use in highcolor-precision LED display panels,”
IEEE Trans. Ind. Electron., vol. 59,no. 12, pp. 4637–4645, Dec. 2012.

[19] S. Li, W. W. X. Zhong, W. Chen, and S. Y. R. Hui, “Novel selfconfigurable current-
mirror techniques for reducing current imbalance in parallel light-emitting diode (LED)
strings,” IEEE Trans. Power Electron.,vol. 27, no. 4, pp. 2153–2162, Apr. 2012.

[20] H. Chen, Y. Zhang, and D. Ma, “A SIMO parallel-string driver IC for dimmable LED
backlighting with local bus voltage optimization and single time-shared regulation
loop,” IEEE Trans. Power Electron., vol. 27, no. 1, pp. 452–462, Jan. 2012.

[21] S. H. Cho, S.-H. Lee, S. S Hong, D. S Oh, and S. K Han, “High-accuracy and cost-
effective current-balanced multichannel LED backlight driver using -->