# Overview

**Goal** 
The goal of this project is to use the city of Chicago's rideshare data 
(11.3 GB) found at data.cityofchicago.org to make a heatmap of traffic in chicago 
caused by various rideshare companies.

**Method** 
Our method is to use 5 columns of the data (Trip Start Timestamp, Pickup
Centroid Latitude, Pickup Centroid Longitude, Dropoff Centroid Latitude, Dropoff
Centroid Longitude) and use google cloud and MapReduce to cluster the trips 
that have identical trip start timestamps and that also intersect meaning their 
pickup and dropoff locations form line segments that cross. Once we have this 
tree structure, which is a sorted key,value structure where the key is the date
and time and the values are the intersection points, we create convert the output
JSON to a pandas dataframe and use folium to imput the intersection points 
organized by date and then by time to create 2 heatmap HTML's depicting the 
heatmap of traffic in Chicago for each hour of the day and for each day of the week.

**Files** 
* #Day heatmap.html - HTML file for the heatmap with days as indices
* #Time heatmap.html - HTML file for the heatmap with hours as indices
* Heatmap.ipynb - Jupyter notebook file with code converting JSON file output from mapreduce to heatmap
* Convert.py - Converts JSON to pandas
* Geo.csv - CSV file containing coordinates to make map of Chicago
* medium.json - JSON file output from google cloud dataproc on "medium" amount (about 1,000,000 rows) of the data
* mr_time_geo.py - MapReduce function to use with cloud 

**Limitations**
For security reasons, the data only includes Census track centroid pickup and 
dropoff coordinates. This means we are only able to get at best within about
an 89,000 square foot radius of the actual pickup and dropoff locations so our 
intersection coordinates are not exactly accurate. Also, the timestamps are rounded
to the nearest 15 minutes.

# Features
* Cloud-Computing/Dataproc
* MapReduce
* Data Visualization

# Technologies
* Python 3.5
* MrJob - MapReduce
* Bintrees - Tree structure used in reducer to yield data in sorted key order
* Shapely - Analyze geometric objects (line segment intersections)
* Folium - Data Visualization/HeatMap

# Authors
* Tyson Miller
* Thomas Wilson
* Matt Auerbach
