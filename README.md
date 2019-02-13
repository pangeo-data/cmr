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
  * ...and Damien's related [AOS tutorials](https://carpentrieslab.github.io/python-aos-lesson/)
* [EarthML](http://earthml.pyviz.org/index.html)
* [Research Computing in Earth Sciences course](https://rabernat.github.io/research_computing_2018/) by Ryan Abernathy
* [pangeo cmr repo](https://github.com/pangeo-data/cmr)
  * ...including [**GOLIVE**](https://nsidc.org/data/NSIDC-0710) ice velocity notebooks 
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
* [STAC catalog program](https://github.com/radiantearth/stac-spec)


#### External resources


* NASA-external platforms for working with NASA-generated data like LANDSAT 
  * [Google Earth Engine (GEE)](https://earthengine.google.com)
  * [AWS hosting of LANDSAT](https://registry.opendata.aws/landsat-8/) 
  * Jupyter Hubs
  * [GOLIVE](https://nsidc.org/data/NSIDC-0710) / ITSLIVE Land Ice Velocity and Elevation derived data products
* NASA-external data sources
  * [Planet](https://www.planet.com)
  * [Polarhub]( http://polar.geodacenter.org/polarhub) is Wenwen Li's cryo crawler
* Web Mapping Services
  * Includes map controls like **ipyleaflet**
  * Search 'NASA WMS' to find NASA (often Goddard) Web Mapping Services. 
    * Add to ipyleaflet Map; GetCapabilities and layer qualifiers help needed


#### More Tactics

As I am running into debugging issues I'm recording some installation steps on an EC2 instance 
with the idea of using an AMI to grab horsepower/RAM/disk space as needed. 

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
rm Miniconda3-latest-Linux-x86_64.sh
```

This install miniconda. Then we have an environment config/activate:


```
conda create -n golive python=3.6
conda activate golive
```

...and `requirements.txt`...

```
boto3==1.9.78
obspy==1.1.0
Pillow==5.4.1
```


...and some package installations not in the requirements...


```
conda install pandas
conda install netcdf4
conda install xarray
conda install ipywidgets
```
