---
layout: page
title: pH measure automation
description: Development of a Proof-of-Concept for Automated pH Measurement Using the Meca500 Robot
img: assets/img/projects/ph1.png
importance: 6
category: "All"
date: 2025-04-15
---

### Summary

This project was part of a broader collaboration with Pfizer, supported by Mitacs BSI funding. The overall objective was to develop a proof-of-concept (PoC) for automating laboratory tasks, either partially or fully, using a robotic arm.

The primary motivation for introducing robotic systems into laboratory environments includes achieving high precision and repeatability, reducing human error, and freeing up scientists’ time to focus on higher-level analytical work.

The main objectives of the project were:

- Develop functional workflows using a robotic arm
- Ensure consistent and accurate experimental results
- Demonstrate the performance advantages of robotic automation

The success criteria included:

- Adapting existing laboratory protocols for robotic execution
- Programming and optimizing robotic workflows for task automation
- Evaluating the performance of the automated system based on user feedback

This proof-of-concept aimed to demonstrate the feasibility, reliability, and practical value of robotic automation in real laboratory settings.

### Technical Stack

🔧 Key Software & Frameworks:
- ROS Noetic
- MoveIt
- OMPL (Open Motion Planning Library)
- Gazebo simulator
- PyBullet simulator
- Qt
- TULIP
- FreeCAD

🤖 Robotic arm platforms:
- Mecademic Meca500

🧠 Methods & Algorithms:
- Robot control 
- Motion planning & collision avoidance
- Circuite design
- Mechanical design
- Vision-guided pick-and-place (simulation phase)

💻 Languages:
- Python
- C++

### Concept

A pH value is a numerical indicator—typically ranging from 0 to 14 that represents the acidity or basicity of a solution. It is directly related to the hydrogen ion (H⁺) concentration and is defined by the formula: *pH=−log(H+)*. As the hydrogen ion concentration decreases, the pH value increases, and vice versa.

A standard pH testing procedure consists of two main stages: calibration and measurement. In both stages, the pH probe must be rinsed with distilled water to prevent contamination and ensure accurate readings. During calibration, buffer solutions are used to define reference points for the device. Typically, three buffer solutions are employed at room temperature (25 °C): pH 7, pH 4, and pH 10. These buffers allow for two- or three-point calibration, depending on the required accuracy.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ph2.webp" title="pH numbers" class="img-fluid rounded z-depth-1 mx-auto d-block" width="65%" %}
    </div>
</div>

From a system perspective, the architecture is built around ROS, with MoveIt serving as the motion planning core. A graphical user interface (GUI), developed using platforms such as TULIP or Qt, provides the frontend interaction layer. The system supports both simulation and real-robot execution, enabling seamless testing and deployment of automated pH measurement workflows.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ph1.png" title="core system" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
    </div>
</div>

### Robot

The robotic platform used in this project is the [Mecademic Meca500](https://mecademic.com/products/meca500-industrial-robot-arm/), a 6-DoF industrial robotic arm. Despite its compact size and limited reach of 33 cm, the Meca500 offers exceptionally high precision, with a position repeatability of 0.005 mm.

Due to its high accuracy, relatively affordable cost, and compact footprint, the Meca500 is well-suited for laboratory automation applications, particularly in constrained workspaces where precision and reliability are critical.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ph4.png" title="Meca500 robot" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
    </div>
</div>

### Simulation

The first phase of the project involved simulation studies in PyBullet and Gazebo to demonstrate the core capabilities of the system. The initial experiments focused on pick-and-place tasks, integrating motion planning with computer vision. The Open Motion Planning Library (OMPL) was used as the motion planner within a ROS Noetic framework, operating in Cartesian space to ensure smooth, precise, and collision-aware trajectory execution.

The following video presents a compilation of demonstrations, including Gazebo simulations with ROS, PyBullet simulations, real motion planning tests with ROS, early GUI designs developed using TULIP and Qt, and computer vision experiments visualized in RViz and Gazebo.

<!-- <video width="500" controls>
  <source src="/assets/img/projects/ph_vid2.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<video width="500" controls>
  <source src="/assets/img/projects/ph_vid1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> -->
<video width="500" controls>
  <source src="/assets/img/projects/ph_vid9.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<!-- <video width="500" controls>
  <source src="/assets/img/projects/ph_vid3.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video> -->

### Real Test

For real-world testing, the system included a digital pH meter, a custom 3D-printed probe holder, a custom probe washing system, and three standard calibration buffer solutions. To validate the measurements, three liquids with different pH values were tested: white vinegar, orange juice, and a baking soda solution.

A graphical user interface (GUI) was developed using Qt to provide intuitive and efficient control over the robotic workflow. The initial interface was designed using TULIP; however, it was later migrated to Qt due to its open-source flexibility and Python-based integration capabilities.

The video below demonstrates the full experimental setup, including the calibration procedure and the automated measurement process (To reduce the file size, the video was exported in 480p resolution and increased speed).

<video width="800" controls>
  <source src="/assets/img/projects/ph_vid4.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

### Appendix
#### Mechanical Design

To build a flexible and functional system, several custom components were designed by FreeCAD and 3D printed.

1- Probe Holder Design:

The probe holder was designed as a fixed mounting structure to ensure stability during operation. Initially, similar to the simulation setup, a two-finger gripper configuration was developed for pick-and-place handling on top of the MEGP 25LS gripper. While this design worked for lightweight objects such as plastic tubes, it was not suitable for handling the pH probe with its attached cable.

Although lighter pH probe models could potentially be handled directly using the robot’s gripper, the available probe in this project required a more stable and secure solution. Therefore, a dedicated holder was designed to ensure proper positioning and reliability during calibration and measurement.

The videos below demonstrate the experimental tests performed with both the gripper-based approach and the fixed probe holder design.

<video width="500" controls>
  <source src="/assets/img/projects/ph_vid5.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<p style="text-align:center;"><em>Successful plastic tube handling with grippers.</em></p>

<video width="500" controls>
  <source src="/assets/img/projects/ph_vid6.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<p style="text-align:center;"><em>Unsuccessful probe handling with grippers.</em></p>

<video width="500" controls>
  <source src="/assets/img/projects/ph_vid7.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<p style="text-align:center;"><em>Fixed probe design for more stability.</em></p>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ph5.png" title="env" class="img-fluid rounded z-depth-1 mx-auto d-block" width="70%" %}
    </div>
</div>
<div class="caption">
    MEGP 25LS gripper and 3D fingers.
</div>

2 - Probe Rinsing System

To ensure proper cleaning of the pH probe after each calibration and measurement step, a custom 3D-printed rinsing system was designed and integrated with an automated water pump. The goal was to create an efficient, compact, and reliable cleaning mechanism that could be seamlessly incorporated into the robotic workflow.

A detailed explanation of the system design and implementation is available on [my Instructables page](https://www.instructables.com/DIY-Automated-Water-Pump-a-Beginners-Guide/).

The video below shows an initial test of the rinsing system. Since the final pH measurements were accurate and consistent, the results confirm that the cleaning mechanism functions properly and does not introduce contamination between measurements.

<video width="500" controls>
  <source src="/assets/img/projects/ph_vid8.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
<p style="text-align:center;"><em>Initial test of probe cleaning system.</em></p>


### References for pH Measurement Systems

This project was completed in Winter 2025 within a limited timeframe. As a result, there is significant room for further development, both in terms of system architecture and mechanical design improvements. The purpose of sharing this work is to provide an initial insight into the feasibility and structure of the proposed system.

I am aware that fully automated laboratory measurement systems already exist, as illustrated in the link PDF below. These commercial solutions offer high reliability and integration. However, their primary limitations are high cost and single-purpose design.

In contrast, a properly designed robotic-arm-based platform offers greater flexibility. With modular tooling and appropriate workflow design, the same robotic system can potentially handle multiple laboratory tasks—ranging from pH measurement to osmolality testing and beyond—while maintaining adaptability and cost efficiency.

<a href="/assets/img/projects/References_pH_measurement_systems.pdf" target="_blank">Download the PDF</a>

### GitHub

To access the source code, please follow this [Link].


