---
layout: page
title: AI and Robotics in art
description: A Journey into Developing Robotic Systems for Art Production
img: assets/img/projects/ac1.webp
importance: 6
category: "All"
---

### Introduction

To gain new experiences, I joined an early-stage startup in Montreal, Quebec, called Acrylic Robotics. The core idea behind the startup was to create art using robotic arms. Artworks are initially designed by digital artists and, after a series of processing steps, are physically painted by a robotic system. The main goal was to help artists create high-quality, textured paintings at a much higher volume than traditional methods allow.

When I joined the team in mid-September 2022, the company was working on scaling its system to produce larger artworks while building a more stable and reliable pipeline for generating different types of acrylic paintings. My role focused on developing a consistent and robust robot control core and pushing the overall art production process forward. I worked there as a PhD intern until the end of 2023, supported by the Mitacs BSI funding and the CoRoM scholarship. During this period, we went through multiple development phases and participated in several events and exhibitions.

During this period, I worked hands-on with various robotic arms, including the Mecademic Meca500, Kinova Gen3 Lite, Kinova Gen3, and Kinova Link 6. In parallel, I was closely involved in AI-related developments that supported both the artistic vision and the technical requirements of the project. In the following sections, I share selected materials and results from my journey at Acrylic Robotics.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac1.png" title="All robots I worked with" class="img-fluid rounded z-depth-1 mx-auto d-block" width="75%" %}
    </div>
</div>
<div class="caption">
    All robotic arms I worked with them.
</div>

### phase 1

The first step was to refine and stabilize all painting functions developed for small-format artworks using the Meca500 robot. These functions were then transferred to larger robotic platforms, first the Kinova Gen3 Lite and later the Kinova Gen3. This transfer was not straightforward, as the precision, repeatability, and kinematic characteristics of these robotic arms differ significantly. In addition, I had to address singularities at the low-level control layer and develop new approaches for painting brush calibration.

Beyond robot control, we also redesigned the brush-cleaning mechanism and color pots to ensure reliable and consistent operation across different painting sessions. By the end of this phase, we were able to produce small-format artworks (5 × 7 inches) using the Meca500 and medium-format artworks (11 × 14 inches) using the 7-DoF Kinova Gen3 robot. The images below show examples of medium-size painting results produced in 2022.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac2.png" title="Some Paint Results " class="img-fluid rounded z-depth-1 mx-auto d-block" width="65%" %}
    </div>
</div>
<div class="caption">
    Some Paint Results.
</div>

In addition, we participated in events such as NextAI and RAW Montreal, where we showcased our work and connected with the creative and tech communities. Some memorable moments from these events are shown below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac3.png" title="the team" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
    </div>
</div>

Two time-lapse videos from this period are also available to watch below. All copyrights for these videos are reserved by Acrylic Robotics.

<div style="display: flex; justify-content: space-between; flex-wrap: wrap; gap: 10px;">
  <div style="text-align: center;">
    <a href="https://youtu.be/ne2WsiwHSmU?si=UQS6F7szodGyz3vG" target="_blank">
      <img src="/assets/img/projects/Youtube_logo.png" alt="Meca500 eye paint" width="120"/>
    </a>
    <div style="font-size: 0.9em;">Meca500 eye paint</div>
  </div>
  <div style="text-align: center;">
    <a href="https://youtu.be/glMbE3oxVs4?si=uG5nYvkrN9dCSkcC" target="_blank">
      <img src="/assets/img/projects/Youtube_logo.png" alt="Meca500 flower paint" width="120"/>
    </a>
    <div style="font-size: 0.9em;">Meca500 flower paint</div>
  </div>
  <div style="text-align: center;">
    <a href="https://youtu.be/COC3XqC6s6g?si=L4AqZJ4u1CrsPN1U" target="_blank">
      <img src="/assets/img/projects/Youtube_logo.png" alt="Gen3 eye paint" width="120"/>
    </a>
    <div style="font-size: 0.9em;">Gen3 eye paint</div>
  </div>
  <div style="text-align: center;">
    <a href="https://youtu.be/q-3vbJUOtd0?si=xccYQFVGXSMyBVk0" target="_blank">
      <img src="/assets/img/projects/Youtube_logo.png" alt="Gen3 wave paint" width="120"/>
    </a>
    <div style="font-size: 0.9em;">Gen3 wave paint</div>
  </div>
  <div style="text-align: center;">
    <a href="https://youtu.be/m-4-JkgW81U?si=t5fDXjwLQzgJBlOM" target="_blank">
      <img src="/assets/img/projects/Youtube_logo.png" alt="Gen3 girl paint" width="120"/>
    </a>
    <div style="font-size: 0.9em;">Gen3 girl paint</div>
  </div>
</div>


### phase 2

The objective of this phase was to make the system more stable and to transition toward large-format paintings. During this period (2023), I worked with several robotic platforms, including the Kinova Gen3 (both 6-DoF and 7-DoF versions) and the Kinova Link 6, an industrial robotic arm.

The main developments required to support larger painting sizes included standardizing the robot’s environment, modifying key painting functions such as brush cleaning, drying, dipping, and color pots with lids, and implementing methods to prevent brushes from becoming overly saturated. We also developed more efficient motion planning strategies for large-scale paintings using RoboDK, along with an improved brush calibration process.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac4.png" title="Main developments for transferring paint sizes​" class="img-fluid rounded z-depth-1 mx-auto d-block" width="100%" %}
    </div>
</div>

In addition to refining painting details and polishing the control code, I worked closely with the software team to enhance the Krita digital design software based on robot testing results. At that time, we were preparing to launch our digital art platform, which required customizing the software to account for robotic constraints, brush behavior, and pressure control.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac5.jpg" title="some results​" class="img-fluid rounded z-depth-1 mx-auto d-block" width="75%" %}
    </div>
</div>
<div class="caption">
    Some Painted Results.
</div>

Another major development direction involved using AI methods to convert images into stroke-based representations for robotic painting. This capability was particularly promising, as it opened new possibilities for robot painting from both digital artworks and real images. To support this goal, I collaborated with the machine learning team to test models and engage in iterative brainstorming sessions. One of the methods explored was DiffVG, which segments an image into regions and fits Gaussian distributions to each region to define stroke parameters. Sequences of Gaussians represent painting trajectories, enabling a novel painterly rendering approach that optimizes curve control points, stroke width, color, and opacity. Although the results were promising, I was not directly involved in the long-term development of this method.

<img src="/assets/img/projects/ac7.png" alt="Sample Image" width="500"/>
<video width="500" controls>
  <source src="/assets/img/projects/ac8.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<img src="/assets/img/projects/ac6.png" alt="Sample Image" width="500"/>


During this period, we also completed several commissioned projects and collaborated with digital artists. Notable works included a Valentine’s Day piece for Kinova and a detailed portrait of the Link 6 robot. In parallel, I supervised three capstone student projects at McGill University focusing on brush switching, brush cleaning, and canvas stretching.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac9.jpg" title="Main developments for transferring paint sizes​" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>
<div class="caption">
    Kinova Link 6 portrait.
</div>

A major milestone for the team was participating in the CBC Dragons’ Den TV show in Toronto. Preparing for this event required producing high-quality artworks and ensuring that every technical and artistic detail was carefully refined. I also had the opportunity to represent the company at several events, including RoboHacks at McGill, the Canadian Robotics Council in Montreal, Startupfest in Montreal, and the CoRoM Summer Forum at ÉTS.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/projects/ac10.png" title="Main developments for transferring paint sizes​" class="img-fluid rounded z-depth-1 mx-auto d-block" width="50%" %}
    </div>
</div>
<div class="caption">
    Dragons’ Den setup.
</div>

### Challenges & Potential Solutions​

In any robotics project, technical challenges are inevitable, and as a robotics engineer, I had to identify and overcome several of them throughout this work. In this section, I highlight some of the key technical challenges I faced while working on this niche application of robotic art production.

Due to differences in precision and repeatability across robotic platforms, a sensor-based feedback system was necessary to maintain consistent brush pressure on the canvas. While the robots’ internal controllers could handle force control to a certain extent, achieving higher consistency required an external feedback mechanism. One potential solution was the use of a distance sensor. I tested a Time-of-Flight (ToF) sensor for this purpose, and the results can be found here: [GitHub Link](https://github.com/pouyan-asg/VL53L4CD-distance-sensor-test/tree/main).

Another challenge involved singularity avoidance. A more robust singularity-handling strategy was required to ensure that painting quality remained unaffected during motion. This called for a well-designed motion planning pipeline. Although the problem was technically interesting, time constraints prevented full development. I attempted to compute inverse kinematics solutions to bypass singular configurations, but limitations in the robots’ low-level controllers posed significant technical barriers.

An additional challenge was translation speed. To increase art production throughput, higher motion speeds were required while maintaining high accuracy. Achieving this balance ideally requires access to low-level robot control and a properly tuned motion planner. While I was able to increase speed to some extent, this often came at the cost of reduced motion quality.

Brush calibration prior to painting was another major challenge. We initially tested brush pressure manually across different regions of the canvas and later experimented with pressure mapping using interpolation of unstructured data to achieve more consistent pressure. However, due to limitations in measurement precision, these methods did not achieve full consistency.

For the Meca500 robot, its extremely high precision was advantageous, but its limited reach became a primary constraint. We considered integrating a gantry system to extend its workspace, but this remained an open idea and was never implemented.

Finally, for AI-rendered images, a key technical challenge was synchronizing brush thickness, stroke length, and stroke curvature to accurately reflect the capabilities of the physical robot. In addition, stroke colors needed to be fully opaque, as achieving certain transparency effects is difficult in real-world painting scenarios.

### Materials

-- Will be completed!: **[PDF report](https://github.com/pouyan-asg)**.

### references

This section presents a selection of reference papers reviewed in the context of this project:

[1] www.cloudpainter.com​

[2] www.engadget.com/ai-painting-project-sxsw-2021-225235320.html​

[3] Santos, M., Notomista, G., Mayya, S., & Egerstedt, M. (2020). Interactive Multi-Robot Painting Through Colored Motion Trails. Frontiers in Robotics and AI, 7, 580415.

[4] https://www.youtube.com/watch?v=0cln5VhQum0​

[5] T. Lindemeier, J. Metzner, L. Pollak, and O. Deussen, “Hardware-Based Non-Photorealistic Rendering Using a Painting Robot,” Comput. Graph. Forum, vol. 34, no. 2, pp. 311–323, May 2015.​

[6] A. I. Karimov, E. E. Kopets, V. G. Rybin, S. V. Leonov, A. I. Voroshilova, and D. N. Butusov, “Advanced tone rendition technique for a painting robot,” Robot. Auton. Syst., vol. 115, pp. 17–27, May 2019.

[7] Karimov, A. I., Kopets, E. E., Rybin, V. G., Leonov, S. V., Voroshilova, A. I., & Butusov, D. N. (2019). Advanced tone rendition technique for a painting robot. Robotics and Autonomous Systems, 115, 17-27.​

[8] Luo, R. C., Hong, M. J., & Chung, P. C. (2016, October). Robot artist for colorful picture painting with visual control system. In 2016 IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS).​

[9] P. Tresset and F. Fol Leymarie, “Portrait drawing by Paul the robot,” Comput. Graph., vol. 37, no. 5, pp. 348–363, Aug. 2013.

[10] Scalera, L., Seriani, S., Gasparetto, A., & Gallina, P. (2019). Watercolour robotic painting: a novel automatic system for artistic rendering. Journal of Intelligent & Robotic Systems, 95(3), 871-886.​

[11] Beltramello, A., Scalera, L., Seriani, S., & Gallina, P. (2020). Artistic robotic painting using the palette knife technique. Robotics, 9(1), 15.​

[12] Scalera, L., Seriani, S., Gallina, P., Lentini, M., & Gasparetto, A. (2021). Human–robot interaction through eye tracking for artistic drawing. Robotics, 10(2), 54.

[13] Monaghan, P. (1997). An art professor uses artificial intelligence to create a computer that draws and paints. The Chronicle of Higher Education, 27-28 

[14] Guo, C., Bai, T., Lu, Y., Lin, Y., Xiong, G., Wang, X., & Wang, F. Y. (2020, August). Skywork-daVinci: A novel CPSS-based painting support system. In 2020 IEEE 16th International Conference on Automation Science and Engineering (CASE) (pp. 673-678). IEEE.​

[15] Schaldenbrand, P., McCann, J., & Oh, J. (2023, May). FRIDA: A collaborative robot painter with a differentiable, real2sim2real planning environment. In 2023 IEEE International Conference on Robotics and Automation (ICRA) (pp. 11712-11718). IEEE.

[16] Li, T. M., Lukáč, M., Gharbi, M., & Ragan-Kelley, J. (2020). Differentiable vector graphics rasterization for editing and learning. ACM Transactions on Graphics (TOG), 39(6), 1-15.​

[17] Chen, G., Dumay, A., & Tang, M. (2021). diffvg+ CLIP: generating painting trajectories from text. preprint.​

[18] Hertzmann, A. (1998, July). Painterly rendering with curved brush strokes of multiple sizes. In Proceedings of the 25th annual conference on Computer graphics and interactive techniques (pp. 453-460).​

[19] Ma, X., Zhou, Y., Xu, X., Sun, B., Filev, V., Orlov, N., ... & Shi, H. (2022). Towards layer-wise image vectorization. In Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (pp. 16314-16323).