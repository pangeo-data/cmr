# [icesat2](https://icesat-2.gsfc.nasa.gov)

Notes from the [Icesat-2](https://icesat-2.gsfc.nasa.gov) hackweek at UW June 17 - 21 2019. 
While NASA-Goddard is managing the mission the Icesat2 data products are
described at the [NSIDC DAAC](https://nsidc.org/data/icesat-2/products). 

The data system is called ATLAS and it is the Level 6 data product ATL06 that we focus on here. 
They are archived by day (folders) with typical HDF5 files spanning some number of seconds with 
file volumes from a few to upwards of 100MB.

## order data, place on S3 

This procedure gets 60 HDF5 Icesat-2 files into my Jupyter environment; and then copies them to a folder
on the AWS cloud. This could be consolidated to a single step straight to the cloud but I want to explore
the data hence my Jupyter-local copy. 

* go to the [NSIDC icesat2 data portal](https://nsidc.org/data/icesat-2/products)
* left sidebar: ICESAT2 Datasets
* in the table: ATL06 link
* **earthdata Search** link (sign in)
* use the map interface to outline a polygon (last click on first click marker to close)
  * a region the size of the Juneau icefield gave about 60 granules
* download all results; choose direct download; Download Data button
* Order status page: Click on **View/Download Data Links** to get a list of granule URLs
* Copy this list of URLs; transfer to a text file (I edit from the Jupyter terminal using `vi`)
  * Each line of this file will be a `wget` command in this format:
  
```
wget https://n5eil...etcetera.h5 --user <username> --password <password><space>
```
  * The `<space>` is simply a trailing space character 
  * Hence to build this script file: 
    * prepend `wget` on each line 
    * append `--user user --password pass ` (note trailing space)
    * ***Pro Tip: Take care not to commit this file to a git repo as it contains a working password***
  * run the file using `source <scriptfile>`. This will pull in the data files to the current working directory
  

The above procedure writes data files (`.h5`) into the Jupyter pod. Nothing up to this point has touched the 
AWS (Amazon Web Services) public cloud. The next step writes data to an S3 bucket. Either you will be able to write 
the data across using the AWS command line or you won't. In the latter case the probable cause involves authentication 
keys, not covered here. 

* In the Jupyter terminal go to the directory that contains the data to copy to the cloud
* Identify the S3 bucket where the data is to be sent
* Identify the folder path *within* that S3 bucket
  * This need not exist yet; it will be created automatically during transfer
  * For this example the bucket is `pangeo-data-upload-oregon` and the folder is `icesat2/juneauicefield`
* Now issue this command...

```
aws s3 sync ./ s3://pangeo-data-upload-oregon/icesat2/juneauicefield
```

This may finish very quickly. To verify success issue the following, taking care to include the final `/` character:

```
aws s3 ls s3://pangeo-data-upload-oregon/icesat2/juneauicefield/
```


