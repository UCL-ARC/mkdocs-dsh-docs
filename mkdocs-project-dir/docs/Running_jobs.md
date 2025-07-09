# Submitting a job

Create a jobscript for non-interactive use and submit your jobscript using qsub. Jobscripts must begin #!/bin/bash -l in order to run as a login shell and get your login environment and modules.

## How do I submit a job to the scheduler?

To submit a job to the scheduler you need to write a jobscript that contains the resources the job is asking for and the actual commands you want to run. This jobscript is then submitted using the `qsub` command.

```
qsub myjobscript
```

It will be put in to the queue and will begin running on the compute nodes at some point later when it has been allocated resources.

 You can also use options on the command-line to override options you have put in your job script.

| Command | Action |
|:--------|--------|
| `qsub myscript.sh`                 | Submit the script as-is  |
| `qsub -N NewName myscript.sh`      | Submit the script but change the job's name |
| `qsub -l h_rt=24:0:0 myscript.sh`  | Submit the script but change the maximum run-time |
| `qsub -hold_jid 12345 myscript.sh` | Submit the script but make it wait for job 12345 to finish |
| `qsub -ac allow=XYZ myscript.sh`   | Submit the script but only let it run on node classes X, Y, and Z |

## qsub emailing
We also have a mailing system that can be implemented to send emails with reminders of the status of your job through `qsub`. In your jobscript, or when you use `qsub` to submit your job, you can use the option `-m`. You can specify when you want an email sent to you by using the below options after `qsub -m`:

|   |   |
|---|---|
| `b` | Mail is sent at the beginning of the job. |
| `e` | Mail is sent at the end of the job. |
| `a` | Mail is sent when the job is aborted or rescheduled. |
| `s` | Mail is sent when the job is suspended. |
| `n` | No mail is sent. (The default.) |

You specify where the email should be sent with `-M`.

You can use more than one of these options by putting them together after the `-m` option; for example, adding the following to your job script would mean you get an email when the job begins and when it ends:

```
#$ -m be
#$ -M me@example.com
```

Further resources can be found here:

* [Scheduler fundamentals (moodle)](https://moodle.ucl.ac.uk/mod/page/view.php?id=4845666) (UCL users)
* [Scheduler fundamentals (mediacentral)](https://mediacentral.ucl.ac.uk/Play/98368) (non-UCL users)

### Job deletion

Use  `qdel` to delete a submitted job. You must give the job ID.

```
qdel 361829
```
You can also delete all the jobs from a user with 

```
qdel -u <username>
```

 To delete a batch of jobs, creating a file with the list of job IDs that you would like to delete and placing it in the following commands will delete the following jobs: `cat <filename> | xargs qdel`

 ### Why is my job in Eqw status?

If your job goes straight into Eqw state, there was an error in your jobscript that meant your job couldn't be started. The standard `qstat` job information command will give you a truncated version of the error:

```
qstat -j <job_ID>
```

The most common reason jobs go into this error state is that a file or directory your job is trying to use doesn't exist. Creating it after the job is in the `Eqw` state won't make the job run: it'll still have to be deleted and re-submitted.

 
### Asking for resources

#### Number of cores

For MPI:
```bash
#$ -pe mpi <number of cores>
```

For threads:
```bash
#$ -pe smp <number of cores>
```

For single core jobs you don't need to request a number of cores.

#### Memory requests (Amount of RAM per core)

Note: the memory you request is always per core, not the total amount. If you ask for 128GB RAM and 4 cores, that may run on 4 nodes using only one core per node. This allows you to have sparse process placement when you do actually need that much RAM per process.

If you want to avoid sparse process placement and your job taking up more nodes than you were expecting, the maximum memory request you can make when using all the cores in a standard node is 128/16 = 8G.

```bash
#$ -l mem=<integer amount of RAM in G or M>
```

e.g. `#$ -l mem=4G` requests 4 gigabytes of RAM per core.

#### Run time
```bash
#$ -l h_rt=<hours:minutes:seconds>
```

e.g. `#$ -l h_rt=48:00:00` requests 48 hours.

#### Working directory

Either a specific working directory:

```bash
#$ -wd /path/to/working/directory
```

or the directory the script was submitted from:

```bash
#$ -cwd
```

#### GPUs 

```bash 
#$ -l gpu=<number of GPUs>
```

### Passing in qsub options on the command line

The `#$` lines in your jobscript are options to qsub. It will take each line which has `#$` as the first two characters and use the contents beyond that as an option. 

You can also pass options directly to the qsub command and this will override the settings in your script. This can be useful if you are scripting your job submissions in more complicated ways.

For example, if you want to change the name of the job for this one instance of the job you can submit your script with:
```
qsub -N NewName myscript.sh
```

Or if you want to increase the wall-clock time to 24 hours:
```
qsub -l h_rt=24:0:0 myscript.sh
```

You can submit jobs with dependencies by using the `-hold_jid` option. For example, the command below submits a job that won't run until job 12345 has finished:
```
qsub -hold_jid 12345 myscript.sh
```

You may specify node type with the `-ac allow=` flags as below: 

```
qsub -ac allow=L myscript.sh
```

This command tells this GPU job to only run the type L nodes which have Nvidia A100s

```
qsub -ac allow=EF myscript.sh
```

This tells this GPU job to only run on the type E and F nodes which have Nvidia V100s.

<!--- provide an alternate example, e.g., using Myriad's or Kathleen's nodes  --->

Note that for debugging purposes, it helps us if you have these options inside your jobscript rather than passed in on the command line whenever possible. We (and you) can see the exact jobscript that was submitted for every job that ran but not what command line options you submitted it with.

## How do I monitor a job?

### qstat

The `qstat` command shows the status of your jobs. By default, if you run it with no options, it shows only your jobs (and no-one else’s). This makes it easier to keep track of your jobs. By adding in the option `-f -j <job-ID>` you will get more detail on the specified job.

The output will look something like this:
```
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
123454 2.00685 DI_m3      ccxxxxx      Eqw   10/13/2017 15:29:11                                    12 
123456 2.00685 DI_m3      ccxxxxx      r     10/13/2017 15:29:11 Yorick@node-x02e-006               24 
123457 2.00398 DI_m2      ucappka      qw    10/12/2017 14:42:12                                    1 
```

This shows you the job ID, the numeric priority the scheduler has assigned to the job, the name you have given the job, your username, the state the job is in, the date and time it was submitted at (or started at, if it has begun), the head node of the job, the number of 'slots' it is taking up, and if it is an array job the last column shows the task ID.

The queue name (`Yorick` here) is generally not useful. The head node name (`node-x02e-006`) is useful - the `node-x` part tells you this is an X-type node. 

If you want to get more information on a particular job, note its job ID and then use the -f and -j flags to get full output about that job. Most of this information is not very useful.
```
qstat -f -j 12345
```

#### Job states

-  `qw`: queueing, waiting
-  `r`: running
-  `Rq`: a pre-job check on a node failed and this job was put back in the queue
-  `Rr`: this job was rescheduled but is now running on a new node
-  `Eqw`: there was an error in this jobscript. This will not run.
-  `t`: this job is being transferred
-  `dr`: this job is being deleted
<!--- dRr  --->
<!--- hqw  --->

Many jobs cycling between `Rq` and `Rr` generally means there is a dodgy compute node which is failing pre-job checks, but is free so everything tries to run there. In this case, let us know and we will investigate. 

If a job stays in `t` or `dr` state for a long time, the node it was on is likely to be unresponsive - again let us know and we'll investigate.

A job in `Eqw` will remain in that state until you delete it - you should first have a look at what the error was with `qexplain`.

### More scheduler commands

Have a look at `man qstat` and note the commands shown in the `SEE ALSO` section of the manual page. Exit the manual page and then look at the `man` pages for those. (You will not be able to run all commands).

## How do I run interactive jobs?

Sometimes you need to run interactive programs, sometimes with a GUI. This can be achieved through `qrsh`.  We have a detailed guide to running [interactive jobs](Interactive_Jobs.md).

## How do I estimate what resources to request in my jobscript?

It can be difficult to know where to start when estimating the resources your job will need. One way you can find out what resources your jobs need is to submit one job which requests far more than you think necessary, and gather data on what it actually uses. If you aren't sure what 'far more' entails, request the maximum wallclock time and job size that will fit on one node, and reduce this after you have some idea. In the case for array jobs, each job in the array is treated independently by the scheduler and are each allocated the same resources as are requested. For example, in a job array of 40 jobs requesting for 24 hours wallclock time and 3GB ram, each job in the array will be allocated 24 hours wallclock time and 3GB ram. Wallclock time does not include the time spent waiting in the queue.

Run your program as:
```
 /usr/bin/time --verbose myprogram myargs
```
where `myprogram myargs` is however you normally run your program, with whatever options you pass to it.

When your job finishes, you will get output about the resources it used and how long it took - the relevant one for memory is `maxrss` (maximum resident set size) which roughly tells you the largest amount of memory it used.

Remember that memory requests in your jobscript are always per core, so check the total you are requesting is sensible - if you increase it too much you may end up with a job that cannot be submitted.

## How do I run a graphical program?

Unfortunately, at the moment it is not possible to run a graphical program in DSH cluster


