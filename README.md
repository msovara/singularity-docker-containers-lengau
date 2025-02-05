# singularity-docker-containers-lengau
Guide to pull singularity image files and run containers on lengau

# Developer Notes

1. ## Sign into Login02 on lengau

```
ssh username@lengau.chpc.ac.za
ssh globus
module load chpc/singularity/3.5.3
module list
```

2. ## Search for a public container
```
singularity search wsclean
```
3. ## Pull container
```
singularity pull library://albatross0210/default/wsclean
```
4. ## Check if image works and verify the image manually 
```
singularity run wsclean_latest.sif
singularity inspect wsclean_latest.sif
```

# User Notes
1. ## Sign into Login02 on lengau
```
ssh username@lengau.chpc.ac.za
ssh globus
module load chpc/singularity/3.5.3
module list
```

2. ## Running the Container Interactively
```
singularity shell wsclean_latest.sif
```
3. ## Run a specific command
```
singularity exec wsclean_latest.sif wsclean --help
```
4. ## Binding a Host Directory
If you need to work with files on your host system, you should bind a directory:
```
singularity exec --bind /your/data/dir:/mnt wsclean_latest.sif wsclean -i /mnt/input.fits -o /mnt/output
```
- Replace /your/data/dir with the actual path to your working directory.
- Inside the container, your files will be available under /mnt.
   
