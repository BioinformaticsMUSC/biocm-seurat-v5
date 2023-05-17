# biocm-seurat-docker

This is a Dockerfile and related files for the biocm-seurat docker image. The container is preloaded with R and many R packages used by the BioCM, including Seurat, dplyr, 
ggplot2, presto, Libra, and more.

## Example usage

This container can be used interactively or with a batch job submission. 

### Interactive use

Make sure you are on a compute node in the palmetto cluster.

Navigate to the `singularity_images` folder:
```
cd /zfs/musc3/singularity_images
```

Use the following command to open an R command prompt:

```
singularity run -B /zfs/musc3:/mnt --pwd /mnt biocm-seurat_latest.sif
```
Note the options used here:
- `-B /zfs/musc3:/mnt`: this command creates a link between the source directory (here, `/zfs/musc3`) and the destination directory inside the container `/mnt`. You may link any 
source directory--those directories and files will then be accessible inside the container. If you save anything within those directories inside the container, it will exist when 
the container is done. 
- `--pwd /mnt`: this sets the working directory inside the container to `/mnt`, which is the mounted volume linked to the source directory.

Alternatively, you can get shell access in the container by using this command:
```
singularity shell -B /zfs/musc3:/mnt --pwd /mnt biocm-seurat_latest.sif
```

### Batch job
For a batch job using R, it is a good idea to have an R script that can be run on the cluster. To do so, use the following code in the PBS file:
```
cd /zfs/musc3/singularity_images

singularity exec -B /scratch1/bryangranger/cecile:/mnt --pwd /mnt biocm-seurat_latest.sif Rscript /mnt/project_directory/example_R_script.R \
--option1 option1
--option2
```

Note the same options used as above. The options are only necessary if the Rscript requires them.

### Installing new packages

Unfortunately, users cannot install new packages into a running container. But a new image can be created with the necessary packages. For new packages, please submit an issue or 
contact the BioCM.
