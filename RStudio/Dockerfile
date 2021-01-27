FROM docker.io/rocker/rstudio:4.0.3


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
  libglpk-dev 
  
RUN R -e "install.packages(c('rmarkdown','dplyr','tidyr','tibble','ggplot2','magrittr','RPostgreSQL','mongolite','stringr','purrr','RColorBrewer'))"