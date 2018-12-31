# pangeo in relation to CMR

## CMR is the NASA Common Metadata Repository


### Introduction

This repo asks a broad pangeo-centric question... 


> **Whereas NASA supoorts this work to promote access to earth remote sensing data, and 
> whereas in pangeo we have organized/automated computing horsepower and infrastructure... 
> what is the learning process and combination of tutorials that enables a newcomer to do
> productive research using those data? 
> And what does this NASA-driven pantheon of data look like? 
> Are there other resources with comparable type, style and scope to be aware of?**


In less grandiose manner we begin here with the NASA CMR (Common Metadata Repository) and code in a 
Jupyter notebook. **CMR** is ideally 'one stop shopping' for metadata on NASA remote sensing resources (earth only).
The CMR API is accessible via the python-cmr package; so we examine this here.


Also of interest is **GIBS**, NASA's Global Image Browser System, ideally one-stop shopping for imagery.
We also want to understand the relationship between **CMR**, **GIBS** and 
[NASA Distributed Active Archive Centers (DAACs)](https://nssdc.gsfc.nasa.gov/earth/daacs.html).


Other NASA projects have produced particular portals. Goddard Space Flight Center (GSFC) 
via GES DISC (Goddard Earth Science Data and Information Services Center)
has produced a data web app called [Giovanni]( http://giovanni.gsfc.nasa.gov/giovanni/). 
So let's cover that. 


What about NASA-external platforms for working with NASA-generated data like LANDSAT? 
We have in mind [Google Earth Engine (GEE)](https://earthengine.google.com) 
as well as AWS hosting of LANDSAT data, to begin with. 


What about non-NASA remote sensing resources? We have in mind [Planet](https://www.planet.com).


InSAR.


Web Mapping Services. Including maps in Jupyter notebooks whereupon to place such tiles?



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
