# DSH Research Compute Services Status Page

This page outlines that status of the DSH Research Compute environment and the planned outages managed by the ARC Bespoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing issues with the cluster, feel free to report them to <rc-support@ucl.ac.uk>.

## Status of the DSH Research Compute Services

  
  - 2026-08-26 @ 8:17am - GPU system maintenance initiated: As outlined below, "Stage 1" of the GPU maintenance has begun, and DSH HPC Cluster machines dsh-sge2gpu04 and dsh-sge2gpu05 as well as machines for CaseRefs 01148 and 00965 are now offline and will be unavailable for the next few hours.
    - @ 6:30pm - This maintenance is taking longer than anticipated, and the above-mentioned machines will remain out of service until at least 9am on Friday morning.
    - @ Fri, 9:08 am - Stage 2 as outlined below is set to begin, and DSH HPC Cluster machine dsh-sge2gpu03 will be powered off. Unfortunately, there was an issue during Stage 1 and those machines will remain offline for some time longer. We apologize for the inconvenience, and will provide updates as soon as we have more information.
    - @ Fri, 10:00 am - Maintenance on Stage 1 machines has failed, and will need to be reattempted at a later date. These machines will be brought back online in the meantime, and they should continue to function as normal. We will provide an update on when this maintenance will be re-attempted when we know more. Stage 2 maintenance continues as normal.
    - @ Fri, 6:00pm - This maintenance is now on hold until a future date. Stage 2 machines will remain out of service until Monday, September 7th.
  - 2026-08-24 - GPU system maintenance required:
    - DSH HPC Cluster GPU nodes and Customer Specialist Servers with GPUs will be receiving maintenance this week, which will result in a brief outage for affected machines. Affected machines and their scheduled maintenance date are outlined below; this maintenance should only take a couple of hours, and all machines should resume normal function by end of day on their scheduled maintenance day:
      - Stage 1, Weds. Aug. 26th: DSH HPC Cluster machines dsh-sge2gpu04, and dsh-sge2gpu05, and Customer GPU machines for CaseRefs 00965, 01148
      - Stage 2, Fri. Aug. 28th: DSH HPC Cluster machine dsh-sge2gpu03

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
17 August 2026 | Completed | Patching and maintenance for Group 1 machines.
19 August 2026 | Completed | Patching and maintenance for Group 2 machines.
21 August 2026 | Completed | DSH HPC Cluster queue will be disabled pending patching on Monday.
24 August 2026 | Completed | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
26 August 2026 | Failed | Maintenance for DSH Research Compute GPU machines (Stage 1)
28 August 2026 | Failed | Maintenance for DSH Research Compute GPU machines (Stage 2)
--- | --- | ---
14 September 2026 | Planned | Patching and maintenance for Group 1 machines.
16 September 2026 | Planned | Patching and maintenance for Group 2 machines.
18 September 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
21 September 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---
19 October 2026 | Planned | Patching and maintenance for Group 1 machines.
21 October 2026 | Planned | Patching and maintenance for Group 2 machines.
23 October 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
26 October 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.




