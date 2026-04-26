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

### The Goal
Our primary objective is to develop a system that yields pixel-level crop height results. By utilizing stereovision, we can also capture additional RGB information about the crops, which paves the way for advanced 3D structural studies and deeper growth characterization.

---

### The Stereo-Vision Processing Pipeline
To achieve this, we developed a robust stereo-vision processing pipeline. 

First, we capture synchronized images of forage quadrants using a Luxonis OAK-D Depth Camera. As shown below, the camera utilizes a center RGB sensor alongside left and right monochrome sensors separated by a $60\text{mm}$ baseline distance.

<div align="center">
  <img src="/images/stereo-vision processing pipeline.JPG" alt="Luxonis OAK-D sensor layout with left/right mono and center RGB">
  <p><em>Camera sensor architecture and disparity matrix capture.</em></p>
</div>

The system calculates the horizontal pixel shift (disparity) between the left and right images. Using basic optical geometry, depth ($Z$) is calculated using the baseline distance ($T$) and the focal length ($f$).

<div align="center">
  <img src="/images/DIsparity_measurement.JPG" alt="Optical geometry and mathematical execution for disparity measurement">
  <p><em>Optical geometry and disparity calculations utilizing Normalized Cross-Correlation (NCC).</em></p>
</div>

Once the raw data is captured, the automated system executes a specific processing pipeline:
1. **Depth Data Preprocessing:** Generating the raw disparity map.
2. **Ground Thresholding:** Applying upper and lower spatial limits to isolate the crop envelope and ignore uneven ground data.
3. **Automated Averaging:** Aggregating the thresholded data into a singular crop height value.

<div align="center">
  <img src="/images/Automated steriovision System.JPG" alt="Automated Stereovision System Flowchart">
  <p><em>The complete processing pipeline from data capture to performance comparison against human ground truth.</em></p>
</div>

---

### Field Data Collection
For ground truth comparison against our automated pipeline, we built a physical mounting rod equipped with an Emlid Reach RS+ RTK-GPS to ensure high-precision spatial tracking.

<div align="center">
  <img src="/images/Mounting rod with height marking for steriovision camera.JPG" alt="Mounting rod with height markings">
  <p><em>Fig 1: Custom mounting rod with precise length markings.</em></p>
</div>

<div align="center">
  <img src="/images/RTK-GPS.JPG" alt="Emlid Reach RS+ RTK-GPS attached to the rig">
  <p><em>Fig 2: Emlid Reach RS+ mounted on the rod for GPS data collection.</em></p>
</div>

We collected data at two different mounting heights in the field: $132\text{ cm}$ ($\sim 4\text{ ft}$) and $190\text{ cm}$ ($\sim 6\text{ ft}$).

<div align="center">
  <img src="/images/Depth camera mounted On a rod.JPG" alt="Depth camera mounted on the collection rod">
  <p><em>Fig 3: Close-up of the depth camera mounted on the collection rod.</em></p>
</div>

<div align="center">
  <img src="/images/Data Collection with depth camera and GPS.JPG" alt="Researcher operating the stereovision collection rig in the field">
  <p><em>Fig 4: Active field data collection utilizing the depth camera and GPS rig.</em></p>
</div>

To streamline this process, we developed a custom Crop Height Collector interface. This software ingests synchronized frames, allowing us to capture ground reference depth and canopy depth simultaneously alongside human manual tape measurements.

<div align="center">
  <img src="/images/Data collection interface.JPG" alt="Crop Height Collector field data system interface">
  <p><em>Fig 5: Software interface for capturing and logging ground reference and canopy depth.</em></p>
</div>

### Data Tables

<div align="center">
  <img src="/images/Data for 132cm-4ft measurements.JPG" alt="Data at 132 cm mounting height">
  <p><em>Table 1: Data collected at 132 cm (~4 ft) mounting height.</em></p>
</div>

<div align="center">
  <img src="/images/Data for 190 cm - 6ft measurements.JPG" alt="Data at 190 cm mounting height">
  <p><em>Table 2: Data collected at 190 cm (~6 ft) mounting height.</em></p>
</div>

---

### Results & Discussion
After processing the raw frames into depth heatmaps, we evaluated the system-averaged outputs against the human-averaged inputs. 

<div align="center">
  <img src="/images/Sample depth images for crop height measurements.JPG" alt="RGB and corresponding depth heatmaps of crop canopies">
  <p><em>Fig 6: Sample RGB images and their corresponding depth heatmaps used for measurement.</em></p>
</div>

Several interesting observations emerged from the data:

1. **System Objectivity:** The crop height measured by the depth camera proved to be far more objective compared to the manual tape measure measurements. 
2. **Mounting Considerations:** We found that relying on a manual mount height made more sense, as perfectly flat ground conditions were rarely met during data collection.
3. **Human Bias in Manual Measurement:** The manual crop height measurements were consistently higher than the depth camera-based measurements. Humans generally tend to measure the topmost outlier plants, ignoring the smaller plants growing beneath that also contribute to the true mean crop height.
4. **Environmental Variables:** We observed a negative crop height value occasionally, which was attributed to hand shaking and unwanted vibrations during the data collection process.

### Conclusion
Depth cameras and stereovision hold immense potential for providing highly accurate crop height measurements. As long as calibration and setup are done properly, and standard conditions are maintained during the data collection procedure, this technology offers a scalable, objective alternative to manual field labor.
