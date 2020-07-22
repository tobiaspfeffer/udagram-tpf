# Udagram Image Filtering Microservice

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.



## Tasks

### Setup Docker Environment
You'll need to install docker https://docs.docker.com/install/. Open a new terminal within the project directory and run:

1. Set version environment variable: `export TAG=0.0.0`
2. Build the images: `docker-compose -f docker-compose-build.yaml build --parallel`
3. Push the images: `docker-compose -f docker-compose-build.yaml push`
4. Run the container: `docker-compose up`

