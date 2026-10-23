---
icon: lucide/life-buoy
title: Support
---

# Support & Consulting

The BRIN HPC team is committed to assisting researchers across all phases of computational research—from initial onboarding and workflow porting to complex parallel optimization.

---

## 1. How to Get Help

If you encounter technical issues, job failures, or software dependencies, please use the following support channels:

<div class="grid cards" markdown>

-   :lucide-mail:{ .lg .middle } __HPC Helpdesk Ticket__

    ---

    Submit a detailed ticket with job IDs, error logs, and batch scripts.

    **Email:** `hpc-support@brin.go.id`

-   :lucide-users:{ .lg .middle } __Weekly Office Hours__

    ---

    Join weekly virtual office hours for live debugging, architecture advice, and consultation with HPC specialists.

    **Schedule:** Every Wednesday, 14:00 - 16:00 WIB

-   :lucide-message-square:{ .lg .middle } __Community Discussion__

    ---

    Connect with fellow researchers, ask questions, and share domain-specific tips on the internal research forum.

    **Platform:** BRIN Research Slack / Teams

-   :lucide-book-open:{ .lg .middle } __Workshops & Training__

    ---

    Register for hands-on sessions covering Linux basics, SLURM, GPU acceleration, and scientific workflows.

    [:octicons-arrow-right-24: View workshops](../events_and_workshops/index.md)

</div>

---

## 2. Submitting an Effective Support Ticket

To help our engineers diagnose and resolve your issue as quickly as possible, please provide the following details when writing to `hpc-support@brin.go.id`:

```text
Subject: [HPC Issue] Brief summary of the problem

1. Username: <your_username>
2. Job ID(s): <e.g., 1234567>
3. Cluster / Partition: <e.g., normal or gpu>
4. Node name (if known): <e.g., compute-04>
5. Path to job script & logs: </scratch/username/job.sh and output.err>
6. Exact error message: <copy and paste full error output>
7. Steps to reproduce: <commands executed prior to failure>
```

---

## 3. Frequently Asked Questions (FAQ)

??? question "Why is my job stuck in 'PD' (Pending) status?"
    Jobs remain pending for several common reasons:
    - `Priority`: Other higher-priority jobs are ahead in the queue.
    - `Resources`: Nodes with your requested CPU, RAM, or GPU configuration are currently busy.
    - `ReqNodeNotAvail`: A requested node is in maintenance or draining.
    
    You can inspect the reason by running:
    ```bash
    squeue --job <job_id> --format="%.18i %.9P %.8j %.8u %.2t %.10M %.6D %R"
    ```

??? question "How do I check my storage quota?"
    Run the quota check utility on the login node:
    ```bash
    # Check disk usage and quota limits
    myquota
    ```

??? question "My job failed with 'OOM' (Out Of Memory). What should I do?"
    An Out Of Memory error occurs when your process exceeds the memory requested via `--mem` or `--mem-per-cpu` in your job script. Check peak memory usage using:
    ```bash
    sacct -j <job_id> --format=JobID,JobName,MaxRSS,Elapsed,State
    ```
    Then resubmit your job with an increased `--mem` parameter.

---

## 4. Essential Linux Quick Reference

| Task | Command |
| :--- | :--- |
| Check directory contents | `ls -lh` |
| Check current disk usage | `du -sh <folder_name>` |
| View disk filesystem space | `df -h` |
| View active jobs | `squeue --me` |
| Cancel a running or pending job | `scancel <job_id>` |
| Check past job accounting stats | `sacct -j <job_id>` |
| Test GPU availability | `nvidia-smi` *(on GPU nodes only)* |
