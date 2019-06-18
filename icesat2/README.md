# [icesat2](https://icesat-2.gsfc.nasa.gov)

Notes from the [Icesat-2](https://icesat-2.gsfc.nasa.gov) hackweek at UW June 17 - 21 2019. 
While NASA-Goddard is managing the mission the Icesat2 data products are
described at the [NSIDC DAAC](https://nsidc.org/data/icesat-2/products). 

The data system is called ATLAS and it is the Level 6 data product ATL06 that we focus on here. 
They are archived by day (folders) with typical HDF5 files spanning some number of seconds with 
file volumes from a few to upwards of 100MB.

## order data, place on S3 

This procedure is unnecessarily cumbersome and should be consolidated to a single AWS script. My example
here pulls files from NSIDC to a Jupyter notebook pod and then writes them to S3. 

* go to the NSIDC data portal
* go to the **earthdata** browser (you will need to sign in)
* use the map interface to outline a polygon (last click on first click marker to close)
  * a region the size of the Juneau icefield gave about 60 granules
* choose a direct download
* click **View Download Data Links** to get a list of URLs
* copy that into a text file using a Jupyter terminal
  * prepend `wget` on each line
  * append `--user user --password pass`
    * Please take care not to commit this file to a repo if it contains a working password
  * source the file: This pulls in 100MB x n_files files
  
This places a bunch of data files (`.h5`) in the Jupyter pod. Nothing up to this point has touched on the Amazon Web Services
public cloud. The next step writes data to an S3 bucket. Either you will be able to write the data across using the AWS
command line or you won't. In the latter case the probable cause involves authentication keys. 

* In the Jupyter terminal go to the directory that contains the data to copy to the cloud
* identify an S3 bucket for the data to land in. 
  * It need not include the folder path; that will be created automatically
* In the case of this data here is the command

```
aws s3 sync ./ s3://pangeo-data-upload-oregon/icesat2/juneauicefield
```

This may run very quickly. To verify success issue the following, taking care to include the final `/` character:

```
aws s3 ls s3://pangeo-data-upload-oregon/icesat2/juneauicefield/
```


