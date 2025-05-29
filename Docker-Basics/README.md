## Common Comands
-  From specifies the Base image to use for the new image
- Work Dir - working Dir
- Copy - copies file or dir from the build context to the image
- Run executes command in the shell during image build
- Expose - Informes docker that the container will listen on speciied port at run time
- Env - env vars during build process
- Arg - Defines build time variables
- Volume - Creates a mount point for externaly mounted volumes
- Cmd - provides default command to executes when the container starts (More flexible and can be overriden)
- Entrypoint - Specifies the default executable to be run when the container starts (Defines defult command that can NOT be overriden)

## How to build Docker Image
- `docker build -t hello-docker .` 
    t here stand for tag - this is optional, if not provided it default to the default tag 
    hello-docker . this is the path to docker file

## How Check if image has been created 
- `docker images`

## How to run docker Image
- `docker run hello-docker` 
- `docker run -it hello-docker sh` to run it in shell mode
    ![Screen Shot of Docker run in shell mode](/Docker-Basics/Hello-Docker/Readme-Images/shellmode.png)

## Useful commands
- list all containers `docker ps -a`
- Stop a single container using the first 4 digits of it's id `docker stop d842`
- Remove all stoped containers `docker container prune`
- Remove a single container by name or id `docker rm [id/name]`
- Inspect a container `docker inspect [First 4 letters of id]`


## how to deploy docker image to your registery
- Login `docker login`
- Publish E.g. `docker tag react-docker 300543025/react-docker` 300543025 this is your username
- `docker push 300543025/react-docker`