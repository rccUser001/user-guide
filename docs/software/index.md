##  Getting your software ready

You should check what software packages are already installed on Midway3 via `module avail` and `module list`. Many commonly used software packages and libraries have been installed on Midway for your use.  For an overview of how to use Software Modules on Midway, consult the RCC [Software](../software/index.md) documentation page.

For this tutorial, let us load `python`

```
module load python
```

which will load the default version of the `python/anaconda` module. You can do `module list` to see which version is just loaded.

Suppose that you would like to install numpy, matplotlib and pandas for your calculations.  You should first create an environment in your own space and install these packages into this environment.  See [managing Python environments](../software/apps-and-envs/python.md) for more information.

Since Python environments might contain many files and/or take a lot space, it is recommended that you create your environments somewhere outside your home folder such as `/project` or `/scratch`. Suppose that your PI has a space under `/project/[pi-folder]` and you have a folder under that location.

```
cd /project/[pi-folder]/[your-cnetid]
python -m venv my-venv
source ./my-venv/bin/activate
pip install matplotlib numpy pandas
```

Note that the base environment of the default `python` module already has many popular packages installed, including the above 3 packages. You can also create an environment and install packages with `conda` or `mamba`.

If you need to compile your software packages from source, you can download the software source code from GitHub to your space, load the compiler modules and build the codes. In this tutorial, let us build [LAMMPS](https://github.com/lammps/lammps) from source code:

```
cd /project/[pi-folder]/[your-cnetid]
git clone https://github.com/lammps/lammps.git
cd lammps
mkdir build && cd build
```

Load the modules for the preferred compiler, MPI libraries and MKL, and cmake to configure the build:
```
module load mpich/3.4.3+gcc-10.2.0 mkl/2023.1 cmake/3.26
cmake ../cmake -C ../cmake/presets/basic.cmake -DFFT=MKL -DFFTW3_INCLUDE_DIR=$MKLROOT/include/fftw
```

and finally build the code

```
make -j4
```

If the build succeeds, you will see a LAMMPS binary, namely `lmp`, generated under the folder `/project/[pi-folder]/[your-cnetid]/build`.

You can use other compilers (Intel oneAPI, GNU GCC) and MPI libraries (OpenMPI, MPICH). For GPU codes, you can use NVIDIA HPC SDK and Intel oneAPI. More information on the available development tools is given in [Compilers](../software/compilers.md). 


# Software packages and compilers 

The best way to view the latest software packages offered on RCC clusters is to check the list of available software modules with the `module avail` command.

All users can install software packages privately in their home and project directories. It is recommended to use **compute nodes** rather than login nodes when compilation and installation processes are time-consuming and require significant resources. Please check our documentation on how to start and use a `sinteractive` session [here](../slurm/sinteractive.md). 

## Loading and using available software modules

RCC uses [Environment Modules](http://modules.sourceforge.net){:target='_blank'} for managing software. The modules system permits us to set up the shell environment to make running and compiling software easier. It also allows us to make available many software packages and libraries that would otherwise conflict with one another. 

When you first log into RCC clusters, you will be entered into a basic user environment with minimal software available.  The `module` system is a script-based system used to manage the user environment and to `activate` software packages.  You must first load the corresponding software module to access software packages installed on RCC clusters. 

Basic `module` commands:

| Command  | Description | 
| --------- | --------- | 
| `module avail`          |   lists all available software modules            |    
| `module avail [name]`   |   lists modules matching [name]                   |
| `module load [name]`    |   loads the named module                          |
| `module unload [name]`  |   unloads the named module                        |
| `module list`           |   lists the modules currently loaded for the user |

!!! note "Module dependencies"
    Note that some modules require other specific modules, i.e., dependencies, to be loaded (or unloaded). If there is a conflict, you must explicitly unload the conflicting module (`module unload ...`), then load the desired module again. In certain cases, usually with loading an out-of-date module, you may get an error such as `Error: Requirement...` if a dependency is absent. In those situations, you can try `module load -f <module>` to force the module to load.

!!! note "Note on software for AMD CPUs" 
    For the `amd` [partitions](../partitions.md) on Midway3, you need the software modules built specifically for AMD CPUs.
```
module use /software/modulefiles-amd
module list
```

### Requesting a software package installation 
If you need software not currently available in the module system and believe that multiple research groups can benefit from installing this software, send a detailed request to our [Help Desk](https://rcc.uchicago.edu/support-and-services/consulting-and-technical-support){:target='_blank'} providing:

1. Complete the name of the software package 
2. Exact version number 
3. Link to the package website 
4. Explain in a paragraph how this software is crucial for your research and having it on RCC clusters. 

## Commonly used software packages

This guide contains instructions for some commonly used applications and environments, including: 

* [Alphafold](../software/apps-and-envs/alphafold.md)
* [CryoSPARC](../software/apps-and-envs/cryosparc.md)
* [Gaussian](../software/apps-and-envs/gaussian.md)
* [GROMACS](../software/apps-and-envs/gromacs.md) 
* [LAMMPS](../software/apps-and-envs/lammps.md)
* [MATLAB](../software/apps-and-envs/matlab.md)    
* [Mathematica](../software/apps-and-envs/mathematica.md)
* [NAMD](../software/apps-and-envs/namd.md)
* [NWChem](../software/apps-and-envs/nwchem.md)
* [OpenMM](../software/apps-and-envs/openmm.md)
* [OpenPose](../software/apps-and-envs/openpose.md)
* [ORCA](../software/apps-and-envs/orca.md)
* [Perl](../software/apps-and-envs/perl.md) 
* [Python, Anaconda, Jupyter Notebook & JupyterLab](../software/apps-and-envs/python.md)
* [R and RStudio](../software/apps-and-envs/r.md)
* [Singularity](../software/apps-and-envs/singularity.md)
* [Spark](../software/apps-and-envs/spark.md)
* [Stata](../software/apps-and-envs/stata.md) 
* [Tensorflow and PyTorch](../software/apps-and-envs/tf-and-torch.md)
* [VS Code (SCode)](../software/apps-and-envs/scode/main.md)

