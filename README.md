# Characterizing percussive damage on primate stone tools using automated image analysis and 3D morphometry
Hannah Rausch (hannah_olivia_rausch@eva.mpg.de), Shannon McPherron, Lydia Luncz

Article link: PLACEHOLDER

This repository contains code used for data processing and analysis. Scripts were executed in Python (v 3.11.3). See requirements.txt for module versions.

The corresponding data can be accessed in the following Zenodo repository: PLACEHOLDER.

## k_means.ipynb
This notebook reads an obj file, segments out triangles corresponding to a selected (damaged) cluster and exports the (damaged) cluster as an obj file. 
K-means clustering is applied to the textured faces of an .obj mesh. The textured color at face centers are sampled, converted rgb to hsv, and clustered on selected hsv channels. The script includes an elbow plot to guide cluster count selection, and side-by-side 3d plots of the original textured mesh and the cluster mapping. The cluster average saturation and brightness are also computed, a plot is generated and the data is exported to csv. The user manually selects a cluster to which a user-defined buffer is applied (default: 0.5 mm) to include neighbourings triangles derived from average triangle edge length of the mesh.

## heatmaps.ipynb
This notebook generates a two panel figure illustrating roughness and curvature data of damaged and undamaged coordinates per anvil. The full, textured anvil surface is plotted and a colour map showing roughness and curvature data is superimposed. The 10 undamaged areas are plotted in a side panel. The shared colourbar is scaled to the 5th-95th percentile for better readability of the data.

## plots.ipynb
This notebook reads scalar field data (roughness and curvature) computed in CloudCompare of the full anvil surface and spatially joins it to damaged and undamaged point coordinates. 
For damaged point coordiantes this is done using a nearest-neighbour match. For undamaged point coordinates, all points within a defined radius are extracted (default = 5.64 mm). The notebook outputs a semi-colon delimited .txt file containing the scalar field data corresponding to the damaged and undamaged coordinates.
Then, the roughness and curvature data corresponding to damaged and undamaged point coordinates are plotted. The following plot types are included in the notebook: Kernel density estimates, box plots and scatterplots of median and maximum roughness and curvature values. The notebook also contains a code block to plot rebound hardness values per locality of the study area as a boxplot.

## stats.ipynb
This notebook computes summary statistic and Mann-Whitney U tests with common language effect sizes (CLES) for roughness and curvature data anvils in the dataset. It compares (1) damaged and undamaged surface conditions within each anvil and (2) between raw material groups. The results are exported as a multi-page excel sheet. 
A code block plots CLES values of roughness and curvature of within anvil comparisons as a dumb bell plot. Last, there are code blocks to run the following linear mixed models: 'roughness ~ hardness + (1 | anvil_id)', 'curvature ~ hardness + (1 | anvil_id)', 'roughness ~ hardness * condition (damaged/undamaged) + (1 | anvil_id)' and 'curvature ~ hardness * condition (damaged/undamaged) + (1 | anvil_id)'.
