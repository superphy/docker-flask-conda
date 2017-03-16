Think of this as two things:
1. The Nginx/uWSGI/Flask/Conda (specifically the Conda environment) can take for

#### To modify the conda env:
* Change lines `55` & `58` of `Dockerfile`

#### To Use:
`docker build -t myimage .`
`docker run -d --name mycontainer -p 80:80 myimage`
