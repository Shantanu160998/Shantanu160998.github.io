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

Crop height is a proven and crucial predictor of biomass quantity and availability. However, collecting this data in the field has historically been a bottleneck. Traditionally, researchers have relied on manual crop height measurement—a practice that is not only labor-intensive but also highly prone to fatigue and human error. 

While modern techniques exist, they come with their own trade-offs. UAV-based Structure from Motion requires lengthy processing times, and satellite imagery often suffers from low temporal resolution, making real-time results impossible. Even ground-based methods, like ultrasound sensors, are limited because they are point-specific and fail to provide a complete spatial distribution of the crop canopy.

To bridge this gap, our recent project explores using **Stereovision** to automate and improve crop height measurement.

### Main Goal
Our primary objective is to develop a system that yields pixel-level crop height results. By utilizing stereovision, we can also capture additional RGB information about the crops, which paves the way for advanced 3D structural studies and deeper growth characterization.

### The Stereo-Vision Processing Pipeline
To achieve this, we developed a robust stereo-vision processing pipeline. 

<img src="/images/YOUR_IMAGE_NAME_ROD.jpg" alt="Mounting rod with Emlid Reach RS+ RTK-GPS">

First, we capture synchronized images of forage quadrants using a Luxonis OAK-D Depth Camera at the Clemson Piedmont REC. The system calculates the horizontal pixel shift between the left and right images. 

Once the raw data is captured, the pipeline executes the following steps:
* **Edge Detection:** Canny Edge Detection is applied to the depth map to identify the "strong edges" representing the top of the crop canopy.
* **Grouping:** The system groups pixels with similar depth intensities to isolate the target crop from the background.
* **Depth-Based Filtering:** To ensure high accuracy, the system removes the ground and distant background objects by setting a specific depth range ($d_l < d < d_u$). 
* **ROI Selection:** The final Region of Interest (ROI) is defined, focusing on the closest clustered crop region to the camera.

### Field Data Collection
For ground truth comparison, we built a mounting rod equipped with an Emlid Reach RS+ RTK-GPS. 

<img src="/images/YOUR_IMAGE_NAME_ROD.jpg" alt="Mounting rod with Emlid Reach RS+ RTK-GPS">

We collected data at two different mounting heights: $132\text{ cm}$ ($\sim 4\text{ ft}$) and $190\text{ cm}$ ($\sim 6\text{ ft}$). The custom interface ingested synchronized frames, allowing us to capture ground reference depth and canopy depth simultaneously alongside human manual tape measurements. 

<img src="/images/YOUR_IMAGE_NAME_HEATMAP.png" alt="Sample depth images showing RGB and heat maps">

### Results & Discussion
After evaluating the system-averaged outputs against human-averaged inputs, several interesting observations emerged:

1. **System Objectivity:** The crop height measured by the depth camera proved to be far more objective compared to the manual tape measure measurements. 
2. **Mounting Considerations:** We found that relying on a manual mount height made more sense, as perfectly flat ground conditions were rarely met during data collection.
3. **Human Bias in Manual Measurement:** The manual crop height measurements were consistently higher than the depth camera-based measurements. Humans generally tend to measure the topmost outlier plants, ignoring the smaller plants growing beneath that also contribute to the true mean crop height.
4. **Environmental Variables:** We observed a negative crop height value occasionally, which was attributed to hand shaking and unwanted vibrations during the data collection process.

### Conclusion
Depth cameras and stereovision hold immense potential for providing highly accurate crop height measurements. As long as calibration and setup are done properly, and standard conditions are maintained during the data collection procedure, this technology offers a scalable, objective alternative to manual field labor.
