# Outreach: Draft articulation of how pangeo works

I am a Researcher with a moderately ambitious interest in understanding *why* I want to work in the pangeo environment
and *how* the pangeo environment comes together. To build the context: First a reminder of the three pangeo pillars; 
and then a narrative. 

**pangeo**

- Foster collaboration around the open source scientific python ecosystem for ocean / atmosphere / land / climate science
- Support the development with domain-specific geoscience packages
- Improve scalability of these tools to handle petabyte-scale datasets on HPC and cloud platforms 


The latter is where much of the horsepower is focused today. As this has become a reality -- including pangeo 
instances -- the opportunity to build the community and support domain-specific package development has grown 
more acute (not to be obtuse). So as a Researcher we state the following axiomatic position...


- I want to work in a Jupyter notebook...
  - ...in fact a JupyterLab notebook which is a feature-rich extension
  - ...that is hosted in a JupyterHub environment
- I want to operate on some fairly large remote sensing datasets...
  - ...to produce some non-trivial results; and produce those tools I built and used to produce them!
  - Example: TenByGolive: 10 scalar fields (including acceleration) over large glaciated regions (400 km x 400 km)
  - Example: Synoptic: Ocean state data from several disparate sources including MODIS
  
## What are these companies: Anaconda? GitHub? Binder? CircleCI? 

- A company that hosts public repos under the git system: Organized by individual (me) or organization
- A company that will host a limited-duration executable instance of a Jupyter notebook GitHub repo
- A company that executes a task sequence in a self-hosted container in response to an API call

## What is the pangeo deployment narrative? 

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
