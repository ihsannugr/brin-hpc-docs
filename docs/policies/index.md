---
icon: lucide/scale
title: Policies
---

# Policies & Guidelines

To ensure fair, secure, and reliable access to BRIN High Performance Computing infrastructure for all researchers, users must adhere to the following policies.

---

## 1. Acceptable Use Policy (AUP)

BRIN HPC facilities are dedicated exclusively to scientific, educational, and authorized national research initiatives.

### Permitted Activities
- Scientific computing, simulations, modeling, and data analytics.
- Machine learning, AI model training, and inference for research projects.
- Software testing and benchmarking related to academic and research goals.

### Prohibited Activities
- Cryptocurrency mining, financial trading algorithms, or commercial processing without explicit agreement.
- Unauthorized vulnerability scanning, penetration testing, or network attacks.
- Storing or processing unlawful, abusive, or copyrighted material without authorization.
- Sharing account credentials or private SSH keys with unauthorized third parties.

!!! danger "Enforcement"
    Violations of the Acceptable Use Policy may result in immediate suspension of HPC access, revocation of research allocations, and referral to institutional administration.

---

## 2. Fair-Share Scheduling and Resource Etiquette

Our job scheduler (SLURM) implements **fair-share priority** to prevent monopolization of compute nodes.

1. **Login Node Etiquette**: Do not run CPU-intensive, memory-heavy, or long-running tasks on the login nodes. Such processes degrade system performance for all users and will be terminated automatically.
2. **Accurate Resource Requests**: Specify realistic runtimes (`--time`) and memory allocations (`--mem`). Requesting excessive resources inflates queue wait times for yourself and other users.
3. **Partition Compliance**: Always submit jobs to the partition appropriate for your workload size and duration (e.g., short interactive test jobs vs. long production batch runs).

---

## 3. Storage & Data Retention

Storage on the cluster is divided into tiers with differing retention guarantees:

| Storage Area | Typical Path | Purpose | Backup Status | Retention Policy |
| :--- | :--- | :--- | :--- | :--- |
| **Home** | `/home/<user>` | Configuration, dotfiles, scripts | Backed up | Kept as long as account is active |
| **Project** | `/project/<group>` | Shared research data, lab assets | Periodic snapshots | Per project allocation duration |
| **Scratch** | `/scratch/<user>` | High-throughput temporary I/O | **No backup** | Auto-purged after 30 days of inactivity |

!!! tip "Scratch Directory Best Practice"
    Always write heavy job outputs directly to `/scratch/`. Once your simulation finishes, move critical results to your project storage or download them locally.

---

## 4. Mandatory Citation and Acknowledgement

Proper acknowledgment of BRIN HPC resources in scientific publications, conference proceedings, posters, and theses is **mandatory**. Citations provide quantifiable evidence of impact, which directly supports facility upgrades and national funding.

### Standard Acknowledgment Statement
Please include the following acknowledgement text in your manuscripts:

> *"The authors acknowledge the High Performance Computing (HPC) facility at Badan Riset dan Inovasi Nasional (BRIN), Indonesia, for providing computational resources and technical support for this research."*

### Reporting Publications
When your paper is published or accepted, notify the BRIN HPC team so we can highlight your work in our [Research Showcase](../research_showcase/index.md).
