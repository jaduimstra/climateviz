# ClimateViz

### ClimateViz Aim:

* Visualize data to answer the question:

*It seems warmer/colder/rainier/etc recently compared to the last few years/when I was younger.*

### Data Source: Global Historical Climatology Network Daily
* [GHCND data](https://www.ncei.noaa.gov/data/global-historical-climatology-network-daily/archive/)
* [GHCND data documentation](https://www.ncei.noaa.gov/data/global-historical-climatology-network-daily/doc/GHCND_documentation.pdf)
* [Station abbreviations](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/ghcnd-stations.txt)
* [Station abbreviation readme](https://www1.ncdc.noaa.gov/pub/data/ghcn/daily/readme.txt)

### ClimateViz UI proposal
1. jupyter notebook:
	
	* 3D plot of given value (e.g. Max Daily Temp, Precipitation Amount) over a range of years plotted on a daily basis
	* __STATUS: Done__.  [Conclusion](Initial_Exploration.md) is that the yearly variation for e.g. _Tmax_ for a given day is quite a bit larger than any trend across years.  So we need to be able to both visualize trends and regressions/statistical analyses of the data in section 2 below
2. App:
	* Enter value of interest, date range
	* Generate user interactive plot

### App Architecture
Further examination of the GHCND data using `database_setup.ipynb` shows the following:

* 114789 unique stations
* 421 unique 3 letter station prefixes
* 109648 of the stations are represented in just 20 station prefixes
* Just focusing on __USC__ stations gives 22480 stations
	* At 100 years of data per station that's 100 x 365 x 22480 = ~820 million rows of data.  Doable for a single table but perhaps not the best idea for the proof of concept app

As an alternative for a prototype visualization a couple of approaches could be taken:

1. Focus on data from a list of cities, such as [Natural Earth Cities](http://www.naturalearthdata.com/downloads/10m-cultural-vectors/)
    * Then use an algorithm (or perhaps just pick the largest file) to select a data station for a given city within a certain radius of that city
2. Only focus on a region of interest that is smaller than the full US (e.g. California)

### Next Steps
* [ ] Build a GIS database using e.g. PostGIS to allow easy spatial queries of the _Stations_ data
* [ ] Using the database, select a subset of U.S. stations and load those daily data into new tables in the database
