# Status of the cluster

This page outlines that status of the DSH cluster and the planned outages managed by the Beskpoke team at UCL.
We endeavour to keep this page as up-to-date as possible but there might be some delay. If you are experiencing 
issues with the cluster, feel free to report them to rc-support@ucl.ac.uk.

## DSH cluster status

  - 2025-06-05 - DSH cluster is working normally.
  - 2025-06-04 - We need to perform maintenance on some of our DSH host machines. The GPU-enabled virtual machines
    listed below will be unavailable from 5:30 pm Tuesday until end of day Wednesday:
    **dsh-00530gpu01, dsh-00965gpu02, dsh-01148app01, dsh-01534gpu01, dsh-sge2gpu01, dsh-sge2gpu02**.
    Please ensure that any long-term processes that you may be running are completed before end of day Tuesday to
    ensure the integrity of your results. The maintenance should be completed before end of day Wednesday.


## Planned outages for the DSH cluster 

Full details of unplanned outages are emailed to the cluster user list. 

The second Tuesday of every month is a RedHat patch release day, aka **Patch Tuesday**. In resposne to this, we perform maintenance in the cluster every month. 
This process starts in the afternoon of the Friday approx. two weeks (17 days) after **Patch Tuesday**. The DSH HPC cluster queue will be disabled on this Friday, 
this will prevent any new jobs from being submitted but will still allow existing jobs to be scheduled and run as normal. On the subsequent Monday morning, all cluster 
VMs will be taken offline for patching and maintenance -- note that any jobs that have not completed by this time will be forcibly interrupted, and may need to 
be re-submitted once the cluster resumes normal operation. This outage should only last a couple of hours on the Monday morning, and the system should resume normal 
operation before noon. If there is a notable delay in bringing the system back, we will contact you after approximately midday.

After an outage, the first day or two back should be considered 'at risk'; that is, things are more likely to go wrong without warning and we might need to make adjustments.

### List of planned outages

Date                | Status  | Reason 
--------------------|---------|--------
20 June 2025        | Planned | Queue of the cluster will be disabled for the weekend from 16:00 to apply the RedHat system updates. Jobs that will not be able to complete before the outage will be killed when the machines are rebooted.

### Previous Outages

Date                | Status    | Reason 
--------------------|-----------|--------
11 May 2025         | Completed | Maintenance day: Queue disabled for a system update. Update suscessfully completed and queue enabled.





