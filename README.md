# TAZ-polygon-and-centroid-geometry
Instruction to find TAZ data and prepare TAZ polygon geometry and centroid longitude and latitude in WKT format.

Three files are required for processing dynamic traffic assignments, TAZ.csv, node.csv, and link.csv. In the classic version of DTALite, the zone-to-node mapping is specified in node.csv through the field of zone_id, as Figure 1 shown. However, there is a challenge when mapping TAZ-based information to the network at different resolutions.
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_1.png)
<p align="center">Figure 1 node.csv</p> 


Thus, in the preprocessing stage, we allow users to prepare (1) TAZ with boundary information, and then (2) DTALite will generate the zone.csv as an explicit mapping between zone_id and access node vector. Then users can still manually edit the accesss_node_vector to refine the zone-to-node mapping in zone.csv

In the assignment stage, DTALite reads the zone-to-node mapping from zone.csv or node.csv, and reads the related OD demand table (defined in terms of o zone id and d zone id) to assign the OD volume to different routes connecting the origin activity node to the destination activity node.

This guide provides an instruction to help users prepare the TAZ.csv (take Alabama as an example). 


## Step 1 Download census shapefiles of Alabama on the [DATA.GOV](https://catalog.data.gov/dataset) 

In addition, we summarize the other two websites to download shapefiles: 1) we can use census tracts as TAZs, the shapefiles of census tracts for all US states are available [here](https://www.census.gov/cgi-bin/geo/shapefiles/index.php?year=2021&layergroup=Census+Tracts) and 2) for some counties/cities, for example, Phoenix, can be found [here](https://koordinates.com/layer/96425-phoenix-arizona-census-tracts-2010/). 

### 1. Search the Census data.
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_2.png)
<p align="center">Figure 2 TAZ census data of Alabama</p> 

### 2. Download one dataset which includes a .shp file.
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_3.png) ![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_4.png)
<p align="center">Figure 3 TAZ census data of Alabama</p> 

## Step 2 Use QGIS to export TAZ shapefile as TAZ.csv

### 1. Right-click the TAZ layer -- "Export"-- "Save Features As"
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_5.png)
<p align="center">Figure 4 Visualization of TAZ polygons</p> 

### 2. Save the features as TAZ.csv
a.	Set up the Format as CSV, and the CRS as WGS 84;
b.	Select fields of "TAZCE10", "INTPTLAT10" and "INTPTLON10"  to export;
c.	Set up the Geometry type as Polygon;
d.	Select the format of GEOMETRY;
e.	OK
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_6.png)
<p align="center">Figure 5 Export TAZ polygons</p> 

### 3. Change the fields' name of "WKT", "TAZCE10", "INTPTLAT10" and "INTPTLON10" as " geometry", "TAZ", "y_coord", and "x_coord " repectively.
![image](https://github.com/FangTang999/TAZ-polygon-and-centroid-geometry/blob/main/image/Fig_7.png)
<p align="center">Figure 6 Change the field name</p> 

**Note**: we need to use a text editor to open the TAZ.csv, since there could be some display errors if we use Excel to open it due to the limitation of string length.
