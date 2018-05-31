[![Build Status](https://travis-ci.org/superphy/docker-flask-conda.svg?branch=master)](https://travis-ci.org/superphy/docker-flask-conda) [![GitHub license](https://img.shields.io/badge/license-Apache%202-blue.svg)](https://raw.githubusercontent.com/superphy/docker-flask-conda/master/LICENSE.txt)

Think of this as two things:
1. The Nginx/uWSGI/Flask/Conda (specifically the Conda environment) can take forever to build/update, hence top level (this project) builds the base image
2. The `example/` serves as the app itself. If your project was in `example/` then you use that `Dockerfile` to copy over your app files

So to reiterate:
* Top level: base image
* `exmample/`: you app
* dogs: :dog:

# Conda vs. Pip

Due to conda's preference for its own Python repository (instead of pip) & the
out-of-date problems assoc. with this, we use conda for dependencies which are
only available there.
Conda also lacks channel pinning (or hash pinning for that matter) and thus, we
try to keep everything out of conda if possible.

A standard pip requirements.txt file is the preferred way to adding Python deps.
Note: if you activate a conda env, then do a `pip install`, conda has a tendency
to add your pypi dependency into its own environment.yml dep. instead when doing
a `conda env export`. Try to ensure that we're pulling for pypi install of
anaconda cloud when updating this repo.

The Dockerfile will build the conda env first, then use pip to install your
requirements.txt deps. inside that env. This image is what's shipped.

#### To modify the conda env:
* Change the app/environment.yml file.

#### To modify the pip requirements:
* Change the app/requirements.txt file.



#### To Build Base Image:
`docker build -t baesimage .`

#### To Build Your App Image:
`cd example/`
`docker build -t myimage .`
`docker run -d --name mycontainer -p 80:80 myimage`
