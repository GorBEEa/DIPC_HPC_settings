# :desktop_computer: DIPC HPC settings

Guidelines, recommendations, and tips for working on the [DIPC High Performance Cluster](https://scc.dipc.org/docs/). All commands have been tested on **`Hyperion`** and are expected to be compatible with `Atlas EDR` and `FDR` systems as well.

a. Before starting 

## 1. Secure Shell Connection :computer: :left_right_arrow: :desktop_computer:
<details><summary>SSH Connection</summary>
<p>
Open a terminal and type the following command with your username:
  
`````shell
ssh <username>@hyperion.sw.ehu.es
`````
<p>
</details>

## 2. Working with modules :toolbox:
<details><summary>Tips for working with modules on the Cluster</summary>
<p>
  
**a) Listing Available Modules:**
  Use the `module avail` command to list all modules available on the system.
  
`````shell
module avail
`````
**b) Loading Modules:**
  Use the `module load` command to load a specific module into your session. This will set up the necessary session variables and paths.
  
`````shell
module load <module_name>
`````
  Some modules have multiple versions available. Use the `module load` command followed by the module name and version to load a specific version.
`````shell
module load <module_name>/<version>
`````

**c) Unloading Modules:**
  Use the `module unload` command to remove a module from your session. This will unset the session variables and paths set by the module.
  
`````shell
module unload <module_name>
`````
**d) Purging All Modules:**
  Use the `module purge` command to unload all currently loaded modules. This is useful when you want to start with a clean session.
  
`````shell
module purge
`````
**e) Listing Loaded Modules:**
  Use the `module list` command to see all modules currently loaded in your session.
  
`````shell
module list
`````
<p>
</details>

## 3. SLURM
<details><summary>Tips for working with SLURM Workload Manager</summary>
<p>

**a) Submitting Jobs.**
`sbatch`: Submit a batch script to SLURM.

`````shell
sbatch my_job_script.sh
`````

More information at:
- https://scc.dipc.org/docs/jobs/slurm/
- https://slurm.schedmd.com/overview.html
<p>
</details>

## 4. Process amplicon sequences :dna:
<details><summary>DADA2 first configuration</summary>
<p>

These steps are only neccesary the first time we use the cluster. This commands are only to correctly install DADA2. Pipeline is in [TO_BE_ADDED repository](link).

1. Connect to hyperion cluster. You need previously an user [account](https://scc.dipc.org/docs/access/accounts/)
`````shell
ssh <username>@hyperion.sw.ehu.es
`````
2. Load Mamba
````shell
module load Mamba
`````
3. Activate Bioconda channel
`````shell
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
conda config --set channel_priority strict
`````
4. Create a new conda environment. You have to replace "myenvname" by a reaseonbale name (e.g. dada2)
````shell
mamba create --name "myenvname" bioconductor-dada2
````

*Some tips to work with mamba/micromamba/conda. I will write all commands using **mamba** below, but the arguments are the same for the two others.*
`````shell
# Activate an environment
mamba activate ENV_NAME

# Deactivate an environment
mamba deactivate

# Adding/Updating software
mamba install -n ENV_NAME PACKAGE
mamba update -n ENV_NAME --all
`````
5. Install dada2 in R
````shell
# Activate the environment
mamba activate dada2
# Star R (v. 4.3)
R
# Install Bioconductor Packages
if (!require("BiocManager", quietly = TRUE))
  install.packages("BiocManager")
BiocManager::install(version = "3.18")
# Check the lastest version of R you have installed. If you have the latest version of R (4.4) you should replace the bioconductor version to "3.19"

# Other sources of installation: https://benjjneb.github.io/dada2/dada-installation.html

# Restart a new R session and check dada2 package by exploring documentation:

quit()

R

library("dada2")

help(package="dada2")
?derepFastq
?dada
`````
<p>
</details>

