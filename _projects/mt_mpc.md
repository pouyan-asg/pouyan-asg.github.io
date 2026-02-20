---
layout: page
title: Model Predictive Control for Intelligent Operation 
description: Applying MPC Method for Robust Control of a DG System
img: assets/img/projects/mpc2.png
importance: 6
category: ""
date: 2016-09-29
---

### Summary

The increasing global trend toward Distributed Generation (DG) is motivated by the significant reduction in system costs and losses achieved by local energy production near the point of use. Among various DG technologies, microturbines (MTs) are highly valued for their reliable operation and inherent flexibility. Connecting microturbines to a larger system or local demands necessitates the use of intermediate electronic converters to regulate the output signal's amplitude and frequency. These converters fall primarily into two computational structures: AC-DC-AC and AC-AC configurations.

A key algorithmic challenge in microturbine operation is designing effective control mechanisms for these intermediate conversion stages. **Model Predictive Control (MPC)** stands out among conventional approaches as a robust and modern strategy for achieving precise system performance objectives. Applying MPC to microturbine generation systems represents a novel and efficient control strategy that significantly enhances operational flexibility and output management. 

The simulation results consistently demonstrate that the MPC algorithm improves system control characteristics beyond those achieved with traditional methods, showing superior adaptability across a wide range of operating conditions.

The following sections present selected research papers and their key results. Full-text access is available via [my website](https://www.pouyanasgharian.com/pub/), [ResearchGate](https://www.researchgate.net/profile/Pouyan-Asgharian), or [Google Scholar](https://scholar.google.com/citations?hl=en&user=XKebYqUAAAAJ).


#### 2016 - 1

This research addresses the critical challenge of controlling interface converters within Microturbine Generation (MTG) systems, particularly when operating in islanding (off-grid) mode. As DG becomes more prevalent, ensuring the reliability and quality of power from sources like microturbines is essential. The primary objective of this work was to develop a high-fidelity dynamic model of an MTG system and implement a more robust control strategy to overcome the limitations of traditional inverter control methods.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt1.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The methodology centers on the application of MPC to manage the current of a three-phase inverter connected to a Permanent Magnet Synchronous Generator (PMSG). By using a discrete-time model to predict future system behavior, the MPC algorithm minimizes a specific cost function—the error between reference and measured currents—to select optimal switching states for the inverter. This approach was simulated in MATLAB/Simulink using a detailed AC-DC-AC configuration that includes the turbine dynamics, fuel system control, and temperature governors.

The simulation results demonstrate that the MPC scheme provides exceptional dynamic performance, producing a high-quality sinusoidal output current with a Total Harmonic Distortion (THD) of approximately 2%, well within IEEE standards. Notably, the system achieves these results without the need for additional output filters, highlighting the efficiency and optimization potential of predictive control in modern power electronics.

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt2.png/" class="img-fluid rounded" alt="Image 1">
    <div class="caption">Rotor speed of the MTG.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt3.png" class="img-fluid rounded" alt="Image 2">
    <div class="caption">Fuel demand of the MTG.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt4.png/" class="img-fluid rounded" alt="Image 3">
    <div class="caption">Output Voltage of the PMSG.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt5.png" class="img-fluid rounded" alt="Image 4">
    <div class="caption">Voltage at DC side.</div>
  </div>
</div>

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt6.png/" class="img-fluid rounded" alt="">
    <div class="caption">Switching signals of the MPC.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt7.png" class="img-fluid rounded" alt="">
    <div class="caption">Load voltage without back-emf.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt8.png/" class="img-fluid rounded" alt="">
    <div class="caption">Load current.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt9.png" class="img-fluid rounded" alt="">
    <div class="caption">THD of output current.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2016.pdf) here.


#### 2016 - 2

This research presents a comprehensive dynamic model of a MTG system designed for high-performance operation in both grid-connected and islanding modes. The study introduces a novel configuration that incorporates a boost converter to stabilize and increase rectified voltage level, alongside a new Remover Ripple Circuit (RRC) filter topology to achieve a ripple-free output current without the need for complex control circuits or additional switches.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt10.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The methodology utilized MATLAB/Simulink to simulate the system's dynamic behavior under varied operational scenarios. This included a complex setup where the MTG unit simultaneously supplied a nonlinear load while maintaining a connection to a distribution network. The control strategies employed were tailored for each mode: a V-f control strategy for islanding to manage voltage magnitude and frequency, and a P-Q control strategy for grid-connected operation to ensure the delivery of desired active and reactive power.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt11.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="35%" %}
    </div>
</div>
<div class="caption">
    Proposed filter: (a) RRC structure (b) key waveforms for eliminating ripples.
</div>

Simulation results confirmed that the proposed architecture offers exceptional load-following performance, with the DC link voltage remaining constant even during significant load changes. The RRC filter demonstrated its effectiveness by delivering nearly sinusoidal output current and voltage with minimal harmonics and ripples in both operation modes.


<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt12.png/" class="img-fluid rounded" alt="">
    <div class="caption">Load output voltages: (a) grid-connected mode (b) isolated mode.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt13.png" class="img-fluid rounded" alt="">
    <div class="caption">Inverter output voltages: (a) grid-connected mode (b) isolated mode.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt14.png/" class="img-fluid rounded" alt="">
    <div class="caption">Voltage at DC side.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt16.png" class="img-fluid rounded" alt="">
    <div class="caption">Load output current: (a) grid-connected mode (b) isolated mode.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2016-.pdf) here.

#### 2019 - 1

This research addresses the critical need for flexible and highly reliable control strategies in MTG systems, specifically for hybrid operations where the system must transition from isolated to grid-connected states. While traditional methods rely on standard voltage-frequency and power-current controls, this paper proposes two distinct, advanced control architectures: a robust voltage-frequency-current controller for stand-alone mode and a novel power-voltage control strategy for grid-tied operation. The primary objective was to ensure the MTG could follow rapid load variations and maintain superior performance even when connected to weak distribution grids.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt17.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The methodology involved detailed dynamic modeling of a single-shaft MTG system—including the compressor, combustor, turbine, and a Permanent Magnet Synchronous Generator (PMSG)—within the MATLAB/Simulink environment. In the proposed grid-tied controller, the inner current loop typically found in traditional systems is replaced with a voltage loop, basing the control objectives entirely on power and voltage. This allows the inverter to effectively function as a controlled voltage source, enhancing its ability to support the grid.

<div class="row text-center">
  <div class="col-6">
    <img src="/assets/img/projects/mt18.png/" class="img-fluid rounded" alt="Image 1">
    <div class="caption">Inverter control in stand-alone mode.</div>
  </div>
  <div class="col-6">
    <img src="/assets/img/projects/mt19.png/" class="img-fluid rounded" alt="Image 2">
    <div class="caption">Power-voltage control method for grid-tied inverter.</div>
  </div>
</div>

Simulation results confirmed that the MTG demonstrates exceptional load-following performance and fast response times during hybrid transitions. Upon connecting to the utility grid at *t=10s*, the MTG successfully shared the demand, reducing its own fuel consumption and electromagnetic torque as the grid took over more than half of the active power load. Throughout the operation, three-phase voltages remained constant with low total THD, proving that these novel control strategies offer a more flexible and reliable solution for modern distributed generation applications.


<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt20.png/" class="img-fluid rounded" alt="">
    <div class="caption">Active power of MTG and grid.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt21.png" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase output voltages.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt22.png/" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase currents MTG-side.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt23.png" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase currents grid-side</div>
  </div>
</div>

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt24.png/" class="img-fluid rounded" alt="">
    <div class="caption">Fuel demand signal.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt25.png" class="img-fluid rounded" alt="">
    <div class="caption">MT output speed.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt26.png/" class="img-fluid rounded" alt="">
    <div class="caption">MTG electromagnetic torque.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt27.png" class="img-fluid rounded" alt="">
    <div class="caption">MTG output power.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2019.pdf) here.

#### 2019 - 2

This research addresses the challenge of maintaining power balance and reliability in isolated MTG systems, particularly when supplying sensitive loads that cannot tolerate voltage or frequency fluctuations. While microturbines are efficient and reliable distributed generation sources, their ability to respond to sudden load changes is limited. The primary objective of this work was to integrate a Battery Energy Storage (BES) system into the MTG architecture to act as a buffer, ensuring an uninterrupted and high-quality power supply even during significant demand variations.

<div class="row text-center">
  <div class="col-6">
    <img src="/assets/img/projects/mt28.png/" class="img-fluid rounded" alt="Image 1">
    <div class="caption">Control of three-phase inverter in isolated mode.</div>
  </div>
  <div class="col-6">
    <img src="/assets/img/projects/mt29.png/" class="img-fluid rounded" alt="Image 2">
    <div class="caption">The BES system control scheme.</div>
  </div>
</div>

The methodology introduces a novel control strategy for the BES based on the instantaneous monitoring of the DC-link voltage. By utilizing Hysteresis Current Control (HCC), the system automatically regulates the power exchange between a lithium-iron-phosphate battery pack and the microturbine. When the DC-link voltage deviates from predefined limits due to load spikes, the HCC system triggers the battery to discharge or charge, effectively suppressing transients. This setup was modeled and simulated in MATLAB/Simulink, featuring a single-shaft microturbine, a high-frequency permanent magnet generator, and a two-loop inverter control scheme to regulate the final AC output.

The simulation results demonstrate that the proposed hybrid system significantly improves power quality compared to standalone MTG units. The integration of the BES successfully stabilized the three-phase output at 400 V and 50 Hz, resolving the significant speed and voltage drops that typically occur when heavy loads are suddenly connected. The study concludes that this configuration is a highly promising solution for remote or emergency power applications, where high reliability and quick response times are essential for protecting sensitive equipment.

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt30.png/" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase output voltage without BES.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt31.png" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase output voltages with BES.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt32.png/" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase output currents without BES.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt33.png" class="img-fluid rounded" alt="">
    <div class="caption">Three-phase output currents with BES.</div>
  </div>
</div>

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt34.png/" class="img-fluid rounded" alt="">
    <div class="caption">Active power.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt35.png" class="img-fluid rounded" alt="">
    <div class="caption">DC-link voltage without BES.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt36.png/" class="img-fluid rounded" alt="">
    <div class="caption">DC-link voltage with BES</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt37.png" class="img-fluid rounded" alt="">
    <div class="caption">Output torque without BES.</div>
  </div>
</div>

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt38.png/" class="img-fluid rounded" alt="">
    <div class="caption">Output torque with BES.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt39.png" class="img-fluid rounded" alt="">
    <div class="caption">The BES power.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt40.png/" class="img-fluid rounded" alt="">
    <div class="caption">The BES current.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt41.png" class="img-fluid rounded" alt="">
    <div class="caption">The BES voltage.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2019-.pdf) here.

#### 2019 - 3

This research addresses the complexities of maintaining stable power quality in MTG systems when operated in stand-alone mode. Unlike grid-connected systems that benefit from the stability of a large utility network, stand-alone microgrids must independently regulate voltage and frequency while facing diverse and often challenging load types. The primary objective of this study was to implement MPC to manage the system's three-phase inverter, offering a more flexible and adaptive alternative to traditional Proportional-Integral (PI) control methods. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt42.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="60%" %}
    </div>
</div>

The methodology combines a high-fidelity dynamic model of a single-shaft microturbine with an advanced power electronics interface. A controlled rectifier is employed to maintain precise DC-link voltage regulation, while the MPC-based inverter uses a discrete-time predictive model to minimize a cost function based on the error between predicted and reference voltages. This architecture was rigorously tested in MATLAB/Simulink across four distinct scenarios involving constant, variable, non-linear, and unbalanced loads, ensuring that the control strategy was evaluated against the most demanding real-world conditions. 

The simulation results confirm that the proposed MPC strategy provides exceptional stability and a quick response to demand changes. Regardless of the load type, the system successfully maintained a steady 400 V, 50 Hz output with low harmonic distortion. By demonstrating the controller's ability to handle unbalanced and non-linear loads without affecting output quality, this work highlights MPC as a superior solution for industrial and domestic remote power applications where reliability and adaptability are paramount.


<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt43.png/" class="img-fluid rounded" alt="">
    <div class="caption">Output voltage and output current.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt44.png" class="img-fluid rounded" alt="">
    <div class="caption">Output powers at constant load scenario.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt45.png/" class="img-fluid rounded" alt="">
    <div class="caption">(a) Output voltage, (b) output current at variable load scenario.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt46.png" class="img-fluid rounded" alt="">
    <div class="caption">Output power at variable load scenario</div>
  </div>
</div>

<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt47.png/" class="img-fluid rounded" alt="">
    <div class="caption">Output current at unbalance load scenario.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt48.png" class="img-fluid rounded" alt="">
    <div class="caption">Inverter output current at unbalance load scenario.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt49.png/" class="img-fluid rounded" alt="">
    <div class="caption">Output current at nonlinear load scenario.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt50.png" class="img-fluid rounded" alt="">
    <div class="caption">Inverter output current at nonlinear load scenario.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2019--.pdf) here.

#### 2020

Microturbines serve as highly reliable energy sources, but their operational efficiency depends heavily on advanced control strategies to manage dynamic performance. This research addresses the challenge of improving the responsiveness of stand-alone microturbine generation systems, which often encounter significant speed drops and increased fuel consumption during sudden load variations. The primary objective was to develop a control architecture that maintains system stability more effectively than conventional models.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/mt51.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>

The proposed methodology introduces a novel approach using MPC  to optimize the microturbine's internal logic. Specifically, this method modifies the traditional Low-Value Gate (LVG)—a critical component in the microturbine's control loop that typically selects the minimum signal from various controllers—by integrating MPC. This shift allows the system to anticipate future operational states and adjust parameters more precisely than traditional dynamic models.

Simulation results confirm that this MPC-based configuration significantly enhances dynamic response times without negatively impacting the load side. Comparative analysis demonstrates that the novel method effectively reduces both fuel consumption and the magnitude of speed drops during transient periods. These findings suggest that replacing traditional control gates with predictive algorithms is a robust solution for increasing the efficiency and reliability of decentralized power units.


<div class="row text-center">
  <div class="col-3">
    <img src="/assets/img/projects/mt52.png/" class="img-fluid rounded" alt="">
    <div class="caption">Speed variations with and without MPC.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt53.png" class="img-fluid rounded" alt="">
    <div class="caption">Fuel demand variations with and without MPC.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt54.png/" class="img-fluid rounded" alt="">
    <div class="caption">Load side outputs: (a) three-phase voltages, (b) three-phase currents.</div>
  </div>
  <div class="col-3">
    <img src="/assets/img/projects/mt55.png" class="img-fluid rounded" alt="">
    <div class="caption">DC-link voltage.</div>
  </div>
</div>

For the full paper, please [Click](/assets/img/projects/papers/2020.pdf) here.