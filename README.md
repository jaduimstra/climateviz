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
2. Web:
	* Enter value of interest, date range
	* Generate user interactive plot


## Initial Data Exploration
#### Setup
Since we are more interested in the historical data here we only need access to the latest data on a less frequent (e.g. weekly) basis.  So rather than access the NCEI server that hosts the GHCND for each request we can use the archived data.

The data comes as a biggish (~10GB) tar.gz file consisting of a single directory with each climate observing station as a subdirectory.  The stations are coded as per the 'Station abbreviations' link above.

* Download and move the 3 Data Source files from the above links to a `data` directory
* `$ tar -ztvf <path_to_data_archive_file>/daily-summaries-latest.tar.gz > daily-summaries-directory.txt` to see what's in the data archive file
*   Explore station contents using jupyter-notebook and pandas.  My notebook is called:

	`Initial_exploration.ipynb`
	
	and I used Docker scipy-notebook image `1386e2046833` [here](https://hub.docker.com/r/jupyter/scipy-notebook/tags/), launched from this repo's root directory with:
	
	`docker run -p 8888:8888 -v "$PWD":/home/jovyan/work jupyter/scipy-notebook:1386e2046833`
	
	but you can use any Jupyter notebook configuration (e.g. local Ananconda) you chose
	
#### Results

Doing some exploration using data from two Palo Alto, California stations (__USC00046642__ and __USC00046646__) it is apparent from visual inspection that the yearly variation for e.g. _Tmax_ for a given day is quite a bit larger than any trend across years:

![Palo Alto Tmax 1922-1953](https://user-images.githubusercontent.com/11878358/66169937-f19fad80-e5f6-11e9-81c5-bd572865de73.png)

Looking specfically at _Tmin_ for 3 days (Jan 1, Feb 1, and March 1):

![Palo Alto 3 day Tmin 1954-2017](https://user-images.githubusercontent.com/11878358/66171193-25c99d00-e5fc-11e9-893f-597a88c06a2e.png)

A linear regression using seaborn's [regpplot](https://seaborn.pydata.org/tutorial/regression.html) shows a small trend in the data for the above 3 days over 63 years:

![Palo Alto 3 day Tmin 1954-2017 regression](https://user-images.githubusercontent.com/11878358/66172101-71ca1100-e5ff-11e9-9fe4-18a7feaec0ec.png)

#### Next Steps
Based on the above analysis it would be nice to have the ability to easily vary and visualize the:

* station
* day or days of the year being examined
* quantity of interest (e.g. _Tmin_, _Tmax_, etc)

A statistical analysis of the resulting data in terms of trends would also be quite useful
