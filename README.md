Think of this as two things:
1. The Nginx/uWSGI/Flask/Conda (specifically the Conda environment) can take forever to build/update, hence top level (this project) builds the base image
2. The `example/` serves as the app itself. If your project was in `example/` then you use that `Dockerfile` to copy over your app files

So to reiterate:
* Top level: base image
* `exmample/`: you app
* dogs: :dog:

#### To modify the conda env:
* Change lines `55` & `58` of `Dockerfile`

#### To Build Base Image:
`docker build -t baesimage .`

#### To Build Your App Image:
`cd example/`
`docker build -t myimage .`
`docker run -d --name mycontainer -p 80:80 myimage`
