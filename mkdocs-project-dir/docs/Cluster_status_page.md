# Status of the cluster

This page outlines that status of the DSH cluster and the planned outages managed by the Beskpoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing 
issues with the cluster, feel free to report them to rc-support@ucl.ac.uk.

### DSH cluster status

  - 2025-06-05 - DSH cluster is working normally, with some machines out of disk space for updates.
    We might need to reboot some machines.


### Planned outages for the DSH cluster 

Full details of unplanned outages are emailed to the cluster user list. 

The second Tuesday of every month is a RedHat patch release day, aka “Patch Tuesday”.
We perform maintenance every month in the cluster in the afternoon of the Friday 17 days after Patch Tuesday. The
queue will be disbles before an outage begins. The nodes may need to be emptied of jobs in advance ('drained')

If there is a notable delay in bringing the system back we will contact you after approximately midday.
After an outage, the first day or two back should be considered 'at risk'; that is, things are more likely to go wrong
without warning and we might need to make adjustments.

Date                | Status  | Reason 
--------------------|---------|--------
20 June 2025        | Planned | Queue of the cluster will be drained for the weekend from 16:00. This is to apply the 
RedHat system updates. Jobs that will not be able to complete before the outage will stay in the queue and will not start 
until after the outage.

## Previous Outages

Date                | Status    | Reason 
--------------------|-----------|--------
11 May 2025         | Completed | Maintenance day: nodes being drained for a system update.


Friday 17 days after Patch Tuesday (T+17) = DSH Prod Cluster preparation

    Date: June 20, 2025

    Tasks: 

        Disable Prod cluster queue (i.e. issue qmod -d all.q from dsh-sge2mast01)

        Perform package updates (i.e. issue dnf update script from dsh-rhldesk01d)

Monday 20 days after Patch Tuesday (T+20) = DSH Prod Cluster patch day

    Date: June 23, 2025

    Tasks:

        Perform updates and manual reboots for machines in Group 3 (see patching inventory)

        Perform Prod cluster health checks (see Wiki page)

        Re-enable the Prod cluster queue (i.e. issue qmod -e all.q from dsh-sge2mast01)

Wednesday 22 days after Patch Tuesday (T+22) = DSH NFS/file server patch day

    Date: June 25, 2025

    Tasks:

        Perform NFS/File server health checks (see Wiki page)

        Perform updates and manual reboots for machines in the “cluster” (file server) group, if necessary (see patching inventory)
