---
icon: lucide/rocket
title: Quick Start
---

# Quick Start Guide

Welcome to BRIN HPC! This guide provides an accelerated walkthrough to get you connected and running your first computational job with minimal setup.

---

## 1. Prerequisites Checklist

Before you begin, ensure you have:

1. **An active BRIN HPC account**: See [Access Guide](../access/index.md) if you need to register.
2. **An SSH client**: Built into Linux, macOS Terminal, and Windows PowerShell / OpenSSH.
3. **An SSH key pair**: Configured and registered with your HPC profile.
4. **Network connectivity**: If connecting from outside the BRIN intranet, connect through the [BRIN VPN](../access/index.md).

---

## 2. Standard Workflow Overview

Every computational workflow on BRIN HPC follows four essential stages:

```mermaid
flowchart LR
    A["1. Login<br>(SSH to Login Node)"] --> B["2. Environment<br>(Load Modules & Data)"]
    B --> C["3. Submit Job<br>(SLURM sbatch / srun)"]
    C --> D["4. Retrieve<br>(Analyze & Download)"]
```

### Stage 1: Logging In
Connect to the login node via SSH:

```bash
ssh <username>@hpc.brin.go.id
```

!!! warning "Login Nodes are for Management Only"
    Login nodes are shared among all active users. Do **not** execute heavy compute jobs, simulations, or model training directly on the login nodes. Heavy processes will be terminated automatically. All compute tasks must be submitted through the SLURM scheduler.

### Stage 2: Preparing Environment and Software
BRIN HPC uses **Lmod (Environment Modules)** to manage software packages without library conflicts.

```bash
# Search for available software modules
module avail

# Load a specific module (e.g., Python 3.11)
module load python/3.11
```

### Stage 3: Submitting Your First Job
Submit batch jobs using `sbatch` with a job script, or start an interactive session using `srun`.

=== "Batch Job Script (submit_test.sh)"
    ```bash
    #!/bin/bash
    #SBATCH --job-name=test_job
    #SBATCH --output=test_%j.out
    #SBATCH --error=test_%j.err
    #SBATCH --partition=normal
    #SBATCH --nodes=1
    #SBATCH --ntasks=4
    #SBATCH --time=00:10:00

    echo "Running on host: $(hostname)"
    echo "Date: $(date)"
    python3 -c "print('Hello from BRIN HPC cluster!')"
    ```

=== "Submit Command"
    ```bash
    # Submit the job script to SLURM
    sbatch submit_test.sh

    # Check status of your queued and running jobs
    squeue --me
    ```

=== "Interactive Session (Testing)"
    ```bash
    # Request an interactive session for 30 minutes with 2 cores
    srun --partition=interactive --cpus-per-task=2 --time=00:30:00 --pty bash
    ```

### Stage 4: Monitoring and Results
When your job completes, check the generated output logs (`test_<job_id>.out`) and retrieve your result files using standard file transfer tools such as `rsync` or `scp`.

---

## Next Steps

- **[Access](../access/index.md)**: Detailed instructions on SSH config, keys, and VPN setup.
- **[Resources](../resources/index.md)**: Hardware partitions, node specifications, and GPU availability.
- **[Software](../software/index.md)**: Comprehensive guide on modules, Conda, and container runtimes.
- **[Support](../support/index.md)**: Troubleshooting help and technical consulting.
