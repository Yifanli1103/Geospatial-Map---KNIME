
# Geospatial Map of Blockchain Social Media Sentiments- KNIME

[![arXiv](https://img.shields.io/badge/arXiv-2409.00843-B31B1B.svg)](https://arxiv.org/abs/2409.00843)  [![Source Code](https://img.shields.io/badge/Source%20Code-GitHub-blue)](https://github.com/yukiyuqichen/GeoBlockchain)

This repository provides a **non-code-based data science workflow tutorial** using **KNIME** for replicating the geospatial maps and analyses presented in the research paper **["Global Public Sentiment on Decentralized Finance: A Spatiotemporal Analysis of Geo-tagged Tweets from 150 Countries"](https://arxiv.org/abs/2409.00843)**.

The workflow here enables users to replicate key geospatial analyses from the paper, such as generating maps that visualize sentiment toward decentralized finance across 150 countries. For users who prefer a no-code or low-code approach to data science, this repository demonstrates how to achieve the same results without the need for extensive programming knowledge.

For users interested in the **source code** and **dataset**, please refer to the complementary repository on GitHub: [GeoBlockchain](https://github.com/yukiyuqichen/GeoBlockchain).

## Overview

In the paper, the authors analyze public sentiment on decentralized finance using over 150 million geo-tagged tweets, covering 150 countries from 2012 to 2022. This KNIME workflow allows you to:

- Visualize spatiotemporal sentiment trends across different countries.
- Explore the relationship between economic factors and public engagement with decentralized finance.
- Create geospatial maps with minimal programming effort.

The KNIME platform provides a visual interface for building data workflows, making it accessible to data science enthusiasts, researchers, and practitioners with diverse technical backgrounds.

## How to Use

### Prerequisites

To replicate the results in KNIME, you will need:

1. **KNIME Analytics Platform**: Download and install the KNIME Analytics Platform from [here](https://www.knime.com/knime-analytics-platform).
2. **Access to Data**: Ensure you have access to the dataset available in the [GeoBlockchain GitHub repository](https://github.com/yukiyuqichen/GeoBlockchain).
3. **KNIME Workflow**: Download the KNIME workflow file from this repository.

### Steps

1. **Download the Workflow**: Clone or download this repository to your local machine.
   ```bash
   git clone https://github.com/sunshineluyao/Geospatial-Map---KNIME.git
   ```
2. **Open in KNIME**: Launch KNIME and import the workflow by navigating to `File > Import KNIME Workflow...`.
3. **Load Data**: Point the workflow to the required data files, which you can obtain from the complementary [GeoBlockchain repository](https://github.com/yukiyuqichen/GeoBlockchain).
4. **Run the Workflow**: Execute the workflow to generate the geospatial maps and visualizations replicating the analyses from the paper.

## Related Resources

- **Research Paper**: ["Global Public Sentiment on Decentralized Finance: A Spatiotemporal Analysis of Geo-tagged Tweets from 150 Countries"](https://arxiv.org/abs/2409.00843)
- **Source Code and Data**: [GeoBlockchain GitHub Repository](https://github.com/yukiyuqichen/GeoBlockchain)


# Introduction
## Our Paper
### Global Public Sentiment on Decentralized Finance: A Spatiotemporal Analysis of Geo-tagged Tweets from 150 Countries
![paper_overview](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Graphs/paper_overview-2.png)
Our Purposes:
* Illustrate and unfold the global imbalances in public attention and sentiments toward decentralized finance with geo-tagged tweet data
* Find out the significant factors that impact the public attention and sentiment towards decentralized finance among countries

## Platform
KNIME (Konstanz Information Miner) is an open-source software platform designed for data analytics, reporting, and integration. It is a powerful and flexible platform for data-driven tasks, suitable for both beginners and experienced data professionals. It is widely used in various industries for tasks ranging from simple data preprocessing to advanced machine learning and predictive analytics.

Key Functions
* Data Processing
* Data Visualization
* Machine Learning
* Statistical Analysis
* Text Mining

KNIME Offical Website: Click [HERE](https://www.knime.com)

# How to create a geospatial map through KNIME[3]

## Overview
![workflow_overview](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Graphs/workflow_overview.png)

## Step 1. Download the KNIME platform from the official website
![KNIME_page](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/knime_page.jpg)
Click the website link above and sign up for the KNIME community Hub. Then, go back to the main page and click the yellow bottom, saying "Download KNIME Analytics Platform". Based on your computer's system, choose the right download package. 

## Step 2. Download the Geospatial Analytics Extension Package
![extension](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/extension.jpg)
1. Once open the KNIME platform, select "menu" and click "install extensions" to direct to the search page.
![install_package](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/install_package.jpg)
2. Type "Geospatial" in the search box. Find the "Geospatial Analytics Extension for KNIME", click "NEXT" and download the extension package in our platform. After successfully downloading the package, you can start creating your geospatial workflow.

## Step 3. Creating the Workflow
### Workflow Overview:
![workflow](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/workflow.jpg)

### Step 3.1 Insert the Dataset
1.Change the name of your country variable (the column of country) into "Region" in your CSV file (see the example dataset in the data file).
![csv_reader](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/csv_reader.jpg)
2.Use the node repository on the left-hand side to search the node, typing "CSV reader". Then, drag the node to the platform.
![csv_config](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/csv_config.jpg)
3.Right click the node and select the configure to set up the node. Then, click browse and find the corresponding dataset that you want to analyze (settings are shown in the graph). After this, click apply and your dataset will be stored at the CSV reader node.

### Step 3.2 Extract the Spatial Information (Coordinate Reference System[^1])
![extraction_spatial](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/extraction_spatial.jpg)
In this step, we use a loop to iterate our extraction process of obtaining the geospatial information (Polygons) of each country. The polygon information will be stored in a Geometry type column its coordinates are expressed in degrees. The node introduction and settings are shown as follows:
* Table Row to Variable Loop Start: This node uses each row of a data table to define new variable values for each loop iteration. The names of the variables are defined by the column names.
[^1]: A coordinate reference system is a methodology to define the location of a feature in space[1].
![start_loop](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/start_loop.jpg)
* OSM Boundary Map: This node gets the place boundary from OpenStreetMap by the geocoding place name. The resulting GeoDataFrame’s geometry column contains place boundaries if they exist in OpenStreetMap (no need to configure).
* Loop End: Node at the end of a loop. It is used to mark the end of a workflow loop and collects the intermediate results by row-wise concatenation of the incoming tables.
![end_loop](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/end_loop.jpg)

### Step 3.3 Change the CRS to ESPG Codes[^2]
For easy calculation and interpretation, we change the units of measurement related to the coordinates and move from the degree system to the metric system with ESPG:3857, which can be universally used for mapping coordinates everywhere in the world, we need the assistance of the "Projection" node.
[^2]: EPSG codes are numerical identifiers assigned to coordinate reference systems and geodetic parameters to ensure consistent and accurate geospatial data management[2].
![projection](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/projection.jpg)
* Projection: This node transforms the Coordinate reference system (CRS) of the selected geometry column to the entered new coordinate reference system. The node will transform the points in all objects individually. It is based on the Geopandas project.
* Settings:
![projection_config](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/projection_config.jpg)
We choose "Replace" to replace our boundary information with ESPG codes. If you don't want to replace and only want an extra line of ESPG codes, we can choose "Append" in the setting.

### Step 3.4 Combine Our ESPG Codes With Our Original Dataset
We use the "Joiner" node to combine our ESPG codes with our original dataset.
![joiner](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/joiner.jpg)
* Joiner: This node combines two tables similar to a join in a database. It combines each row from the top input port with each row from the bottom input port that has identical values in selected columns. Rows that remain unmatched can also be output.
* Settings:
![joiner_config1](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/joiner_config1.jpg)
![joiner_config2](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/joiner_config2.jpg)
![joiner_config3](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/joiner_config3.jpg)

## Step 4. Visualize the Geospatial Map
So far we have already created a dataset with our original data and ESPG codes. Next, we need to visualize the variables in the world map. By doing this, you can choose either the "Geospatial View" node or the "Geospatial View with Static" node. Since the "Geospatial View" includes the interactive view, it needs more time to process. The "Geospatial View with Static" node generates a static map with a much faster processing speed. Based on your computer's capacity, you can choose "Geospatial View with Static" to create a map in a short time, or "Geospatial View" to create a more fancy and interactive map.
![geospatial_view](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/geospatial_view.jpg)
* Geospatial View: This node creates an interactive map view based on the selected geometric elements of the input table. It provides various dialog options to modify the appearance of the view e.g. the base map, shape color, and size. The geometric elements are drawn in the order they appear in the input table. 
* Geospatial View Settings:
![geospatial_config1](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/geospatial_view_config1.jpg)
![geospatial_config2](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/geospatial_config2.jpg)
![geospatial_config3](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/geospatial_config3.jpg)
* Geospatial View Map:
![geospatial_map](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/geospatial_map.jpg)
* Geospatial View with Static: This node will visualize the given geometric elements using the Matplotlib. It can be used to create Choropleth Maps by assigning a marker color column. The node further supports various settings to adapt the legend to your needs.
* Geospatial View with Static Settings:
![static_config1](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/static_config1.jpg)
![static_config2](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/static_config2.jpg)
* Geospatial View with Static Map:
![static_map](https://github.com/Yifanli1103/Geospatial-Map---KNIME/blob/main/Figures/static_map.jpg)

# KNIME Community Hub
You can directly download my complete workflow through my Community Hub, and click [HERE](https://hub.knime.com/-/spaces/-/~IhGFsKkfL8H5jkZE/current-state/). 

# Reference
[1] Janssen, V. (2009). Understanding coordinates reference systems, datums, and transformations. <br>
[2] International Association of Oil & Gas Producers. (2019). EPSG Geodetic Parameter Dataset. Retrieved from https://www.epsg.org. <br>
[3] KNIME. (2023, July 4). Tutorial: Geospatial analytics no code. KNIME. https://www.knime.com/blog/tutorial-geospatial-analytics-no-code. <br>
