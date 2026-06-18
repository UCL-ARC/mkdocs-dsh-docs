# DSH Research Compute Services Status Page

This page outlines that status of the DSH Research Compute environment and the planned outages managed by the ARC Bespoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing issues with the cluster, feel free to report them to <rc-support@ucl.ac.uk>.

## Status of the DSH Research Compute Services

  
  - 2026-06-17 @ 4:00 pm - GPU system patching required:
    - All DSH Research Compute GPU machines must be temporarily powered off to implement system patching -- this will be done in stages as outlined below. The patching of a given system should only take a few hours, and all machines should be back up and running by end of day Thursday, June 18th. The DSH HPC Cluster queue will also be temporarily disabled until this work is completed.
      - Stage 1: A subset of VMs using V100 GPUs will be powered down first, this will include cluster node dsh-sge2gpu03. This is expected to begin at 4:00 pm on Wed. June 17th and be completed by end of day.
      - Stage 2: All VMs using A100 GPUs will be powered down second, this will include cluster nodes dsh-sge2gpu01 and dsh-sge2gpu02 as well as select Customer Specialist Servers. This is expected to begin at end of day on Wed. June 17th, and be completed by lunchtime Thurs. June 18th.
      - Stage 3: All remaining VMs using V100 GPUs will be powered down, this will include cluster nodes dsh-sge2gpu04, dsh-sge2gpu05, as well as all Customer Specialist Servers using V100 GPUs. This is expected to begin in the morning of Thurs. June 18th, and be completed by end of day.
    - @ Wed, 4:00 pm - Stage 1 machines have been powered off and patching is in progress.
    - @ Wed, 4:30 pm - Stage 2 machines have been powered off and are awaiting patching.
    - @ Thurs, 10:00 am - Maintenance for Stage 1 machines has been completed. Patching is in progress for Stage 2 machines.
    - @ Thurs, 10:17 am - Stage 3 machines have been powered off and are awaiting patching.
    - @ Thurs, 11:30 am - The DSH HPC Cluster queue has been re-enabled (but note that only one GPU node is currently available for jobs in the cluster)
    - @ Thurs, 4:02 pm - Maintenance for Stage 2 machines has been completed. Patching is in progress for Stage 3 machines.
  - 2026-04-30 @ 11:30 am - Emergency security patching required:
    - All DSH Research Compute machines must be rebooted to implement an emergency security patch.
    - @ 11:30 am - The DSH HPC Cluster job queue has been temporarily disabled to facilitate the patching of the compute nodes, and all login nodes and user-facing standalone machines will be rebooted between 4:00 pm and 5:00 pm this afternoon. The DSH HPC Cluster queue will be re-enabled after all patching and reboots have been completed.
    - @ 4:08 pm - DSH HPC Cluster and Customer Specialist Server machines powered off for above-noted maintenance
    - @ 4:17 pm - Customer Specialist Server machines should now be fully available
    - @ 4:27 pm - DSH HPC Cluster nodes are back online, and the cluster queue has been re-enabled
    - @ 4:30 pm - All maintenance actions are completed and DSH Research Compute Services are fully back in service.
  - 2026-01-26 - New V100 GPU nodes added to DSH HPC Cluster:
    - Three new GPU-capable compute nodes have been added to the DSH HPC Cluster, each using an NVIDIA Tesla V100 32 GB GPU. To request a GPU node of any type you can continue to use `#$ -l gpu` and the scheduler will assign your job to the first available GPU node, regardless of which GPU it has. To request a specific GPU type, you can add one of the `a100` (for NVIDIA A100 Tensor Core 80 GB GPUs) or `v100` (for NVIDIA Tesla V100 32 GB GPUs) boolean operators, for example: `#$ -l a100=TRUE`. See [Submitting Jobs to the DSH HPC Cluster](3.3-Running_jobs.md/#gpus) for more information.

## Planned outages for DSH Research Compute Services

Full details of unplanned outages are emailed to the DSH Research Compute user list. 

The second Tuesday of every month is a RedHat patch release day, aka **Patch Tuesday**. In response to this, we perform maintenance on DSH HPC machines every month, including patching and possible system reboots. Any outages should only last a couple of hours, and the system should resume normal operation before noon on the machine's respective patch day. If there is a notable delay in bringing a system back, we will contact affected users after approximately midday.

For Customer Specialist Servers, machines are patched and rebooted on a set monthly schedule. Generally, these updates will occur on Mondays and Wednesdays starting the second Monday after Patch Tuesday (i.e. approx. 13 days later). You can see your machine's next scheduled update in the Message of the Day banner when logging into the machine via SSH.

For the DSH HPC Cluster, in anticipation of its patching window, the cluster queue will be disabled in the afternoon of the second Friday after Patch Tuesday (i.e. approx. 17 days after the first Tuesday of the month). 
This will prevent any new jobs from being submitted, but will still allow existing jobs to be scheduled and run as normal. On the subsequent Monday morning, all cluster machines will be taken offline for patching and maintenance -- note that any jobs that have not completed by this time will be forcibly interrupted, and may need to be re-submitted once the cluster resumes normal operation.

After an outage, the first day or two back should be considered 'at risk'; that is, things are more likely to go wrong without warning and we might need to make adjustments.

### List of planned outages

Date                | Status  | Reason 
--------------------|---------|--------
15 June 2026 | Completed | Patching and maintenance for Group 1 machines.
17 June 2026 | Completed | Patching and maintenance for Group 2 machines.
19 June 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
22 June 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---
20 July 2026 | Planned | Patching and maintenance for Group 1 machines.
22 July 2026 | Planned | Patching and maintenance for Group 2 machines.
24 July 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
27 July 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---
17 August 2026 | Planned | Patching and maintenance for Group 1 machines.
19 August 2026 | Planned | Patching and maintenance for Group 2 machines.
21 August 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
24 August 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---




