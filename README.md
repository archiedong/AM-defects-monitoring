[![IMAGE ALT TEXT](http://img.youtube.com/vi/YTl2wdyGfww/0.jpg)](http://www.youtube.com/watch?v=YTl2wdyGfww "laser additive manufacturing")

# AM_defects_monitoring
In situ multivariate monitoring methods for selective laser melting additive manufacturing process based on images.

## Introduction
[![IMGAE ALT TEXT](http://img.youtube.com/vi/3AfuCaKLspo/0.jpg)](http://www.youtube.com/watch?v=3AfuCaKLspo "laser additive manufacturing2")

The limited stability and repeatability of metal AM processes represent a major barrier for the industrial breakthrough of metal AM systems. Meanwhile, by in-situ monitoring of the image data in the AM process, it becomes possible to quick detect the defects and unstable conditions, adapt and even correct the process for zero-defect AM. For example, a hot-spot is a local over-heating caused by diminished heat flux towards surrounding materials. The conventional statistical methods have indicated that the location plays a crucial role on the hotspot formation, but only few take temporal features into account. Consider the hotspot located in the corner and edge, it is expected that the corner position should have a higher chance of hotspots than the edge. For time variation, it is also expected that overtime heating tend to occur more hotspots. Further, locations and time themselves may be both auto-correlated and cross-correlated. Therefore, due to the limited resources and high cost of AM process, it is important to accurately identify the location and time simultaneously that are likely to cause hotspots.

![](https://user-images.githubusercontent.com/60518209/219544576-de91286f-33e5-432c-b949-0d05435bcf41.mp4)

A hot-spot is a local over-heating caused by a dimished heat flux towards surrounding material, shown in the pictures
<p align="center">
  <img src = "https://user-images.githubusercontent.com/60518209/219547544-4effa63d-c011-46a0-97d2-734d9ea50288.mp4" width = "630" />
  <img src="https://user-images.githubusercontent.com/60518209/219546708-b6863677-6971-45d3-9f5d-0dfda6348cca.png" width="630" />
</p>

The data is coming from high-speed camera (300 fps). 
<p align="center">
  <img src="https://user-images.githubusercontent.com/60518209/219547021-15e9f4cb-dda4-4565-9dbc-138c839e1258.png" width="630" />
</p>

## Methodology
1. Temporal Principla Component Analysis: Unfolding (from images to vectors), and apply principal component analysis to image data with no segmentation or edge detection operation needed.
2. Spatial Principla Component Analysis.
<p align="center">
  <img src = "https://user-images.githubusercontent.com/60518209/219688834-6504ac18-c1d1-40cd-b458-1bfb03a274eb.png" width = "230" />
  <img src="https://user-images.githubusercontent.com/60518209/219690131-7f482536-25c0-48fd-b5a6-6e7e8dd32870.png" width="530" />
</p>

Use of Hotelling’s $𝑇^2$ as a synthetic index to describe the information content along the most relevant components of the video image data within 𝐽 observed frames. Alarm rule based on k-means clustering of $T^2(m, n)$. When process is IC: k = 2 clusters are expected (background and normal melting). When the process is OOC, addtional clusters correspond to defective areas (hotspots).

<p align="center">
  <img src="https://user-images.githubusercontent.com/60518209/219692322-d9108cb1-c279-4e07-bd8f-d5f2f210d8eb.png" width="630" />
</p>
3. Spatially weighted T-mode PCA: incorporating pixel spatial correlation into the projection entailed by the T-mode PAC to preserve the spatial depency and enhance the identification of local defects. The weighted sample variance-covariance matrix is

```math
S = \frac{1}{p - 1} (X - \bar{x})^T W(X - \bar{x})
```

where $X \in R^{p \times J}$ is the data matrix and $\bar{x}$ is the sample mean vector. $W$ is the spatial weight matrix, where the (k, h) element of matrix, $w_{k,h}$ quantifies the spatial dependency between the k-th and h-th pixels.


## Simulation Analysis
ST-PCA requires a smaller number of PCs to explain a given % of the overall variability. And moving window updating is more parsimonious. The method is suitable to deal with detection and localization of anomalies in video image data (where an underlying process dynamics is present). And it is suitable for anomalies that are clustered in space and auto-correlated in time.

<p align="center">
  <img src="https://user-images.githubusercontent.com/60518209/219696878-3832b6ea-6ba8-4796-8512-1ee40a94efa0.png" width="430" />
  <img src="https://user-images.githubusercontent.com/60518209/219696929-3bf619b4-48a7-40b9-bca4-74377e11debb.png" width="430" />
</p>
