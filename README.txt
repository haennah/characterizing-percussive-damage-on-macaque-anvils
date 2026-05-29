k_means.ipynb
 	applies k-means clustering to the textured faces of an .obj mesh.
	samples texture color at face centers (averaged from vertex uvs), converts rgb to hsv, and clusters on selected hsv channels (default: saturation and value).
	includes an elbow plot (k=2-10) to guide cluster count selection, a 3d scatter plot of hsv color space colored by cluster, and side-by-side 3d plots of the original 	textured mesh and the cluster mapping.
	cluster average saturation and brightness are exported to csv.
	damage clusters are selected manually based on visual inspection. selected clusters are grown outward by a user-defined metric buffer (default 0.5mm, converted to 	topological rings via average edge length) and extracted as a masked .obj.

plots.ipynb
  reads scalar field data (roughness and curvature) from the full anvil surface and
  spatially joins it to damaged and undamaged point coordinates.
  - damaged: nearest-neighbour match (1 point per input coordinate, k=1 kdtree query).
  - undamaged: all full-surface points within radius_mm (default 5.64mm) are included, giving more rows than input coordinates.
  - outputs one semicolon-delimited .txt file per anvil.
  - DESCRIBE PLOTTING CODE HERE
  - includes code to read schmidt hammer hardness values from the tools phangnga database (.xlsx) for
  the 19 study anvils. averages repeated measurements per anvil, groups by locality
  (island + raw material type), and plots a strip/box plot for comparison across
  kbn sandstone, kby sandstone, al limestone i, and al limestone ii.

stats.ipynb
  runs summary statistics and non-parametric tests on the spatial join output, using a
  balanced dataset where n damaged and n undamaged patches are equalised per anvil
  (random downsampling, random_seed=4). tests: mann-whitney u (within-anvil, bonferroni),
  kruskal-wallis + pairwise mann-whitney (between-group, benjamini-hochberg fdr).
  outputs formatted excel workbook.
  Also includes some statistical modelling (work in progress).

heatmaps.ipynb
  produces a two-panel figure per anvil (roughness and curvature) showing:
  - main plot: full anvil surface coloured by rgb, with damaged area overlaid as a
    scalar field heatmap, and a 3x3 grid overlay in gold.
  - side panels: 10 undamaged patches (k-means clustering), each reoriented to flat
    using pca before plotting so local surface tilt does not distort the 2d view.
  - shared colorbar scaled to the 5th-95th percentile range.