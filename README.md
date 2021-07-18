# JHU Thesis RStudio Container

I built this container to support my thesis work. It takes the base rocker rstudio container from Docker Hub, updates and installs required system libraries and then installs all required additional R Packages.  

This container image is connected to my Docker Hub repository at [neilkester/thesis-rstudio](https://hub.docker.com/repository/docker/neilkester/thesis-rstudio). Docker Hub automatically builds a new version of this container as changes are made to this GitHub project's Master branch.

I reference this container image in my Thesis-Charts GitHub project as the source image of the RStudio component of that Helm Chart and Rancher Questions file.

## R Packages included in this image  

R Packages:
  rmarkdown  
  dplyr  
  tidyr  
  tibble  
  ggplot2  
  magrittr  
  RPostgreSQL  
  mongolite  
  stringr  
  purrr  
  RColorBrewer  
  renv  
  golem  
  reticulate  
  
Also, Miniconda3-latest-Linux-x86_64

## Building this image locally with Buildah

If building this image locally, use the buildah command below. Note to update the tag (currently `v1.4`) to something more meaningful. Also, this assumes you are in this GitHub project's folder. If not, replace `.` with the relative or absolute path to the Dockerfile.

`buildah build-using-dockerfile -f Dockerfile -t docker.io/neilkester/thesis-rstudio:v1.4 .`

## Interacting with Podman

Running a Container

Now you can run that container with the podman run command. Before we execute that, however, it is important to understand some of the often used flags.

Here are a few that I use often:

`-i`: This makes the container interactive
`-t`: This creates a temporary or pseudo terminal. This allows you to pass commands to the container.
`--rm`: This removes the container (but not the container image) when the container is stopped. This is helpful if you are testing the container and do not need to retain any changes you make. If you don’t have this flag you will need to run manual commands to remove existing containers.
`-d`: This detaches the container. This is useful if you want to start a container that runs in the background and still use your WSL terminal.
`-p`: Forward a container port to a host port. This is required if the container is a server that needs to be accessible from a web browser. For instance, RStudio-Server, Jupyter Notebook/Lab, and many DBMS GUIs.
`-n`: Name the container to make it easier to find later. If this flag is not provided podman assigns a random name that consists of two words separated by an _.
In general, a podman run command looks like this:

`podman run <flags and input parameters> <container image>:<tag> <command (not required)>`
The following command runs the Ubuntu container with an interactive shell and deletes the container when it is stopped.

`podman run -it --rm docker.io/library/ubuntu:focal` 

As of 2021-02-05 there has been a change to Podman that breaks it when running in WSL2. To fix this you must pass two additional flags. An interactive `podman run` command should look like this:  

`podman run -it --rm --events-backend=file --cgroup-manager=cgroupfs docker.io/neilkester/thesis-rstudio:v1.2 bash` 

Run the pod in detached mode for RStudio with:  

`podman run -d -p 8787:8787 -e PASSWORD=mypass --rm --events-backend=file --cgroup-manager=cgroupfs docker.io/neilkester/thesis-rstudio:v1.2 bash` 