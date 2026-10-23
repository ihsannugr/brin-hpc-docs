---
icon: lucide/server
title: Resources
---

# Compute Resources & Hardware

BRIN High Performance Computing operates multi-tiered compute clusters tailored for heterogeneous research workloads—from large-scale parallel simulations to distributed deep learning.

---

## 1. System Architecture Overview

The computing facility consists of dedicated login nodes, CPU compute nodes, high-memory fat nodes, and high-performance GPU accelerators linked by a low-latency interconnect.

```text
                           ┌────────────────────────┐
                           │      Login Nodes       │ (SSH Access, Editing, Compiling)
                           └───────────┬────────────┘
                                       │ 100GbE / InfiniBand
             ┌─────────────────────────┼─────────────────────────┐
             │                         │                         │
┌────────────▼────────────┐ ┌──────────▼──────────┐ ┌────────────▼────────────┐
│    CPU Compute Nodes    │ │    GPU Accelerators │ │    High-Memory Nodes    │
│  Parallel MPI / OpenMP  │ │ PyTorch / CUDA / AI │ │  Large Genomes & Graphs │
└─────────────────────────┘ └─────────────────────┘ └─────────────────────────┘
             │                         │                         │
             └─────────────────────────┼─────────────────────────┘
                                       │ InfiniBand Fabric
                           ┌───────────▼────────────┐
                           │ High-Speed Filesystem  │ (/scratch & /project)
                           └────────────────────────┘
```

---

## 2. Node Specifications

The following table summarizes the compute capabilities available across cluster partitions:

| Node Type | Processor Architecture | Cores / Threads | Total RAM | Accelerators / GPUs | Typical Workloads |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Standard Compute** | AMD EPYC / Intel Xeon | 64 - 128 cores | 256 - 512 GB | None | Molecular dynamics, CFD, climate modeling |
| **GPU Compute** | AMD EPYC / Intel Xeon | 64 cores | 512 GB | 4x - 8x NVIDIA A100 / H100 | Deep learning, LLM training, cryo-EM |
| **High Memory (Fat)**| AMD EPYC / Intel Xeon | 128 cores | 1 TB - 2 TB | Optional | De novo genome assembly, graph analytics |
| **Interactive** | AMD EPYC / Intel Xeon | 32 cores | 128 GB | 1x GPU (optional) | Debugging, visualization, preprocessing |

---

## 3. Storage Hierarchy

The cluster provides high-performance tiered storage to balance speed and capacity:

1. **Local NVMe SSD (`$TMPDIR` / `/tmp`)**: 
   High IOPS local scratch on each node, ideal for unpackaged small files or temporary job artifacts.
2. **Parallel Scratch (`/scratch/<user>`)**: 
   Distributed parallel filesystem (Lustre / GPFS / BeeGFS) accessible from all compute nodes with multi-gigabyte/second throughput.
3. **Project Storage (`/project/<group>`)**: 
   Shared group storage for dataset preservation and active collaborative research.
4. **Home Directory (`/home/<user>`)**: 
   Persistent home storage for dotfiles, environment configurations, and scripts.

---

## 4. Partitions and Queues

Workloads are scheduled into distinct SLURM partitions depending on resource requirements:

| Partition Name | Max Walltime | Default Walltime | Max Nodes / Job | Target Purpose |
| :--- | :--- | :--- | :--- | :--- |
| `normal` | 48 hours | 2 hours | 16 nodes | General batch compute jobs |
| `long` | 168 hours (7 days)| 24 hours | 4 nodes | Extended sequential/parallel jobs |
| `gpu` | 48 hours | 4 hours | 4 nodes | GPU-accelerated computing & AI |
| `highmem` | 72 hours | 8 hours | 2 nodes | Workloads exceeding 512 GB RAM |
| `interactive` | 2 hours | 30 minutes | 1 node | Interactive testing and debugging |

---

## 5. Maintenance Schedules

Regular cluster maintenance windows are scheduled monthly for security updates, kernel patching, and filesystem maintenance. Maintenance announcements are broadcast via system motd banners and posted to [Events & Announcements](../events_and_workshops/index.md).
