# San Luis Obispo Canopy Cover
## Purpose
In October 2019, I participated in a graduate seminar at Cal Poly, SLO that asked the question, "How much urban canopy cover is there in San Luis Obispo?" I created this classified raster to answer this question. Results can be found in the powerpoint. 

## Methods
I used a combination of publicly available LiDAR data and NAIP imagery to identify tree canopy. 

I used [OpenTopograhy](https://opentopography.org/) to source the LiDAR data. I needed two flights to cover the extent of the City of San Luis Obispo, primarily a [2011 PG&E survey](https://portal.opentopography.org/datasetMetadata?otCollectionID=OT.022013.26910.3), and an additional [2013 PG&E survey](https://portal.opentopography.org/datasetMetadata?otCollectionID=OT.032013.26910.2). I downloaded bare earth and surface model rasters for the area of interest and combined them in QGIS. I then subtracted the surface model from the bare earth raster to create a canopy height model (CHM), providing a standardized image of all above-ground objects. After experimenting with different thresholds, I settled on 3 meters (approximately 10ft) as my cut-off for tree canopy. I reclassified the CHM to either be zero (below 3 meters), or one (3 meters or above).

I downloaded a 2012 4-band NAIP orthoimage of the city from [USGS EarthExplorer](https://earthexplorer.usgs.gov/) to help identify trees. Then, I calculated [NDVI](https://towardsdatascience.com/remote-sensing-with-qgis-calculate-ndvi-c2095f0de21b#:~:text=To%20calculate%20NDVI%20in%20QGIS%2C%20use%20the%20raster%20calculator%20to,and%20an%20installation%20of%20QGIS.) from the available bands and reclassified the raster. Values that indicated healthy photosynthesis (greater than 0.1) were reclassified as one, and values below were classified as zero. 

With both the CHM and NDVI rasters now reclassified, I added them together. Areas that were both above 10ft off the ground and photosynthetic were classified as tree canopy. Places that did not meet both conditions were classified as other. 


## Known Issues
I did not conduct an accuracy assessment, and you will need to visually inspect the raster to see if it will suit your project needs. I provide no guarantee of accuracy.

Additionally, tall power lines over green fields erroneously are classified as canopy.

Rarely, discrepancies arise when trees were removed sometime between the first lidar survey and the NAIP imagery flight. The result is a small percentage of trees are undercounted. 

Finally, new [LiDAR data](https://portal.opentopography.org/usgsDataset?dsid=CA_FEMA_Z4_B2_2018) is available, inviting someone to see the current state of canopy cover in SLO and how much has changed. 