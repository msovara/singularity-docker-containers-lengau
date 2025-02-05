
# Singularity Docker Containers on Lengau  
A guide to pulling Singularity image files and running containers on Lengau.

---

## **Developer Notes**  

### 1. Sign into Login02 on Lengau  
Run the following commands to access Lengau and load Singularity:  
```bash
ssh username@lengau.chpc.ac.za
ssh globus
module load chpc/singularity/3.5.3
module list
```

### 2. Search for a Public Container  
To find an available container in the Singularity library, use:  
```bash
singularity search wsclean
```

### 3. Pull the Container  
Download the WSClean container from Singularity Library:  
```bash
singularity pull library://albatross0210/default/wsclean
```

### 4. Verify the Image  
Check if the image works and manually verify its metadata:  
```bash
singularity run wsclean_latest.sif
singularity inspect wsclean_latest.sif
```
### 5. Check Basic Metadata and List Installed packages
For Debian/Ubuntu-based containers
```
singularity exec wsclean_latest.sif dpkg --list
```
For CentOS/RHEL-based containers
```
singularity exec wsclean_latest.sif rpm -qa
```

---

## **User Notes**  

### 1. Sign into Login02 on Lengau  
Before using the container, sign in and load the required modules:  
```bash
ssh username@lengau.chpc.ac.za
module purge
module load chpc/singularity/3.5.3
module load wsclean/3.0
module list
```

### 2. Open a Shell Inside the Container  
To start an interactive session inside the container, run:  
```bash
singularity shell wsclean_latest.sif
```
You will see a `Singularity>` prompt. Inside the shell, you can run:  
```bash
wsclean --help
```

### 3. Run a Specific Command from Outside the Container  
If you prefer to run WSClean without entering the container shell:  
```bash
singularity exec wsclean_latest.sif wsclean --help
```

### 4. Binding a Working Directory  
If you need to access files from your host system inside the container:  
```bash
singularity exec --bind /path/to/data:/data wsclean_latest.sif wsclean --help
```
- Inside the container, `/data` will map to `/path/to/data` on your host.

### 5. Binding a Host Directory for Input/Output  
For processing files stored on the host system:  
```bash
singularity exec --bind /your/data/dir:/mnt wsclean_latest.sif wsclean -i /mnt/input.fits -o /mnt/output
```
- Replace `/your/data/dir` with the actual path to your working directory.
- Inside the container, files will be accessible under `/mnt`.

### 6. Running WSClean in Batch Mode  
To run WSClean in batch mode, pass the input and output directly:  
```bash
singularity run wsclean_latest.sif input.fits output
```

---

## **Additional Notes**
- If you encounter permission issues, check that the `.sif` file is accessible.
- Ensure that `/path/to/data` is correctly mapped inside the container.
- If needed, use `singularity run --cleanenv` to avoid environment conflicts.

---

This guide is also available at:  
📌 **[GitHub Repository](https://github.com/msovara/singularity-docker-containers-lengau)**
