# LiDAR data for enriching open geospatial building datasets: implications for urban building energy modeling 

<p align="center"><img src="https://raw.githubusercontent.com/SustainableUrbanSystemsLab/CP-GNI2024-Symposium-Enriching-geospatial-building-datasets/refs/heads/main/Figures/GraphicalAbstract.jpg"></p>

## Introduction

Informed decision-making is critical to facilitating sustainable urban development as urban populations grow larger. Using geospatial data and energy simulation tools, Urban Building Energy Models (UBEM) can provide data-driven decision support for architects, urban planners, and energy policymakers.  A crucial part of developing an accurate UBEM is the seamless integration of high-quality aerial light detection and ranging (LiDAR), digital elevation models (DEM), building stock, and weather data​. These data are fundamental for solar rooftop potential analysis and simulation-based energy consumption estimation​. In this study, we aim to streamline and optimize the creation of urban building models using publicly available datasets for the purpose of UBEM simulations. We do this by using an automated 3D model creation workflow that consists of requesting geospatial datasets via open APIs and processing these data using platform-independent software libraries. 

## Methodology

We propose a data enrichment pipeline that requests and processes the following datasets: pre-labeled LiDAR and DEM data from the USGS 3D Elevation Program (3DEP), and building footprint data from Open Street Maps (OSM) and Federal Emergency Management Agency (FEMA). We combine these data by using two common bounding box geodetic coordinates. Then, we separate the point cloud data based on point class as either ground, tree, or building and intersect the building points with the footprints. Afterward, we use basic Alpha Shape triangulation for reconstructing roofs, Efficient RANSAC to identify roof slope planes, and 3D Alpha Wrapping for reconstructing tree canopies as meshes. Finally, we reconstruct the DEM as mesh geometry and project the building footprints onto it. To estimate building height, we use the average difference between the projected building elevation and the corresponding LiDAR point z coordinates. Algorithms are developed in Python and are implemented as components in Grasshopper 3D for 3D model creation and as stand-alone methods in a Jupyter Notebook (available here on GitHub) for GeoJson generation. 

## Results

We have examined the city of Atlanta, GA, which represents common residential building types in the US. In cities such as Atlanta, where high vegetation is prevalent, it is difficult to infer building heights due to the density of pre-labeled vegetation points. We also observe that the FEMA dataset provides oversimplified building footprint geometry, but accurate building type information, while OSM buildings have better footprint geometry, but almost no height data. By merging both building datasets and estimating building height using LiDAR data at scale, especially in regions with high tree density, we aim to average out errors caused by vegetation occlusion. 

## Conclusion

In this study, we demonstrate how streamlining data collection and processing can expedite the preparation of UBEM inputs. A major limitation of this approach is that it is difficult to achieve a high level of detail, as aerial LiDAR data mainly captures the roofs of buildings. One possible solution would be to use street view imagery to gather additional insight into façade materials and characteristics such as window-to-wall ratio. Future work could involve measuring how geometry reconstruction quality affects UBEM simulation accuracy and finding which spatial properties of the urban landscape influence results. 

## Author

- Name: [Silvia Vangelova](mailto:vangelova@ibi.baug.ethz.ch)
- LinkedIn: [Link](https://www.linkedin.com/in/silvia-vangelova-5ba9a4163/)
- Institution: Georgia Institute of Technology
- Program: M.S. Analytics (OMSA)
- Advisor: Dr. Patrick Kastner

## Repository Structure

- `data/`: Directory containing the data used in this Notebook
- `images/`: Directory containing images produces from running the Notebook
- `README.md`: This file, providing an overview of the thesis and repository.

## Instructions for reconstructing mesh geometry in Jupyter Notebook 

Environment set-up:
  - python -m venv env  
  - env\Scripts\activate
  - pip install -r requirements.txt

## Source

[Link](https://github.com/xtearas/GNI-Symposium-Enriching-geospatial-building-datasets/tree/main) to this repository.
