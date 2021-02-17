FROM docker.io/rocker/rstudio:4.0.3

#ENV PATH="/root/miniconda3/bin:${PATH}"
#ARG PATH="/root/miniconda3/bin:${PATH}"


RUN apt update && apt upgrade -y \
  && apt install -y \
  pandoc \
  pandoc-citeproc \
  libcurl4-gnutls-dev \
  libcairo2-dev \
  libxt-dev \
  libssl-dev \
  libssh2-1-dev \
  libgsl0-dev \
  libclang-dev \
  libpq-dev \
  openssh-client \
  libxml2 \
  libglpk-dev \
  libgit2-dev

# This didn't work
#RUN export ADD=shiny && bash /etc/cont-init.d/add
  
RUN R -e "install.packages(c('rmarkdown','dplyr','tidyr','tibble','ggplot2','magrittr','RPostgreSQL','mongolite','stringr','purrr','RColorBrewer','renv','golem','reticulate'))"

USER rstudio

RUN R -e "reticulate::install_miniconda()"

USER root