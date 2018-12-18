# pangeo in relation to CMR

## CMR is the NASA Common Metadata Repository


### Introduction

This repo in broad strokes asks a pangeo-centric question: 


> **So NASA is funding this work to help promote access to their earth remote sensing data, potentially involving 
> the public in some capacity. In pangeo we have tremendous
> computing horsepower and organizing infrastructure... so how do we bring that to bear, with very 
> specific examples please? And for that matter what does this NASA pantheon of data look like? And are there other resources
> of comparable type style and scope that we might also want to be aware of???**


This repo in less grandiose terms looks into the NASA CMR (Common Metadata Repository) data sources via Jupyter notebook. 
**CMR** is hypothetically 'one stop shopping' for metadata on NASA remote sensing resources (earth only).
The CMR API is accessible via the python-cmr package; so we will look at that a bit here. This is our starting point.


Since this is NASA you are wondering 'how much longer before the acronym deluge begins?' and the answer
is of course 'Zero'. As in 'Zero longer'. **GIBS** is a related system, NASA's Global Image Browser System, 
which is hypothetically one-stop shopping for imagery. We'll consider **GIBS** to be a stretch topic.


Other NASA projects have produced different bespoke portals. For example Goddard Space Flight Center (GSFC) 
via GES DISC (Goddard Earth Science Data and Information Services Center)
has produced a data web app called [Giovanni]( http://giovanni.gsfc.nasa.gov/giovanni/). So we need a picture of
all that, circa 2019. 


What about NASA-external platforms for working with NASA-generated data like LANDSAT? 
We have in mind [GEE](https://earthengine.google.com) and AWS hosting of LANDSAT data and so on. So that's a topic. 


What about non-NASA remote sensing resources? We have in mind [Planet](https://www.planet.com). So that's a topic. 


What about InSAR? Another topic.


What about using WMSii (the only good plural of WMS)? And including maps in Jupyter notebooks whereupon to place such tiles?


Ok so with that, plenty to think about, let's paste in a few...

### Links

* [Jupyter notebook editing shortcuts](https://www.dataquest.io/blog/jupyter-notebook-tips-tricks-shortcuts/)
* [CMR](https://earthdata.nasa.gov/about/science-system-description/eosdis-components/common-metadata-repository)
* [GIBS](https://pypi.python.org/pypi/python-cmr/0.3.1)
* [Python-CMR](https://pypi.python.org/pypi/python-cmr/0.3.1)
* [NEP NASA Earth Observations WMS resource page](https://neo.sci.gsfc.nasa.gov/about/wms.php)



\* but note: It is possible to search for 'NASA WMS' to find NASA (often GSFC) Web Mapping Services. These can be 
added as layers to an ipyleaflet Map. (To do: Restore notes on GetCapabilities and layer qualifiers and whether
a particular resource works well or not... and how to debug bad layers.)

