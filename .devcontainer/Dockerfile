FROM rocker/tidyverse:4.4.1

# Install some dependencies
RUN apt-get update 
RUN apt-get install -y --no-install-recommends \
    htop \
    r-cran-irkernel

# Give the id=1000 user sudo access without password
ARG USERNAME=rstudio
RUN apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# [Optional] Set the default user. Omit if you want to keep the default as root.
USER $USERNAME

# # Install some R packages
RUN Rscript -e "install.packages(c('languageserver','devtools','IRkernel','future.apply','rlist','pheatmap','BiocManager'), repos='https://cloud.r-project.org', dependencies = TRUE)" 
RUN Rscript -e "BiocManager::install(c('DESeq2','apeglm','DEGreport'), dependencies = TRUE)"
RUN Rscript -e "devtools::install_github('GeNeHetX/CancerRNASig')"