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


### Initial Data Exploration
Since we are more interested in the historical data here we only need access to the latest data on a less frequent (e.g. weekly) basis.  So rather than access the NCEI server that hosts the GHCND for each request we can use the archived data.

The data comes as a biggish (~10GB) tar.gz file consisting of a single directory with each climate observing station as a subdirectory.  The stations are coded as per the 'Station abbreviations' link above.

* Download and move the 3 Data Source files from the above links to a `data` directory
* `$ tar -ztvf <path_to_data_archive_file>/daily-summaries-latest.tar.gz > daily-summaries-directory.txt` to see what's in the data archive file
*   Explore station contents using jupyter-notebook and pandas.  My notebook is called:

	`Initial_exploration.ipynb`
	
	and I used Docker scipy-notebook image `1386e2046833` [here](https://hub.docker.com/r/jupyter/scipy-notebook/tags/), launched from this repo's root directory with:
	
	`docker run -p 8888:8888 -v "$PWD":/home/jovyan/work jupyter/scipy-notebook:1386e2046833`
	
	but you can use any Jupyter notebook configuration (e.g. local Ananconda) you chose
	
