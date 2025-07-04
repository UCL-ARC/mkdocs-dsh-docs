# Submitting a job

Create a jobscript for non-interactive use and submit your jobscript using qsub. Jobscripts must begin #!/bin/bash -l in order to run as a login shell and get your login environment and modules.

## How do I submit a job to the scheduler?

To submit a job to the scheduler you need to write a jobscript that contains the resources the job is asking for and the actual commands you want to run. This jobscript is then submitted using the `qsub` command.

```
qsub myjobscript
```

It will be put in to the queue and will begin running on the compute nodes at some point later when it has been allocated resources.



### Preventing a job from running cross-CU

If your job must run within a single CU, you can request the parallel environment as `-pe wss` instead of `-pe mpi` (`wss` standing for 'wants single switch'). This will increase your queue times. It is suggested you only do this for benchmarking or if performance is being greatly affected by running in the superqueue.



### Job deletion

If you `qdel` a submitted Gold job, the reserved Gold will be made
available again. This is done by a cron job that runs every 15 minutes,
so you may not see it back instantly.


### Memory requests

Note: the memory you request is always per core, not the total amount. If you ask for 192GB RAM and 40 cores, that may run on 40 nodes using only one core per node. This allows you to have sparse process placement when you do actually need that much RAM per process.

Young also has high memory nodes, where a job like this may run.

If you want to avoid sparse process placement and your job taking up more nodes than you were expecting, the maximum memory request you can make when using all the cores in a standard node is 4.6G.


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

The `qstat` command shows the status of your jobs. By default, if you run it with no options, it shows only your jobs (and no-one else’s). This makes it easier to keep track of your jobs. 

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

### qexplain

This is a utility to show you the non-truncated error reported by your job. `qstat -j` will show you a truncated version near the bottom of the output.

```
qexplain 123454
```

### qdel

You use `qdel` to delete a job from the queue.

```
qdel 123454
```

You can delete all your jobs at once:
```
qdel '*'
```

### More scheduler commands

Have a look at `man qstat` and note the commands shown in the `SEE ALSO` section of the manual page. Exit the manual page and then look at the `man` pages for those. (You will not be able to run all commands).

### nodesforjob

This is a utility that shows you the current percentage load, memory used and swap used on the nodes your job is running on. If your job is sharing the node with other people's jobs, it will show you the total resources in use, not just those used by your job. This is a snapshot of the current time and resource usage may change over the course of your job. Bear in mind that memory use in particular can increase over time as your job runs.

If a cluster has hyperthreading enabled and you aren't using it, full load will show as 50% and not 100% - this is normal and not a problem.

For a parallel job, very low (or zero) usage of any of the nodes suggests your job is either not capable of running over multiple nodes, or not partitioning its work effectively - you may be asking for more cores than it can use, or asking for a number of cores that doesn't fit well into the node sizes, leaving many idle.

```
[uccacxx@login02 ~]$ nodesforjob 1234
Nodes for job 1234:
  Primary:
    node-r99a-238:  103.1 % load, 12.9 % memory used, 0.1% swap used
  Secondaries:
    node-r99a-206:  1.7 % load, 1.6 % memory used, 0.1% swap used
    node-r99a-238:  103.1 % load, 12.9 % memory used, 0.1% swap used
    node-r99a-292:  103.1 % load, 12.9 % memory used, 0.1% swap used
    node-r99a-651:  1.6 % load, 3.2 % memory used, 0.1% swap used
```
The above example shows a multi-node job, so all the usage belongs to this job itself. It is 
running on four nodes, and node-r99a-238 is the head node (the one that launched the job) and 
shows up in both Primary and Secondaries. The load is very unbalanced - it is using two nodes 
flat out, and two are mostly doing nothing. Memory use is low. Swap use is essentially zero.

### jobhist

Once a job ends, it no longer shows up in `qstat`. To see information about your finished jobs - 
when they started, when they ended, what node they ran on - use the command `jobhist`, part of
the [`userscripts`](Installed_Software_Lists/module-packages.md) module.

```
[uccacxx@login02 ~]$ jobhist
        FSTIME        |       FETIME        |   HOSTNAME    |  OWNER  | JOB NUMBER | TASK NUMBER | EXIT STATUS |   JOB NAME    
----------------------+---------------------+---------------+---------+------------+-------------+-------------+---------------
  2020-06-17 16:31:12 | 2020-06-17 16:34:19 | node-h00a-010 | uccacxx |    3854822 |           0 |           0 | m_job   
  2020-06-17 16:56:50 | 2020-06-17 16:56:52 | node-d00a-023 | uccacxx |    3854836 |           0 |           1 | k_job  
  2020-06-17 17:21:12 | 2020-06-17 17:21:46 | node-d00a-012 | uccacxx |    3854859 |           0 |           0 | k_job
```

`FSTIME` - when the job started running on the node
`FETIME` - when the job ended
`HOSTNAME` - the head node of the job (if it ran on multiple nodes, it only lists the first)
`TASK NUMBER` - if it was an array job, it will have a different number here for each task

This shows jobs that finished in the last 24 hours by default. You can search for longer as well:
```
jobhist --hours=200
```

If a job ended and didn't create the files you expect, check the start and end times to see whether 
it ran out of wallclock time. 

If a job only ran for seconds and didn't produce the expected output, there was probably something 
wrong in your script - check the `.o` and `.e` files in the directory you submitted the job from 
for errors.

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

If your job is not completing successfully or you need to know how the memory usage 
changes throughout the job, there is a tool called [Ruse](https://github.com/JanneM/Ruse)
that can measure this for you.

Run your program as:
```
module load ruse/2.0

# sample the current memory usage every 120s and output each step to stdout
ruse --stdout --time=120 -s myprogram myargs
```
where `myprogram myargs` is however you normally run your program, with whatever options you 
pass to it.

Remember that memory requests in your jobscript are always per core, so check the total you are requesting is sensible - if you increase it too much you may end up with a job that cannot be submitted.

You can also look at [nodesforjob](#nodesforjob) while a job is running to see a snapshot of the memory, swap and load on the nodes your job is running on.

## How can I see what types of node a cluster has?

As well as looking at the cluster-specific page in this documentation for more details (for example 
[Myriad](Clusters/Myriad.md)), you can run `nodetypes`, which will give you basic information about 
the nodes that exist in that cluster.

```
[uccacxx@login12 ~]$ nodetypes
    3 type * nodes: 36 cores, 188.4G RAM
    7 type B nodes: 36 cores,   1.5T RAM
   66 type D nodes: 36 cores, 188.4G RAM
    9 type E nodes: 36 cores, 188.4G RAM
    1 type F nodes: 36 cores, 188.4G RAM
   55 type H nodes: 36 cores, 188.4G RAM
    3 type I nodes: 36 cores,   1.5T RAM
    2 type J nodes: 36 cores, 188.4G RAM
```

This shows how many of each letter-labelled nodetype the cluster has, then the number of cores 
and amount of memory the node is reporting it has. It also shows the cluster has some utility 
nodes - those are part of the infrastructure. The `*` nodes are the login nodes.


## How do I run a graphical program?

To run a graphical program on the cluster and be able to view the user interface on your own 
local computer, you will need to have an X-Windows Server installed on your local computer and 
use X-forwarding.

### X-forwarding on Linux

Desktop Linux operating systems already have X-Windows installed, so you just need to ssh in with the correct flags.

You need to make sure you use either the `-X` or `-Y` (look at `man ssh` for details) flags on all ssh commands you run to establish a connection to the cluster.

For example, connecting from outside of UCL:
```
ssh -X <your_UCL_user_id>@ssh-gateway.ucl.ac.uk
```
and then
```
ssh -X <your_UCL_user_id>@myriad.rc.ucl.ac.uk
```

[A video walkthrough of running remote applications using X11, X-forwarding on compute nodes](https://www.youtube.com/watch?v=nVQlnuo3GSc).

### X-forwarding on macOS

You will need to install XQuartz to provide an X-Window System for macOS. (Previously known as X11.app).

You can then follow the Linux instructions using Terminal.app.

### X-forwarding on Windows

You will need:

* An SSH client; e.g., PuTTY
* An X server program; e.g., Exceed, Xming

Exceed is available on Desktop@UCL machines and downloadable from the [UCL software database](http://swdb.ucl.ac.uk). Xming is open source (and mentioned here without testing).

#### Exceed on Desktop@UCL

1. Load Exceed. You can find it under Start > All Programs > Applications O-P > Open Text Exceed 14 > Exceed
2. Open PuTTY (Applications O-P > PuTTY)
3. In PuTTY, set up the connection with the host machine as usual:
    * Host name: `myriad.rc.ucl.ac.uk` (for example)
    * Port: `22`
    * Connection type: `SSH`
4. Then, from the Category menu, select Connection > SSH > X11 for 'Options controlling SSH X11 forwarding'.
    * Make sure the box marked 'Enable X11 forwarding' is checked.
5. Return to the session menu and save these settings with a new identifiable name for reuse in future.
6. Click 'Open' and login to the host as usual
7. To test that X-forwarding is working, try running `nedit` which is a text editor in our default modules.

If `nedit` works, you have successfully enabled X-forwarding for graphical applications.

#### Installing Xming

Xming is a popular open source X server for Windows. These are instructions for using it alongside PuTTY. Other SSH clients and X servers are available. We cannot verify how well it may be working.

1. Install both PuTTY and Xming if you have not done so already. During Xming installation, choose not to install an SSH client.
2. Open Xming - the Xming icon should appear on the task bar.
3. Open PuTTY
4. Set up PuTTY as shown in the Exceed section.
