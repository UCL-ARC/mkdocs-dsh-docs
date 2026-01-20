# DSH Research Compute Services Status Page

This page outlines that status of the DSH Research Compute environment and the planned outages managed by the ARC Bespoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing issues with the cluster, feel free to report them to <rc-support@ucl.ac.uk>.

## Status of the DSH Research Compute Services

  - 2025-12-23 - Support Staff Unavailable:
    - Support staff for DSH Research Compute services will be unavailable for the holiday season starting Weds., December 24th, 2025. All services will return to full supported status as of Mon., January 05, 2026.

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
06 January 2026 | Completed | Power-off of select machines pending decommission at end of month (IAO and IAA of affected machines will have been previously informed, and will receive additional email notification)
19 January 2026 | Completed | Patching and maintenance for Group 1 machines.
21 January 2026 | Planned | Patching and maintenance for Group 2 machines.
23 January 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
26 January 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
30 January 2026 | Planned | Select machines will be decommissioned and deleted (project's IAO and IAA will have been previously informed)
--- | --- | ---
16 February 2026 | Planned | Patching and maintenance for Group 1 machines.
18 February 2026 | Planned | Patching and maintenance for Group 2 machines.
20 February 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
23 February 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---
16 March 2026 | Planned | Patching and maintenance for Group 1 machines.
18 March 2026 | Planned | Patching and maintenance for Group 2 machines.
20 March 2026 | Planned | DSH HPC Cluster queue will be disabled pending patching on Monday.
23 March 2026 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines, and Cluster queue re-enabled.
--- | --- | ---





