# How pangeo works

I am a Researcher; so *why* do I want to work in the pangeo environment? 
And *how* does the pangeo environment come together? These notes help you the Researcher
understand **pangeo** the geoscience platform. 


The quick answer is: You may want a JupyterLab environment available to your community of scientists 
that is (a) always available online (b) cost-effective (c) loaded with the packages, tools and tech
you need for your research (d) connected to vast data resources in the public cloud and (e) at a 
moment's notice is capable of expanding into a compute cluster to do large calculations quickly.


If you **do** want this: Look for a pangeo deployment to join and use. **OR** if it makes sense to
invest the time and effort you can deploy your own. This as you might imagine is a bigger undertaking; 
and it may involve paying for supporting resources on the public cloud.



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
  
  
## Context 1: Companies Anaconda, GitHub, Binder, CircleCI, Docker


pangeo depends on services/tech provided at no cost


- ***Anaconda*** builds and maintains a Python package manager called `conda`
- ***Github*** hosts public repos under the git system: Organized by individual (me) or organization
- ***Binder*** hosts a limited-duration executable instance of a Jupyter notebook GitHub repo
- ***CircleCI*** executes a task sequence in a self-hosted container in response to an API call
- ***Docker*** is containers, images, stuff like that


## Context 2: pangeo deployment narrative 

- Someone creates a Kubernetes cluster **KC**, a latent resource of processing power
  - This is a cloud resource that can be shared by multiple pangeo instances ('deployments') as described below
  - A head node is always on at minimal cost; and then other machines spin up / down based on demand
  - The cluster has capacity rules: For spinning up additional public cloud instances (VMs)
  - When scientists are authenticated onto the system they can start tasks that spin up resources
  - When the system goes idle the resources are de-allocated; back to a quiescent state
  
  
- There is a GitHub organization *pangeo-data* and a 
repo [*pangeo-cloud-federation*](https://github.com/pangeo-data/pangeo-cloud-federation)
  - This repo is supported by a separate [pangeo deployment repo](https://github.com/Element84/pangeo-deployment)
  - The *federation* repo will be causal for multiple pangeo JupyterHub instances
    - Abstractly: Suppose three exist, `Alpha`, `Bravo` and `Charlie` and we wish to add `Delta`
    - I Fork the `pangeo-cloud-federation` repo to my GitHub account; where I will work in the `staging` branch
      - I can also `git clone` my Fork to a local machine (easier to modify) 
        - I `push` commits up to the Fork
      - I do Pull Requests from my Fork to the `pangeo-cloud-federation` repo


> ***PRO TIP:*** The pangeo JupyterHub provides a container environment where I develop Jupyter Notebooks... 
So far so good. Now suppose I fire off some task that makes use of `dask` (perhaps a big processing job). 
Pangeo will allocate `dask workers` that are clones of my default container environment. So I can modify
that environment for example using `conda install` but this may make my environment incompatible with the
`dask` worker clones. To maintain that compatibility we modify the configuration of the pangeo deployment; 
and then redeploy it. pangeo is designed to be redeployed easily so that this process is not painful. 


The narrative continues...


- From the pangeo-data organization
  - From the pangeo-cloud-federation repo (Fork) we have a folder called `deployments`
    - Delta build: In the `deployments` folder I create folder `Delta` as a copy of folder `Bravo`.
      - Here are sub-folders `config`, `image`, `secrets` and there are files `README.md` and `hubploy.yaml`.
        - In practice you customize all contents of `Delta` 
        - Then do a PR to build the `Delta` pangeo JupyterHub
      - `Delta/image` represents the scientists' working environment. It could be built from scratch as well...
        - For example: Pull from another repo
          - Such as from [this ESIP tech dive repo](https://github.com/scottyhq/esip-tech-dive)
          - Overwrite default content without including `.git`, `.gitignore`
          - Modify `README.md` 
        - `Delta/image/notebooks` contains `xxx.ipynb` notebooks files
          - These will be pre-populated into the container environment
        - `Delta/image/binder` contains...
          - `apt.txt`: additional Linux packages to pre-install
          - `environment.yml` listing conda packages to pre-install
            - How do we generate this file from some environment?
              - `% conda activate esip-tech-dive`
              - `% conda list`
              - `% conda env export -f environment.yml`
              - DESCRIBE how `jupyterlab-workspace.json` supports jupyterlab 
              - TRANSLATE "the postBuild script therein extends jupyter notebook to jupyter lab   
        - `Delta/image/.dask`
          - contains `config.yaml` describing a kubernetes dask worker
            - Intended to be cloud-vendor agnostic
            - This is also the Users container environment where they can for example build Jupyter notebooks
        - `Delta/image` also contains some files: `LICENSE.TXT`, `Welcome.md`, maybe some logos etcetera
      - `Delta/config` contains some `.yaml` files: Copied from `Bravo`, no changes.
      - `Delta/secrets` is authentication material; not covered at this time
      - `Delta/README.md` is the usual thing
      - `Delta/hubploy.yaml` is also not documented here yet; relegated to section 3 below 
      
Now that this is all "completed" the PR to `pangeo-data/pangeo-cloud-federation` is sufficient to start 
the deployment in motion. 


#### How a PR triggers the build

- ELABORATE How CircleCI is triggered and what it does
- repo2docker will read these files and create the docker image with all this stuff. 
- hubploy calls the repo2docker api. 
- hubploy is called by circle.ci


# Context 3: Tactics of building a pangeo instance


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
