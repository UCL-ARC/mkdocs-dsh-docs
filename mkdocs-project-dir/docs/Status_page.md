---
layout: docs
---

# Status of the cluster

This page outlines that status of the DSH cluster managed by the Beskpoke team at UCL. We endeavour to keep this page as up-to-date as possible but there might be some delay. Also there are spontaneous errors that we have to deal with (i.e. high load on login nodes) but feel free to report them to rc-support@ucl.ac.uk. Finally, details of our planned outages can be found [here](https://www.rc.ucl.ac.uk/docs/Planned_Outages/).  

### DSH cluster

  - 2023-03-06 - Myriad's filesystem is getting full again, which will impact performance. If you are 
    able, please consider backing up and deleting any files that you aren't actively using for your 
    research for the time being.
    
    You can check your quota and see how much space you are using on Myriad with the `lquota` command, 
    and you can see which directories are taking the most space using the `du` command, which can also 
    be run in specific directories. You can tell `du` to only output details of the first level of 
    directory sizes with the `--max-depth=1` option.
    
    Jobs are still running for the moment, but if the filesystem keeps getting fuller we may need to 
    stop new jobs running until usage is brought down again.

  - 2023-07-31 12:30 - Myriad's filesystem is currently being very slow because we have two failed 
    drives in the Object Store Target storage. One drive has fully failed and the volume is under 
    reconstruction. The other has been detected as failing soon and is being copied to a spare, but
    this is happening slowly, likely because the disk is failing.

    They are in separate volumes so there isn't a risk there, but it can take some time for 
    reconstruction to complete and this will make the filesystem sluggish. This will affect you 
    accessing files on the login nodes, and also your jobs reading or writing to files on Scratch 
    or home, and accessing our centrally-installed software. (It won't affect writing to `$TMPDIR`,
    the local hard disk on the compute node).

    Once the reconstruction is complete, performance should return to normal. This could take most 
    of the day and potentially continue into tomorrow.

  - 2023-08-01 11:00 - We have had a report of another impending disk failure in the same volume as
    the first failed disk, which puts data at risk. The volume reconstruction is still in progress 
    and expected to take another 30-odd hours. (The second copy to spare has completed).

    We have stopped Myriad from running jobs to reduce load on the filesystem while the 
    reconstruction completes, so no new jobs will start for the time being. We'll keep you updated 
    if anything changes.

  - 2023-08-03 10:30 - We have another estimated 18 hours of volume reconstruction to go, so we are
    leaving jobs off today. On Friday morning we will check on the status of everything and 
    hopefully be able to re-enable jobs then if all is well.

  - 2023-08-04 10:00 - The reconstruction is complete and we have re-enabled jobs on Myriad.

  - 2023-11-23 14:00 - We need to stop new jobs running on Myriad while its filesystem recovers.

    This means that jobs that are already running will keep running, but new jobs will not start 
    until we enable them again. The filesystem is likely to be slower than usual. You can still log 
    in and access your files.

    This is because we've just had two disks fail in the same area of Myriad's filesystem and the 
    draining of jobs is to reduce usage of the filesystem while it rebuilds onto spare disks.

    The current estimated time for the disk rebuild is 35 hours (but these estimates can be 
    inaccurate).

    We will update you when new jobs can start running again.

  - 2023-11-24 09:45 - **Myriad filesystem is down.** 

    I'm afraid Myriad's filesystem is currently down. You will not be able to log in and jobs are 
    stopped.

    A third disk failed in the same area as the last two and we started getting errors that some 
    areas were unreadable and reconstruction failed. We need to get this area reconstructed so are 
    in contact with our vendors.

    **Detail**

    Our parallel filesystem is Lustre. It has Object Storage Targets that run on the Object 
    Storage Servers. Data gets striped across these so one file will have pieces in multiple 
    different locations, and there is a metadata server that keeps track of what is where. One of 
    the Object Storage Targets has lost three disks, is unreadable and is what needs to be 
    reconstructed. While it is unavailable, the filesystem does not work. We will also have some 
    amount of damaged files which have pieces that are unreadable.

    If the reconstruction succeeds, we will then need to clear out the unreadable sectors. Then we 
    will be able to start checking how much damage there is to the filesystem.

    This is all going to take some time. We will update you again on Monday by midday, but there 
    may be no new information by then.

    I'm sorry about this, we don't know right now how long an interruption this will cause to 
    service, or how much data we may have lost.

    Please send any queries to rc-support@ucl.ac.uk 

  - 2023-11-27 12:10 - There is not much of an update on Myriad's filesystem yet - we've been in 
    contact with our vendors, have done some things they asked us to (reseating hardware) and are 
    waiting for their next update.

    In the meantime, we are starting to copy the backup of home that we have from the backup system
    where it is very slow to access to somewhere faster to access, should we need to recover files 
    from it on to Myriad.

    We received a question about backups - the last successful backup for Myriad home directories 
    ran from Nov 20 23:46 until Nov 22 03:48. Data before that interval should be backed up. Data 
    after that is not. Data created or changed during it may be backed up, it depends on which 
    users it was doing when.

    (Ideally we would be backing up every night, but as you can see the backup takes longer than a 
    day to complete, and then the next one begins. The next backup had started on Nov 22 at 08:00 
    but did not complete before the disk failures).

  - 2023-11-29 11:30 Today's Myriad filesystem update:

    * We are continuing to meet with our vendor and have sent them more data to analyse.

    * We are going to copy over the failed section of filesystem to a new area, with some data 
      loss, so we end up with a working volume that we can use to bring the whole filesystem back 
      up.

    * The copy of data from our backup location to easier access location is ongoing (we have 
      48TiB of home directories consisting of 219M items, currently copied ~~15TiB~~ 7.5TiB and 27M 
      items).

    Date of next update: Monday 4 Dec by midday.

    Myriad will definitely not be back up this week, and likely to not be back up next week - but 
    we'll update you on that. The data copying all takes a lot of time, and once it is there, we 
    need to run filesystem checks on it which also take time.

  - 2023-12-04 12:30 - The data copying is continuing.

    * The copy of the failed section of filesystem to a new area is at 33% done, expected to take 
      4.5 days more.

    * The copy of home directories from our backup location to easier access location is at 
      ~~44TiB~~ 22TiB (GPFS was reporting twice the real disk usage) 
      and 86M items out of 48TiB and 219M. It is hard to predict how long that may take, as the 
      number of items is the bottleneck. It has been going through usernames in alphabetical order 
      and has reached those starting "ucbe".

    If the first of these copies completes successfully, we will then need to go through a 
    filesystem check. This will also take possibly a week or more - it is difficult to predict 
    right now. If this recovery continues as it has been and completes successfully, it looks like 
    we may have lost a relatively small proportion of data - but we cannot guarantee that at this 
    stage, and the copy has not completed.

    So at present we expect to be down at least all of this week, and all of next week - and 
    possibly into the week of the 18th before UCL's Christmas closing on the 22nd.

    I'm sorry about this - with these amounts of data and numbers of files, it gets difficult to 
    predict how long any of these operations will take.

    We've had a couple of questions about whether there is any way people can get their data from 
    Myriad - until the filesystem is reconstructed and brought back up, we cannot see separate 
    files or directories on Myriad.

  - 2023-12-12 15:00 - First data copy complete.

    * The copy of the failed section of filesystem has completed and is showing at 99.92% rescued, 
      leaving around 75GB of data as not recoverable. (At present we don't know what this data is -
      it could be from all of home, Scratch, shared spaces and our application install area).

    * The copy of home directories from our backup location to easier access location is still 
      going, currently at 42.5TiB and 166M items out of 48TiB and 219M. My earlier reports had 
      doubled the amount we had successfully copied, so when I said 44TiB previously, that was only
      22TiB. (Corrected in this page). This is progressing slowly and has stalled a couple of times.

    We next need to bring the filesystem up so we can start running checks and see what files are 
    damaged and missing. We will be discussing our next steps to do this with our vendor. 

    I intend to send another update this week, before the end of Friday. 

  - 2023-12-15 17:20 - No news, Christmas closing.
    
    No news, I'm afraid. It is looking like Myriad's filesystem will definitely remain down over 
    Christmas.

    * Our vendors are investigating filesystem logs.

    * The copy of home directories from our backup location to easier access location appears to 
      have finished the copying stage but was still doing some cleanup earlier today.

    UCL is closed for Christmas from the afternoon of Friday 22 December until 9am on Tuesday 2 
    January. Any tickets received during this time will be looked at on our return.

    We will send an update next week before UCL closes.

  - 2023-12-18 15:30 - Home directories from backup available

    We have restored Myriad HOME directories only (no Scratch, Projects or
    Apps) from the most recent back up which ran from:
 
    Monday Nov 20 23:46 to Wednesday Nov 22 03:48
 
    They are mounted READ ONLY on the Myriad login nodes so you can login
    to check what files are missing or need updating and scp results etc
    back to your local computer. We apologize for the delay in making this
    data available, unfortunately the restore process was only finished during
    the weekend.
 
    Work on restoring more data (i.e. HOME from after the backup, as well
    as Scratch and Projects) is still in progress.
 
    It is currently not possible to run jobs.
 
    We still don't expect Myriad to be restored to service before the
    Christmas and New Year UCL closure.
 
    UCL is closed for Christmas from the afternoon of Friday 22 December until 9am on Tuesday 2 
    January. Any tickets received during this time will be looked at on our return.

  - 2023-12-22 15:00 - A final Myriad update before UCL closes for the Christmas and New Year break.
 
    The copy of rescued data back onto the re-initialised volume completed this morning (Friday 
    22nd). We are now running filesystem checks. Myriad will remain down during the Christmas and 
    New Year closure apart from the read only HOME directories as detailed previously.

  - 2024-01-05 16:50 - An update on the status of Myriad before the weekend

    We wanted to give you a quick update on the progress with Myriad before the weekend as we 
    know several of you are asking for one.
 
    We are meeting on Monday morning to consider options for returning the live filestore 
    including Apps, HOME, Scratch and projects to service. We should have some rough timescale we 
    can give you later on Monday.
 
    Currently a scan is running to discover which files existed either wholly or in part on the 
    failed volume. So far this has discovered around 60M files, and the scan is about halfway. This 
    will carry on running over the weekend. Unfortunately, there is likely to be significant data 
    loss from your Scratch directories.
 
    We will send another update later on Monday.

  - 2024-01-08 17:50 - Myriad update (Monday)
 
    We met this morning to discuss options for returning the live filestore including Apps, HOME, 
    Scratch and projects to service. Tentatively we hope to be able to allow you access to your 
    HOME, Scratch and projects by the end of this week.
 
    The scan to discover which files existed either wholly or in part on the failed volume has 
    completed and found about 70M files which is around 9.1% of the files on Myriad. We are 
    planning to put files in your HOME directory:
 
    One listing the missing files from your HOME directory.
 
    One listing the missing files from your Scratch directory.
 
    There are also missing files in projects so if you own a project we will give you a list of 
    these too.

  - 2024-01-11 12:30 - Jobs on Myriad

    We've had questions from you about when jobs will be able to restart. We were able to assess 
    the damage to our software stack yesterday and most of the centrally installed applications 
    are affected by missing files and need to be copied over from other clusters or reinstalled.

    We're going to begin by copying over what we can from other systems. We'll be looking at the 
    results of this first step and seeing how much is still missing after it and how fundamental 
    those packages are. 

    It would be possible for us to enable jobs before the whole stack was reinstalled, but we need 
    enough there for you to be able to carry out useful work. We should have a much better idea of 
    what is still missing by Monday and our plans for reinstating it. I would rather lean towards 
    giving you access sooner with only the most commonly-used software available rather than 
    waiting for longer.

    We're on schedule for giving you access to your files by the end of this week.

    New user accounts will start being created again once jobs are re-enabled.

    I'll also be sending an update in the next few days about our future filesystem plans and 
    mitigations we were working on before this happened.

#### Check lists of damaged files on Myriad

  - 2024-01-12 14:00 Myriad: filesystem access restored, jobs tentatively expected for Monday

    We've restored read-write access to Myriad's filesystem, and you will be able to log in and 
    see all your directories again. Here's some detail about how you can identify which of your 
    files were damaged.

    **Your data on Myriad**

    During the incident all files that resided at least partially on OST00 have been lost. 
    In total these are 70M files (out of a filesystem total of 991M).

    We restored files in `/lustre/home` from the latest backup where available. Data that was 
    created while the backup was running or afterwards had no backup and could not be restored. 
    For the time being, we will keep the latest backup available read-only in the directory 
    `/lustre-backup`.

    Files in `/lustre/scratch` and `/lustre/projects` were not backed up, as a matter of policy. 
    All OST00 files from these directories have been lost.

    Where files were lost but still showing up in directory listings, we have removed ("unlinked") 
    them so it doesn't appear that they are still there when they are not.

    For a tiny fraction of the lost files (0.03%), there is still some file data accessible, but 
    most of these files are damaged (e.g. truncated or partially filled with zeroes). For some 
    users these damaged files might still contain useful information, so we have left these files 
    untouched.

    The following files have been placed into your home directory:

     - OST00-FILES-HOME-restored.txt
         - A list of your home directory files that resided on OST00 and that were successfully 
         restored from backup.

     - OST00-FILES-HOME-failed.txt
         - A list of your home directory files that resided on OST00 and that could not be restored 
           from backup, including one of the following messages:
         - "no backup, stale directory entry, unlinked" - There was no backup for this file, and we 
           removed the stale directory entry.
         - "target file exists, potentially corrupt, leaving untouched" - Original file data is still 
           accessible, but likely damaged or corrupt. Feel free to delete these files if there's no 
           useful data in there.

     - OST00-FILES-SCRATCH.txt
         - A list of your Scratch directory files that resided on OST00, including one of the 
           following messages (similar to the above):
         - "stale directory entry, unlinked"
         - "file exists, potentially corrupt, leaving untouched"

    For projects, the following file has been placed in the project root directory:

     - OST00-FILES-PROJECTS.txt
         - A list of project files that resided on OST00, including one of the following messages:
         - "stale directory entry, unlinked"
         - "file exists, potentially corrupt, leaving untouched"

    A very few users had newline characters (`\n`) in their filenames: in this case in the above 
    .txt files the `\n` has been replaced by the string `__NEWLINE__`, and an additional .bin file 
    has been placed alongside the .txt file, containing the list of original filenames terminated 
    by null bytes (and not including the messages).

    These OST00-FILES-* files are owned by root, so that they don't use up any of your quota. 
    You can still rename, move, or delete these files.

    **Jobs**

    We're currently running a Lustre filesystem check in the background. Provided it does not throw 
    up any serious problems, we expect to be able to re-enable jobs during Monday. We'll be putting
    user holds on all the jobs so you can check that the files and applications they are trying to 
    use exist before allowing them to be scheduled. They will show in status `hqw` in qstat.

    Once you have made sure they are ok, you will be able to use `qrls` followed by a job ID to 
    release that job, or `qrls all` to release all your jobs. They will then be in status `qw` and 
    queue as normal. (Array jobs will have the first task in status `qw` and the rest in `hqw` - 
    this is normal). If you want to delete the jobs instead, use `qdel` followed by the job ID.

    **Software**

    We have successfully restored the vast majority of Myriad's software stack. I'll send a final 
    update when we re-enable jobs, but at present I expect the missing applications to be:
 
     - ABAQUS 2017
     - ANSYS (all versions)
     - STAR-CCM+ (all versions)
     - STAR-CD (all versions)

    These are all licensed applications that are best reinstalled from their original media, so 
    we'll be working through those, starting with the most recent version we had.

    Please send any queries to rc-support@ucl.ac.uk. If you've asked us for account deletions, we 
    will be starting those next week, along with new user account creations.

  - 2024-01-15 16:00 - Myriad jobs enabled

    We have now allowed jobs to start on Myriad. 

    We have reinstalled ABAQUS 2017, ANSYS 2023.R1, STAR-CCM+ 14.06.013 and STAR-CD 4.28.050. The 
    older versions of these applications are still missing at the moment.

    Your jobs that were still in the queue from before have user holds on them and show in status 
    `hqw` in qstat.

    Once you have made sure the files and applications the jobs are using are present and correct, 
    you will be able to use `qrls` followed by a job ID to release that job, or `qrls all` to 
    release all your jobs. They will then be in status `qw` and queue as normal. (Array jobs will 
    have the first task in status `qw` and the rest in `hqw` - this is normal). If you want to 
    delete the jobs instead, use `qdel` followed by the job ID.

    User deletions and new user creations are underway. We'll need to check that the 
    synchronisation to the mailing list is working correctly and people are being added and removed
    as appropriate.

#### Action required - compression or removal of data

  - 2024-10-18 13:55 - **Action required: compression or removal of data on Myriad**

    Myriad's filesystem is too full, so we need everyone to check what data they are keeping on the 
    cluster and to remove data they are not currently using. To perform effectively, the filesystem 
    needs a significant portion of empty space. As it gets fuller, performance begins to get worse 
    and then stability also decreases. 

    The filesystem is at 70% full, and we will need to stop jobs running when it reaches 75%. (1% of 
    the filesystem is 19.4 TiB).

    Keeping data unnecessarily on the system affects everyone's ability to run jobs.

    We will also be contacting those of you with large amounts of data separately.

    **How to check usage and compress data**

    You can check your quota and see how much space you are using on Myriad with the lquota command, 
    and you can see which directories are taking the most space using `du -h` which can also be run 
    in specific directories. You can tell du to only output details of the first level of directory 
    sizes with the `--max-depth=1` option.

    If you cannot remove your data from the cluster, please consider whether you can archive and 
    compress any of it for the time being.

    Example to tar up and gzip compress a directory:

    - `tar -czvf /home/username/Scratch/myarchive.tar.gz /home/username/Scratch/work_data` 
      will (c)reate a g(z)ipped archive (v)erbosely in the specified (f)ilename location. The 
      contents will be everything in this user's `work_data` directory.

    You can request bzip2 compression instead with `-j` or `--bzip2` and `xz` compression with `-J` 
    or `--xz`. These will give you better compression than gzip, with xz generally being the most 
    compressed.

    If you are compressing an individual file rather than a directory, you can use the `gzip`, 
    `bzip2` and `xz` commands on their own without tar.

    (Have a look at `man tar` or gzip, bzip2 and xz for the manual page details - they also contain 
    the names of the uncompress commands).

    If you are transferring data to Windows and want to uncompress the data there, 7-zip can open 
    all of these formats. Or you can create your archives using the `zip` command.

    **Quota policies**

    We are going to be adjusting the policies for granting Scratch quota increases - the CRAG will 
    be granting them for shorter periods of time and will not be as easily re-granting increases at 
    the end of that time period. We will have a process for what happens when a quota increase 
    expires, including notifications to you. You will be asked to consider your plans for what to 
    do with the data when the quota increase expires at the time of requesting one.

    We are also going to be setting up annual account reapplications again, so we can identify 
    users who are no longer using the system and activate our account deletion policies.

    This is to prevent the current situation where new users to the system cannot get relatively 
    small and short term quota increases necessary for their work because increases granted in the 
    past are still using the space.

    **ARC Cluster File System (ACFS)**

    Timelines for access to the ARC Cluster Filesystem (ACFS) from Myriad are currently being 
    considered. There is some info about the ACFS at 
    [ARC Cluster File System](https://www.rc.ucl.ac.uk/docs/Background/Data_Storage/#arc-cluster-file-system-acfs) 

    The ACFS once available from Myriad will give you 1T in total of backed-up data (and your home 
    directories will no longer be backed up). For those of you with larger Scratch quota increases, 
    you will still need to consider what you will do with the bulk of your data. 

    **Info**

    We recently added some pages to our documentation which may be relevant:

    - [Parallel Filesystems](https://www.rc.ucl.ac.uk/docs/Background/Parallel_Filesystems/) includes 
      sections on working effectively with parallel filesystems and tips for use.
    - [Data Storage](https://www.rc.ucl.ac.uk/docs/Background/Data_Storage/) - what storage locations exist.
    - [Data Management](https://www.rc.ucl.ac.uk/docs/Data_Management/) - checking quotas, transferring 
      data to other users, requesting data from those who have left.

    Please email rc-support@ucl.ac.uk with any queries or raise a request about Myriad via 
    [UCL MyServices](https://myservices.ucl.ac.uk/). If you are no longer using the cluster and 
    wish to be removed from this mailing list, please also contact us and say we can delete your account.

  - 2024-10-25 18:20 - Filesystem issues on Myriad

    We have been having some filesystem issues since around 16:50.

    One of the servers that is part of the filesystem kept crashing, we had a failover and then the new 
    active one crashed as well. This will be preventing logins and jobs will have failed.

    Depending on what is happening, we may not be able to sort this out until Monday and if access is 
    restored it may be unstable throughout the weekend.

  - 2024-10-28 10:20 - Filesystem recovered

    The filesystem recovered on Friday evening and was running ok over the weekend. 

    While it was down, it is likely that many running jobs failed with I/O errors. There will also be 
    numbers of them in state `dr` which we need to reboot the nodes to clear.

    At the moment we're still seeing some leftover activity in the logs but there don't appear to be any 
    active problems.

  - 2024-11-12 17:20 - **Myriad filesystem and refresh news; ACFS available now**

    **The ARC Cluster File System (ACFS) is now available on Myriad.**

    The ARC Cluster File System (ACFS) is ARC's centralised storage system that will be available from 
    multiple ARC systems. If you also have a Kathleen account and already put some data in the ACFS, you 
    will now be able to see that data on Myriad too.

    It is the backed-up location for data which you wish to keep.

    The ACFS is available read-write on the login nodes but read-only on the compute nodes. This means 
    that your jobs can read from it, but not write to it, and it is intended that you copy data onto it 
    after deciding which outputs from your jobs are important to keep.

    * Location: `/acfs/users/<username>`
    * Also at: `/home/<username>/ACFS` (a shortcut or symbolic link to the first location).
    * Backed up daily.
    * 1T quota - no quota increases available on ACFS at present.
    * Check your ACFS quota with `aquota`.

    The ACFS has dual locations for resilience, and as a result commands like `du -h` or `ls -alsh` will 
    report filesizes on it as being twice what they really are. The `aquota` command will show you real 
    usage and quota.

    * [Data Storage - ACFS](Background/Data_Storage.md#arc-cluster-file-system-acfs)
    * [Data Management - ACFS quotas](Data_Management.md#acfs-quotas)

    **Until Myriad's filesystem is replaced, your home will continue to be backed up.** After the new 
    filesystem is available, only the ACFS will be backed up.

    Please move some of your current data to the ACFS to reduce the usage on Myriad's Scratch.

    **Myriad refresh and new filesystem**

    The Myriad refresh is going ahead, and we will be adding some new compute nodes to Myriad as well 
    as replacing the filesystem, networking and admin nodes.

    We expect the new filesystem to go live during March 2025. Prior to that, we will be conducting 
    setup, tuning and testing behind the scenes. (We expect the hardware to arrive in December or first 
    week of January depending on delivery windows).

    We expect the new compute nodes to also go live during March 2025 - they will be purchased and 
    arrive later than the filesystem, but their testing period should coincide.

    The new filesystem will be GPFS. The new compute nodes will be AMD EPYC 64 core, ~750G RAM, with 
    ~950G local disk for tmpfs. Some of the oldest nodes will be removed (eg types H, I, J which are 
    nodes named node-h, node-i, node-j).

    Timescales are based on our current knowledge and best estimates!

    There will be many software changes as part of this refresh as well - we will be updating the 
    operating system, changing the scheduler to Slurm and refreshing the software stack. More details 
    nearer the time.

    **Action required - compression or removal of data**

    Myriad's filesystem is still at 70% full and we need to stop jobs at 75% full. Please continue to 
    look at [our previous message with full info](#action-required-compression-or-removal-of-data) and 
    move data to the ACFS, off-cluster, or compress it if possible.

  - 2025-02-10 - **OS, software stack, scheduler and hardware update news**

    This is to keep you informed about upcoming changes to Myriad.

    **Live now:**

    * Research Data Storage Service mount point on login nodes
    * Open OnDemand pilot access available on request until OS upgrade

    If you have an RDSS project, you can now access that read-write on the Myriad login nodes at `/rdss`. 
    There are subdirectories `rd00`, `rd01` that contain projects with names beginning 
    `ritd-ag-project-rd00` or `ritd-ag-project-rd01` and so on. You cannot access it from the compute 
    nodes. You should `cp` or `rsync` data to your home, Scratch or the ACFS via the login nodes before 
    doing any computation using the data.

    If you want to access our [Open OnDemand pilot](https://www.rc.ucl.ac.uk/docs/Supplementary/OnDemand/) 
    for a remote desktop, Jupyter Notebooks or RStudio, contact rc-support@ucl.ac.uk and we will give you 
    access. Please fill in the feedback survey if you use it. This will be used to prioritise whether we 
    redo the work to set it up after the OS upgrade or concentrate on other improvements.

    **Incoming:**

    * OS upgrade to RHEL 9.5
    * Scheduler move to Slurm
    * New software via Spack
    * Alteration to hardware refresh schedule

    We will be moving to RHEL 9.5 as our operating system and Slurm as our new scheduler. The new 
    filesystem below will be available before this is rolled out on Myriad.

    If you have access to paid priority time on Myriad, we will stop using Gold for this and use Slurm 
    mechanisms for priority allocations instead. You will receive the equivalent resource.

    Our user documentation will be updated with examples of Slurm jobscripts instead of the SGE ones we 
    currently have. Slurm uses `srun` and `sbatch` commands instead of `qsub`, if you have come across 
    those in other software documentation.

    The OS upgrade should allow you to run more recent binaries that currently give errors about GLIBC 
    being too old. System tools will be newer and may look a little different.

    We are also creating a new small software stack built with Spack. This will available to you to test 
    before the OS upgrade, then rebuilt again after it, so it will change slightly in the meantime. Do 
    let us know if applications you use in it are missing options we currently have or not working as 
    you expect. 

    Most of the existing software stack will be reinstalled for the new OS. We are looking to remove 
    some of the oldest installs and modules that are not being used in jobs. We then intend to prune 
    this further over time and add newer versions into the Spack stack.

    **Alteration to hardware refresh schedule**

    The oldest nodetypes (H,I,J) in Myriad have been drained of jobs as planned and are being removed 
    to make space in the racks.

    The new Myriad filesystem is in place, undergoing its final testing period and we should have 
    information on 24 Feb for timescales when you can expect to begin using it.

    We are still adding new hardware to Myriad for general use, but it will not be added in March/April 
    as previously stated. Instead, we will be replacing all Myriad's network hardware first, and then 
    getting the new standard compute nodes in the next UCL financial year after August 2025. The specs 
    for the new compute nodes are:

    * AMD EPYC 9554P 64C 360W 3.1GHz (64 cores)
    * 768G RAM
    * 2x 480GB M.2 7450 PRO NVMe SSD (960G local disk)

    Note, this does not affect timelines for any paid nodes and those can still go in before this. It 
    is to split the purchase over financial years rather than any issue with hardware supply times.

    There is some additional hardware that we may be able to make available to increase general use 
    Myriad capacity in the intervening period. The details need working out and that will take a few 
    months. The OS and scheduler upgrade will need to happen first.

    **Maintenance day Tues 11 Feb**

    The nodes are being drained for a system config change this maintenance day - they'll be rebooted 
    and jobs restarted after each is updated. There will also be a reboot of switches in the ACFS that 
    will cause the ACFS mount on Myriad to hang for a period during the day. This is listed at 
    [Planned Outages](https://www.rc.ucl.ac.uk/docs/Planned_Outages/ )

    **Documentation links**

    The SSL certificate for www.rc.ucl.ac.uk is due to expire at midnight on 12 Feb. We're getting a 
    new one but there might be a gap if it can't be renewed in time. If that happens your browser may 
    prevent you accessing that link because the certificate is expired.

    * [mkdocs-rc-docs on Github](https://github-pages.arc.ucl.ac.uk/mkdocs-rc-docs/) will work

    If there is a gap when the certificate expires we'll update the links in the message you see when 
    you log in to the cluster, but if you are using an existing link or bookmark for www.rc.ucl.ac.uk 
    at that point you will get an error or warning about the expired certificate.

    (This did not happen, the certificate was renewed in time).

#### Latest on Myriad

    2025-03-05 - **Myriad new filesystem update**

    The Myriad new filesystem is going to have a system update before we put it into production - the 
    new version fixes a number of security vulnerabilities, and it will be less disruptive to your 
    jobs if we do this before you have access to it. We also have some minor hardware issues that have 
    failed deployment checks that we are getting resolved with our vendors.

    We're currently expecting to be able to give you access to the new filesystem around **31 March**, 
    assuming all goes well with the above updates and the remaining snagging issues.

    **What will happen?**

    When the new filesystem goes live, you'll log in and will see a new empty home and Scratch. Your 
    old home and Scratch will be available read-only at `/old_lustre/home/username` and 
    `/old_lustre/scratch/username`. You'll be able to copy or rsync data out of it to the new 
    filesystem, to the ACFS or archive it elsewhere. You will not be able to modify or delete the data 
    in `/old_lustre`.

    Your new home directory will not be backed up. The ACFS will remain as your backed-up location.

    `/old_lustre` will remain available for three months after the new filesystem go-live date and will 
    then be removed. 

    All jobs will be held in the queue and you'll be able to remove the holds yourself when the data 
    they need is in the right place on the new filesystem.

    Information on how best to do the data moving will be sent nearer the time and added to the documentation.

    **Quota expiry on the new filesystem**

    For the new filesystem we will be updating our policy on what happens when increased quotas expire 
    and are not renewed. This will involve moving your user data off Myriad's filesystem to another 
    location temporarily, and then deletion of it on specified timescales. This is to avoid the new 
    filesystem filling up with data which is no longer being worked on and to allow those of you who are 
    actively using an increased quota to be able to have the space you need.

    Myriad's filesystem is not a long-term data store - if you are using the data in your jobs, that is 
    fine. If you are no longer using Myriad to do computations on the data, it shouldn't be left on 
    Myriad's filesystem.

    You will receive multiple notifications before and after your quota expires if this is happening.

    Further details on this to come. A similar process will take place when your Myriad user account 
    expires.




