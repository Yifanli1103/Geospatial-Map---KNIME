# ![KNIME® logo](https://www.knime.com/sites/default/files/knime_logo_github_40x40_4layers.png) KNIME® - The Geospatial Map for Geotagged Tweets Data

# Introduction
## Our Paper
### Global Public Sentiment on Decentralized Finance: A Spatiotemporal Analysis of Geo-tagged Tweets from 150 Countries
![paper_overview](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Graphs/paper_overview-2.png)
Our Purposes:
* Illustrate and unfold the global imbalances in public attention and sentiments toward decentralized finance with geo-tagged tweet data
* Find out the significant factors impact the public attention and sentiment towards decentralized finance among countries

## Platform
KNIME (Konstanz Information Miner) is an open-source software platform designed for data analytics, reporting, and integration. It is a powerful and flexible platform for data-driven tasks, suitable for both beginners and experienced data professionals. It is widely used in various industries for tasks ranging from simple data preprocessing to advanced machine learning and predictive analytics.

Key Functions
* Data Processing
* Data Visualization
* Machine Learning
* Statistical Analysis
* Text Mining

KNIME Offical Website : Click [HERE](https://www.knime.com)

# How to create a geospatial map through KNIME

## Overview
![workflow_overview](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Graphs/workflow_overview.png)

## Step 1. Download the KNIME platform from the offical website
![KNIME_page](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/knime_page.jpg)
Click the website link above and sign up for the KNIME community Hub. Then, go back to the main page and click the yellow bottom, saying "Download KNIME Analytics Platform". Based on your computer's system, choose the right download package. 

## Step 2. Download the Geospatial Analytics Extension Package
![extension](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/extension.jpg)
1.Once open the KNIME platform, select "menu" and click "install extensions" to direct to the searching page.
![install_package](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/install_package.jpg)
2.Type "Geospatial" in the search box. Find the "Geospatial Analytics Extension for KNIME", click "NEXT" and download the extension package in our platform. After successfully downloading the package, you can start create your own geospatial workflow.

## Step 3. Creating the Workflow
### Workflow Overview:
![workflow](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/workflow.jpg)

### Step 3.1 Insert the Dataset
![country_example](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/country_example.jpg)
1.Change the name of your country variable (the column of country) into "Region" in your CSV file.
![csv_reader](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/csv_reader.jpg)
2.Use the node repository on the left-hand side to search the node, typing "CSV reader". Then, drag the node to the platform.
![csv_config](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/csv_config.jpg)
3.Right click the node and select the configure to set up the node. Then, click browse and find your corresponding dataset that you want to analyze (settings are shown in the graph). After this, click apply and your dataset will be stored at the CSV reader node.

### Step 3.2 Extract the Spatial Information (Coordinate Reference System)
![extraction_spatial](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/extraction_spatial.jpg)
In this step, we use a loop to iterate our extraction process of obtaining the geospatial information (Polygons) of each country. The node introduction and settings are shown as followed:
* Table Row to Variable Loop Start: This node uses each row of a data table to define new variable values for each loop iteration. The names of the variables are defined by the column names.
![start_loop](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/start_loop.jpg)
* OSM Boundary Map: This node gets place boundary from OpenStreetMap by the geocoding place name. The resulting GeoDataFrame’s geometry column contains place boundaries if they exist in OpenStreetMap (no need to configure).
* Loop End: Node at the end of a loop. It is used to mark the end of a workflow loop and collects the intermediate results by row-wise concatenation of the incoming tables.
![end_loop](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/end_loop.jpg)

### Step 3.3 Change the Geometry Column Contains Place Boundaries Into ESPG Codes
To replace our place boundaries with ESPG codes, which can be universally used for mapping coordinates everywhere in the world, we need the assistance of "Projection" node.
![projection](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/projection.jpg)
* Projection: This node transforms the Coordinate reference system (CRS) of the selected geometry column to the entered new coordinate reference system. The node will transform the points in all objects individually. It is based on the Geopandas project.
* Settings:
![projection_config](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/projection_config.jpg)
We choose "Replace" to replace our boundaries information with ESPG codes. If you don't want to replace and only want an extra line of ESPG codes, we can choose "Append" in the setting.

### Step 3.4 Combine Our ESPG Codes With Our Original Dataset
