# pangeo in relation to CMR

## CMR is the NASA **Common Metadata Repository**

### Introduction

This repo asks (answers) pangeo-centric questions... 


> **NASA intends the pangeo project will support access to earth remote sensing data (and related)
via the public cloud and technologies built thereupon. This involves organized/automated 
computing horsepower and infrastructure. In turn this begs a number of questions, foremost
'What is the learning process that enables a scientist to take advantage of both pangeo and CMR?' 
Jointly 'What does this pantheon of data look like?' and 'Are there other comparable resources
(type, style, scope) to be aware of?'**


This repo begins with 'How to access metadata from the NASA CMR from a Jupyter notebook?' 
We use the python-cmr package and build the notebooks in a science/tutorial manner. From
that starting point we expand out to the NASA data ecosystem, starting with...

* CMR
* GIBS: (NASA) Global Image Browser System
* EOSDIS
* DAACs: [NASA Distributed Active Archive Centers](https://nssdc.gsfc.nasa.gov/earth/daacs.html).
* MEaSUREs
* [Giovanni](http://giovanni.gsfc.nasa.gov/giovanni/): A Goddard Space Flight Center data application


From there we proceed to...

* NASA-external platforms for working with NASA-generated data like LANDSAT 
  * [Google Earth Engine (GEE)](https://earthengine.google.com)
  * AWS hosting of LANDSAT 
  * Jupyter Hubs
  * GOLIVE / ITSLIVE Land Ice Velocity and Elevation derived data products
* NASA-external data sources
  * [Planet](https://www.planet.com).
* Web Mapping Services
  * Includes map controls like **ipyleaflet**


### Links


* [Jupyter notebook editing shortcuts](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)
* [CMR](https://earthdata.nasa.gov/about/science-system-description/eosdis-components/common-metadata-repository)
* [GIBS](https://pypi.python.org/pypi/python-cmr/0.3.1)
* [Python-CMR](https://pypi.python.org/pypi/python-cmr/0.3.1)
* [NEP NASA Earth Observations WMS resource page](https://neo.sci.gsfc.nasa.gov/about/wms.php)



### Note on WMS
Search 'NASA WMS' to find NASA (often Goddard) Web Mapping Services. 
Add some as layers to an ipyleaflet Map: In a perfect world this works well...
but in reality we need some guidance on GetCapabilities and layer qualifiers and how to debug bad layers.)


### Datasets of interest

* Anything that comes out of the python-cmr interface query
* GOLIVE and its successor ITSLIVE are two surface ice velocity products at NSIDC
