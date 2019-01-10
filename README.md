# pangeo in relation to CMR

## CMR is the NASA **Common Metadata Repository**

### Introduction

This repo asks (answers) some pangeo-centric questions... 


> **NASA intends the pangeo project will support access to earth remote sensing data (and related)
via the public cloud and technologies built thereupon. This involves organized/automated 
computing horsepower and infrastructure. In turn this begs a number of questions, foremost
'What is the learning process that enables a scientist to take advantage of both pangeo and CMR?' 
Jointly 'What does this pantheon of data look like?' and 'Are there other comparable resources
(type, style, scope) to be aware of?'**


We begin in the notebooks with basic tactics; basically *How to access metadata from the NASA CMR from a Jupyter notebook?*
However this repo is really a higher-level effort to get our collective arms around the learning and adoption process, by example.
We have links to outreach efforts such as Damien Irving's excellent software carpentry sequence on Python for Ocean and
Atmospheric Sciences. We provide Python notebooks that demonstrate a set of useful tools applied to various data resources. 



### Links

#### Education and Outreach 


* [Damien Irving oceanography data carpentry blog](https://datacarpentry.org/blog/2018/09/atmos-ocean-launch)
  * Related [AOS tutorials](https://carpentrieslab.github.io/python-aos-lesson/)
* [EarthML](http://earthml.pyviz.org/index.html)
* [pangeo cmr repo](https://github.com/pangeo-data/cmr)
* [**GOLIVE**](https://nsidc.org/data/NSIDC-0710) ice velocity notebooks are present in this repo
* [Jupyter notebook editing shortcuts](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)
* [Giovanni](http://giovanni.gsfc.nasa.gov/giovanni/) data discover application from Goddard



#### Organizations


* [pangeo](https://pangeo.io/)
* [Ocean pangeo](https://github.com/raphaeldussin/example.pangeo.io-deploy)
* [Atmos pangeo](https://github.com/pangeo-data/atmos.pangeo.io-deploy)


* [EOSDIS](https://earthdata.nasa.gov/about) the NASA Earth Observing System Data Information System
* [CMR](https://earthdata.nasa.gov/about/science-system-description/eosdis-components/common-metadata-repository)
* [GIBS](https://pypi.python.org/pypi/python-cmr/0.3.1) for browsing NASA imagery
* [NASA Distributed Active Archive Centers](https://nssdc.gsfc.nasa.gov/earth/daacs.html)
* [MEaSUREs]()https://earthdata.nasa.gov/community/community-data-system-programs/measures-projects)
* [EarthML](http://earthml.pyviz.org/index.html)


#### Tech and Tactics


* [Python-CMR](https://pypi.python.org/pypi/python-cmr/0.3.1)
* [NEP NASA Earth Observations WMS resource page](https://neo.sci.gsfc.nasa.gov/about/wms.php)


#### External resources


* NASA-external platforms for working with NASA-generated data like LANDSAT 
  * [Google Earth Engine (GEE)](https://earthengine.google.com)
  * AWS hosting of LANDSAT 
  * Jupyter Hubs
  * GOLIVE / ITSLIVE Land Ice Velocity and Elevation derived data products
* NASA-external data sources
  * [Planet](https://www.planet.com)
* Web Mapping Services
  * Includes map controls like **ipyleaflet**
  * Search 'NASA WMS' to find NASA (often Goddard) Web Mapping Services. 
    * Add to ipyleaflet Map; GetCapabilities and layer qualifiers help needed

