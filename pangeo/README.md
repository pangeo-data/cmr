# How pangeo works

I am a Researcher; so *why* do I want to work in the pangeo environment? 
And *how* does the pangeo environment come together? Notes to build context and skills: 

**pangeo pillars of existence**

- Foster collaboration around the open source scientific python ecosystem for ocean / atmosphere / land / climate science
- Support the development with domain-specific geoscience packages
- Improve scalability of these tools to handle petabyte-scale datasets on HPC and cloud platforms 


Pillar 3 is where effort is focused today. 


Now here is an axiomatic view... and then we carry on with tactics

- I want to work in a Jupyter notebook...
  - ...in fact a JupyterLab notebook (feature-rich extension of Jupyter notebooks)
  - ...hosted in a JupyterHub environment (supports multiple users)
  - ...that connects with the NASA catalog (CMR via Intake-STAC)
- I want to operate on some fairly large remote sensing datasets...
  - ...and produce non-trivial results; preserving my code and tools I used
  - Example: Golive: 10 scalar fields (including acceleration) over large glaciated regions (400 km x 400 km)
  - Example: TRMM latent heat profile work on pole-ward energy transport
  - Example: Synoptic: Ocean state data from several disparate sources including MODIS
- In consequence I need 
  - A kubernetes cluster on standby
  - A pangeo JupyterHub 
  - Proper authentication/security
  
## Context 1: Companies Anaconda, GitHub, Binder, CircleCI


pangeo depends on services provided at no cost


- ***Anaconda*** builds and maintains a Python package manager called `conda`
- ***Github*** hosts public repos under the git system: Organized by individual (me) or organization
- ***Binder*** hosts a limited-duration executable instance of a Jupyter notebook GitHub repo
- ***CircleCI*** executes a task sequence in a self-hosted container in response to an API call


## Context 2: pangeo deployment narrative 

- I create a Kubernetes cluster **KC** 
  - This is represented by a head node and a capacity plan: For spinning up additional cloud resources
- We have a GitHub organization *pangeo-data* and a repo *pangeo-cloud-federation* 
  - This repo will be responsible for multiple pangeo JupyterHub instances
    - Two exist ('**Alpha**' and '**Bravo**') and I wish to add '**Charlie**'
    - I Fork the entire repo to my own GitHub account; working in the `staging` branch
      - ...and I clone this fork to my local computer for ease of modification; I will push commits directly to the fork
    - In the `deployments` folder I go from **Alpha** to a new pangeo instance **Charlie**: By copying the **Alpha** folder
      - In **Charlie** I go to the `image` folder which represents my work environment
        - Note there are folders `config`, `image`, `secrets` and 'README.md`
        - In `image` the folders are `.dask` and `binder` plus `.ipynb` files, `.gitignore` and `README.md`
          - `.dask` contains `config.yaml` which describes a kubernetes dask worker... 
          - This is cloud-vendor agnostic
        - It is possible to invent the `image` contents out of whole cloth; for example pulling from another repo
          - With Scott we pulled from [this esip tech dive repo](https://github.com/scottyhq/esip-tech-dive)
          - This overwrite of the default content did not include copying `.git` or `.gitignore`
          - Then be sure to modify `README.md`
        - Moving from `/image` to `/binder` we find environment configuration material
          - `apt.txt` installs additional Linux packages
          - `environment.yml` is the conda packages to install
          - How do we generate this file from some environment?
            - % conda activate esip-tech-dive
            - % conda list
            - % conda env export -f environment.yml

- same folder jupyterlab-workspace.json supports jupyterlab. 
- the postBuild script has the stuff to extend jupyter notebook to jupyter lab
- repo2docker will read these files and create the docker image with all this stuff. 
- hubploy calls the repo2docker api. 
- hubploy is called by circle.ci


# Notes on hubploy / pangeo builder


* [hubploy on github](https://github.com/yuvipanda/hubploy)

```
% aws eks update-kubeconfig --name $CLUSTER_NAME
```

GCP key in deployments/dev/secrets/gcloud-service-key.json:

```
{
  "type": "service_account",
  "project_id": "myproject",
  "private_key_id": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "private_key": "-----BEGIN PRIVATE KEY-----\nXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX\n-----END PRIVATE KEY-----\n",
  "client_email": "mykey@myproject.iam.gserviceaccount.com",
  "client_id": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/mykey%40myproject.iam.gserviceaccount.com"
}
```
