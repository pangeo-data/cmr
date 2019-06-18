# [icesat2](https://icesat-2.gsfc.nasa.gov)

Notes from the [Icesat-2](https://icesat-2.gsfc.nasa.gov) hackweek at UW June 17 - 21 2019. 
While NASA-Goddard is managing the mission the Icesat2 data products are
described at the [NSIDC DAAC](https://nsidc.org/data/icesat-2/products). 

The data system is called ATLAS and it is the Level 6 data product ATL06 that we focus on here. 
They are archived by day (folders) with typical HDF5 files spanning some number of seconds with 
file volumes from a few to upwards of 100MB.

## get data 

This procedure is unnecessarily cumbersome and should be consolidated to a single AWS script. My example
here pulls files from NSIDC to a Jupyter notebook pod and then writes them to S3. 

* go to the NSIDC data portal
* go to the **earthdata** browser
* use the map interface to outline a polygon (last click on first click marker to close)
  * a region the size of the Juneau icefield gave about 60 granules
* choose a direct download
* click **View Download Data Links** to get a list of URLs
* copy that into a text file using a Jupyter terminal
  * prepend `wget` on each line
  * append `--user user --password pass` 
  * source the file: This pulls in 100MB x n_files files
* configure the AWS command line using `aws configure` 
  * enter a public key and a private key
* identify an S3 bucket for the data


