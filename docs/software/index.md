---
icon: lucide/box
title: Software
---

# Software Environment

BRIN HPC provides a comprehensive scientific software stack, ranging from optimized compilers and numerical libraries to bioinformatics suites and deep learning frameworks.

---

## 1. Environment Modules (Lmod)

To avoid library version conflicts and maintain flexibility, software packages are provided as dynamic **Environment Modules** managed by Lmod.

### Essential Module Commands

| Command | Description | Example |
| :--- | :--- | :--- |
| `module avail` | List all available software modules | `module avail python` |
| `module load <name>` | Load a module into your shell environment | `module load openmpi/4.1.5` |
| `module list` | Show modules currently loaded in your session| `module list` |
| `module unload <name>` | Unload a specific module | `module unload cuda/12.1` |
| `module purge` | Unload all currently loaded modules | `module purge` |
| `module show <name>` | Display module description, dependencies, and environment variables | `module show gromacs` |

### Recommended Module Loading in Job Scripts
Always purge and explicitly load required modules inside your SLURM job scripts to guarantee reproducibility:

```bash title="submit_example.sh"
#!/bin/bash
#SBATCH --partition=normal
#SBATCH --nodes=1
#SBATCH --ntasks=8

# Clear inherited modules and load exact versions
module purge
module load gcc/11.3.0
module load openmpi/4.1.5
module load gromacs/2023.2

# Execute your application
srun gmx_mpi mdrun -deffnm simulation
```

---

## 2. Python, Conda, and Mamba

For custom Python environments, users are strongly encouraged to use **Miniconda** or **Mambaforge** in their scratch directory.

```bash
# Load pre-installed Miniconda module or activate your own
module load miniconda3

# Create an isolated environment with Mamba
mamba create -n my_research_env python=3.11 numpy scipy pandas pytorch -c conda-forge
conda activate my_research_env
```

!!! tip "Conda Storage Location"
    By default, Conda caches package tarballs in `~/.conda/pkgs`, which can fill your Home directory quota quickly. Set your cache to scratch:
    ```bash
    conda config --add pkgs_dirs /scratch/$USER/conda_pkgs
    conda config --add envs_dirs /scratch/$USER/conda_envs
    ```

---

## 3. Containers (Apptainer / Singularity)

For maximum portability and complex software dependencies, BRIN HPC supports **Apptainer** (formerly Singularity). Apptainer allows running Docker images securely without root privileges.

### Pulling and Running Images

```bash
# Pull an image directly from Docker Hub into an Apptainer SIF file
apptainer pull docker://pytorch/pytorch:2.2.0-cuda12.1-cudnn8-runtime

# Execute an interactive shell within the container with GPU pass-through
apptainer shell --nv pytorch_2.2.0-cuda12.1-cudnn8-runtime.sif

# Run a Python script inside the container in a batch job
apptainer exec --nv pytorch_2.2.0-cuda12.1-cudnn8-runtime.sif python3 train.py
```

---

## 4. Popular Software Packages

The BRIN HPC software repository maintains popular packages across major scientific domains:

- **AI & Data Science**: PyTorch, TensorFlow, JAX, Scikit-learn, Ollama, Hugging Face Transformers.
- **Molecular Modeling & Chemistry**: GROMACS, Gaussian, Quantum ESPRESSO, LAMMPS, VASP, CP2K.
- **Bioinformatics**: BLAST+, BWA, SAMtools, GATK, Trinity, AlphaFold2, QIIME 2.
- **Engineering & Physics**: OpenFOAM, ANSYS (academic license), Elmer FEM.
- **Mathematics & Statistics**: MATLAB, R, Julia, GNU Octave.

If a required package or library is not currently installed, you can compile it locally in your user directory or contact the [Support](../support/index.md) team to request a system-wide deployment.
