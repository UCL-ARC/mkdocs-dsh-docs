# DSH Research Compute Services Status Page

This page outlines that status of the DSH Research Compute environment and the planned outages managed by the ARC Bespoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing issues with the cluster, feel free to report them to <rc-support@ucl.ac.uk>.

## Status of the DSH Research Compute Services

  - 2025-11-19 - Update: 16:56
    - Data Safe Haven now working as expected - The replacement network equipment has been installed this afternoon, and we have tested both data centre configurations.  The Data Safe Haven is now working as expected, at full capacity.  Those services which have been unavailable since Monday should now be accessible.
    - If you find a problem, please report it in the usual way through the MyServices portal: [Live - Self Service | UCL MyServices](https://myservices.ucl.ac.uk/self-service)
    - I would like to apologise for the disruption this outage has caused and your patience while we were working at reduced capacity. 
  - 2025-11-17 - Update: 16:15
    - Our network support team has a replacement device on order which should arrive tomorrow.  This will take some time to install and configure, so hard to predict exactly when we will be able to bring the DSH back to normal functioning, but we will be working on this as a priority.
    - We have now completed all steps to failover to the second data centre.  The service will be running at reduced capacity and some actions will be slower than usual.
    - Remote desktop is now working as expected with profiles and start menu.  All study shares should be available.
    - The following services will not be available until we can replace the broken network device:
      - The HPC service
      - Study specific application or database servers.
  - 2025-11-17 - Update: 12:00
    - We have migrated all main DSH portals to run from our other data centre, there are still some impacted features but the remote desktop, file transfer portal and REDCap are now working.   We are still working with our colleagues and support service to repair the underlying network issue, but until this is fully restored the service will be running at reduced capacity, and some lower priority services may not be available.
    - As we are running at reduced capacity many features will be running slower than usual.   You may see messages about logging in with a temporary profile and your start menu may not have all the applications you usually do.  We are working to fix this at the moment.
    - The majority of shares are now available, but some are still being migrated and may take longer to appear.
    - The HPC service will be unavailable until we have fixed the underlying network issue, as we are not able to migrate this to the other data centre.
    - If you have a database or application server this may not be available at the moment and it might not be possible to restore these until we have repaired the underlying network issue.
  - 2025-11-17 - Update: 10:00
    - There is a failure of an important network component in one of our data centres, the network team are working on this at the moment, but we do not have an ETA for its recovery.
    - This is impacting most DSH services.  The DSH team are working to migrate all services to work only in our other data centre.
    - We are treating this as our highest priority, and will provide updates as the situation changes.
  - 2025-11-17 - Problems with Data Safe Haven, 17/11/2025:
    - There are wide spread problems with the Data Safe Haven this morning. The team noticed this early this morning and have been working with colleagues to restore the service. The problem is with a specific piece of network equipment in one of our data centre's unfortunately we are unable to fix this remotely, so members of our team are heading to the data centre to fix this in person.

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
15 December 2025 | Planned | Patching and maintenance for Group 1 machines.
17 December 2025 | Planned | Patching and maintenance for Group 2 machines.
19 December 2025 | Planned | Cluster queue will be disabled pending patching on Monday.
22 December 2025 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines.
--- | --- | ---
19 January 2025 | Planned | Patching and maintenance for Group 1 machines.
21 January 2025 | Planned | Patching and maintenance for Group 2 machines.
23 January 2025 | Planned | Cluster queue will be disabled pending patching on Monday.
26 January 2025 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines.
--- | --- | ---
16 January 2025 | Planned | Patching and maintenance for Group 1 machines.
18 January 2025 | Planned | Patching and maintenance for Group 2 machines.
20 January 2025 | Planned | Cluster queue will be disabled pending patching on Monday.
23 January 2025 | Planned | Patching and maintenance for DSH HPC Cluster and Group 3 machines.





