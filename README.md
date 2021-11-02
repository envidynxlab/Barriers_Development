# Road networks and robustness to flooding on US Atlantic and Gulf barrier islands

This repository contains the code and instructions needed to extract the required data and explore road network robustness to coastal flooding on US Atlantic and Gulf barrier islands.

## Data
All data used in this project are open source and publicly available. To download the data, run the provided notebooks in the following order:
* Barriers.ipynb &rightarrow; With this notebook, the digitized perimeters of 702 modern barrier islands are downloaded from the semi-global database created by Mulhern et al. (2017) and available at https://hive.utah.edu/concern/datasets/cf95jb516?locale=en (Mulhern et al., 2021). From those, 184 barrier islands are located along the Atlantic and Gulf coasts of the US. 200-meter buffers are created for the US Atlantic and Gulf barrier islands to be used in the next step.
* CUDEM.ipynb &rightarrow; This notebook downloads elevation tiles from the Continuously Updated Digital Elevation Model (CUDEM), a ninth arc-second resolution bathymetric-topographic dataset developed by NOAA's National Centers for Environmental Information (NCEI) and available at https://coast.noaa.gov/htdata/raster2/elevation/NCEI_ninth_Topobathy_2014_8483/. The 200-meter buffers are used as a mask to clip CUDEM tiles and create mosaics for each barrier island. 
* Exceedance.ipynb &rightarrow; The purpose of this notebook is to calculate exceedance probabilities of extreme water levels in the US Atlantic and Gulf barrier islands using a GEV approach. For the correct use of this notebook, download the three tables provided in the "Data" section of this repository: 
  * Parameters.csv provides the GEV parameters (scale, shape, and location) for the closest NOAA CO-OPS (Center for Operational Oceanographic Products and Services) station to each barrier island (Table A in NOAA Technical Report NOS CO-OPS 067 (Zervas, 2013) available in https://tidesandcurrents.noaa.gov/publications/NOAA_Technical_Report_NOS_COOPS_067a.pdf.¶). 
  * Stations.csv lists the 112 NWLON long-term water level stations used in NOAA's report (Table 1 in the same report). 
  * MHHW.csv provides Mean Higher High Water levels for the closest station to each barrier island (manually extracted from https://tidesandcurrents.noaa.gov/est/).
 * Roads.ipynb &rightarrow; This notebook retrieves drivable road networks from OpenStreetMaps using the Python package OSMnx (Boeing, 2017). Detailed installation instructions for OSMnx package are found at https://osmnx.readthedocs.io/en/stable/. Then, each network node (road intersection) is assigned an elevation using CUDEM mosaics and the exceedance probability of extreme water events associated to that specific elevation. 

## Analysis
* Analysis.ipynb &rightarrow; The purpose of this notebook is to identify, for each barrier island, the elevation and exceedance probability of the critical node that causes the failure of the network and the overall robustness of each road network to flood-induced failures. For statistically meaningful metrics of network structure, the analysis is restricted to the 71 US Atlantic and Gulf barrier islands with drivable road networks of at least 100 nodes. In this analysis, network nodes are sequentially removed, starting from the lowest elevation, to mimic a simplified, “bathtub” flooding scenario. As nodes are deactivated, the original network (connected in a large cluster known as the giant-connected component) breaks into smaller unconnected subnetworks until its complete fragmentation. The identification of the critical node that causes the failure of each road network provides an estimation of the flood high necessary to cause the collapse of the network and the probability of occurrence of such an event. Overall network robustness, estimated by systematically measuring the summed size of the giant-connected component during the entire node removal, supplements the analysis by considering the functioning of the network even after the critical node is damaged, which  allows comparisons between barrier island road networks in terms of the entire architecture, vs. solely the elevation (and exceedance) of the single critical node.

## Requirements
Python 3.4.2
### Python packages
basemap 1.2.1
cartopy 0.18.0
colorama 0.4.4
contextily 1.1.0
fiona==1.8.18
gdal==3.2.1
geopandas 0.9.0
matplotlib 3.4.2
networkx 2.5
osmnx 1.0.1
pandas 1.2.5
rasterio 1.2.6
requests 2.25.1
scipy 1.7.0
seaborn 0.11.1
shapely 1.7.1
urllib3 1.26.7
zipp==3.4.1
Pandas 1.2.5
