# Dockerfile for biocm-seurat-v5:1.0.1
FROM bioinformaticsmusc/biocm-seurat-v5:1.0.0

#Install other R Packages
RUN R -e "remotes::install_github('immunogenomics/presto')"

RUN git clone https://github.com/BioinformaticsMUSC/biocm-resources.git

RUN R -e "BiocManager::install(c('limma', 'edgeR', 'DESeq2'))"

RUN R -e "remotes::install_github('neurorestore/Libra')"

#Install infercnv
RUN R -e "BiocManager::install('infercnv')"

#install doMC
RUN R -e "install.packages(c('doMC', 'optparse', 'rstatix'))"

RUN R -e "install.packages('clue')"

RUN R -e "install.packages('heatmap3')"

RUN R -e "install.packages('RSpectra')"

RUN R -e "BiocManager::install('ConsensusClusterPlus')"

#install archR
RUN R -e "remotes::install_github('GreenleafLab/ArchR', ref = 'master', repos = BiocManager::repositories())"

RUN R -e "BiocManager::install(c('BSgenome.Hsapiens.UCSC.hg38','BSgenome.Mmusculus.UCSC.mm10'))"


