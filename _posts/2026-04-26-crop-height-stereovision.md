---
title: 'Using Stereovision for Crop Height Estimation'
date: 2026-04-26
permalink: /posts/2026/04/crop-height-stereovision/
tags:
  - bioengineering
  - agriculture
  - computer vision
  - stereovision
---

*Co-authored by Jasanmol Singh (Ph.D. Student, Agriculture) and Shantanu Kore (Ph.D. Student, Bioengineering).*

[cite_start]Crop height is a proven and crucial predictor of biomass quantity and availability[cite: 6]. However, collecting this data in the field has historically been a bottleneck. [cite_start]Traditionally, researchers have relied on manual crop height measurement—a practice that is not only labor-intensive but also highly prone to fatigue and human error[cite: 7]. 

While modern techniques exist, they come with their own trade-offs. [cite_start]UAV-based Structure from Motion requires lengthy processing times, and satellite imagery often suffers from low temporal resolution, making real-time results impossible[cite: 8]. [cite_start]Even ground-based methods, like ultrasound sensors, are limited because they are point-specific and fail to provide a complete spatial distribution of the crop canopy[cite: 9].

[cite_start]To bridge this gap, our recent project explores using **Stereovision** to automate and improve crop height measurement [cite: 10-11].

### The Goal
[cite_start]Our primary objective is to develop a system that yields pixel-level crop height results[cite: 12]. [cite_start]By utilizing stereovision, we can also capture additional RGB information about the crops, which paves the way for advanced 3D structural studies and deeper growth characterization [cite: 13-14].

### The Stereo-Vision Processing Pipeline
[cite_start]To achieve this, we developed a robust stereo-vision processing pipeline[cite: 15]. 

[cite_start]First, we capture synchronized images of forage quadrants using a Luxonis OAK-D Depth Camera at the Clemson Piedmont REC[cite: 16]. [cite_start]The system calculates the horizontal pixel shift between the left and right images[cite: 17]. 

Once the raw data is captured, the pipeline executes the following steps:
* [cite_start]**Edge Detection:** Canny Edge Detection is applied to the depth map to identify the "strong edges" representing the top of the crop canopy[cite: 18].
* [cite_start]**Grouping:** The system groups pixels with similar depth intensities to isolate the target crop from the background[cite: 19].
* [cite_start]**Depth-Based Filtering:** To ensure high accuracy, the system removes the ground and distant background objects by setting a specific depth range $(d_l < d < d_u)$[cite: 20]. 
* [cite_start]**ROI Selection:** The final Region of Interest (ROI) is defined, focusing on the closest clustered crop region to the camera[cite: 21].

### Field Data Collection
[cite_start]For ground truth comparison, we built a mounting rod equipped with an Emlid Reach RS+ RTK-GPS [cite: 23-24]. 

<img src="Slide8.jpg" alt="Mounting rod with Emlid Reach RS+ RTK-GPS">

[cite_start]We collected data at two different mounting heights: $132\text{ cm}$ ($\sim 4\text{ ft}$) and $190\text{ cm}$ ($\sim 6\text{ ft}$)[cite: 142, 254]. [cite_start]The custom interface ingested synchronized frames, allowing us to capture ground reference depth and canopy depth simultaneously alongside human manual tape measurements [cite: 147-153]. 

<img src="Slide10.jpg" alt="Sample depth images showing RGB and heat maps">

### Results & Discussion
After evaluating the system-averaged outputs against human-averaged inputs, several interesting observations emerged:

1.  [cite_start]**System Objectivity:** The crop height measured by the depth camera proved to be far more objective compared to the manual tape measure measurements[cite: 256]. 
2.  [cite_start]**Mounting Considerations:** We found that relying on a manual mount height made more sense, as perfectly flat ground conditions were rarely met during data collection[cite: 257].
3.  **Human Bias in Manual Measurement:** The manual crop height measurements were consistently higher than the depth camera-based measurements. [cite_start]Humans generally tend to measure the topmost outlier plants, ignoring the smaller plants growing beneath that also contribute to the true mean crop height[cite: 258].
4.  [cite_start]**Environmental Variables:** We observed a negative crop height value occasionally, which was attributed to hand shaking and unwanted vibrations during the data collection process[cite: 259].

### Conclusion
Depth cameras and stereovision hold immense potential for providing highly accurate crop height measurements. [cite_start]As long as calibration and setup are done properly, and standard conditions are maintained during the data collection procedure, this technology offers a scalable, objective alternative to manual field labor [cite: 260-261].
