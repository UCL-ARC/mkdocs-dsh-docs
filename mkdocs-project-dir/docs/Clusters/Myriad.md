---
title: DSH cluster
layout: cluster
---
DSH is designed for high I/O, high throughput jobs that will run within a single node rather than multi-node parallel jobs.
Also, allows extensively parallel, multi-node batch-processing jobs, having high-bandwidth connections between each individual node.

## Accounts
DSH accounts can be applied for via the [Research Computing sign up process](../Account_Services.md).

## Logging in

You will use your UCL username and password to log in into the DSH portal.




```
ssh uccaxxx@myriad.rc.ucl.ac.uk
```

If you are outside the UCL firewall you will need to follow the
instructions for [Logging in from outside the UCL firewall](../howto.md#logging-in-from-outside-the-ucl-firewall).

Idle ssh sessions will be disconnected after 7 days.

### Login nodes
The login nodes allow you to manage your files, compile code and submit jobs. Very short (< 15 mins) and non-resource-intensive software tests can be run on the login nodes, but anything more should be submitted as a job.

### Logging in to a specific node

You can access a specific Myriad login node with: 

```
ssh uccaxxx@login12.myriad.rc.ucl.ac.uk
ssh uccaxxx@login13.myriad.rc.ucl.ac.uk
```

The main address will redirect you on to either one of them.

Using the system
Young is a batch system. The login nodes allow you to manage your files, compile code and submit jobs. Very short (<15mins) and non-resource-intensive software tests can be run on the login nodes, but anything more should be submitted as a job.

## Copying data onto DSH

You will need to use the DSH portal. Please refer to the page on [How do I transfer data onto the system?](../howto.md#how-do-i-transfer-data-onto-the-system)

## Quotas

The default quota on DSH are 15B for home, backed up, no increases available

These is a soft quotas: once you reach them, you will still be able
to write more data but try to Keep an eye on them in consideration to other users.

You cannot apply for quota increases.

Here are some tips for [managing your quota](../howto.md#managing-your-quota) and
finding where space is being used.

## Job sizes

| Cores   | Max wallclock |
| ------- | ------------- |
| 1       | 72hrs         |
| 2 to 36 | 48hrs         |

[Interactive jobs](../Interactive_Jobs.md) run with `qrsh` have the same
maximum wallclock time as other jobs.

## Node types

DSH contains three main node types: standard compute nodes, high memory
nodes and GPU nodes. As new nodes as added over time with slightly newer processor
variants, new letters are added.

| Type  | Cores per node   | RAM per node | tmpfs | Nodes |
| ----- | ---------------- | ------------ | ----- | ----- |
| H,D   | 36               | 192GB        | 1500G | 342   |
| I,B   | 36               | 1.5TB        | 1500G | 17    |
| J     | 36 + 2 P100 GPUs | 192GB        | 1500G | 2     |
| E,F   | 36 + 2 V100 GPUs | 192GB        | 1500G | 19    |
| L     | 36 + 4 A100 GPUs | 192GB        | 1500G | 6     |

You can tell the type of a node by its name: type H nodes are named
`node-h00a-001` etc.

Here are the processors each node type has:

  - F, H, I, J: Intel(R) Xeon(R) Gold 6140 CPU @ 2.30GHz
  - B, D, E, L: Intel(R) Xeon(R) Gold 6240 CPU @ 2.60GHz

(If you ever need to check this, you can include `cat /proc/cpuinfo` in your jobscript so
you get it in your job's .o file for the exact node your job ran on. You will get an entry
for every core).

## GPUs

Myriad has four types of GPU nodes: E, F, J and L. 

  - L-type nodes each have four NVIDIA 40G A100s. (Compute Capability 80)
  - F-type and E-type nodes each have two NVIDIA Tesla V100s. The CPUs are slightly different on the different letters, see above. (Compute Capability 70)
  - J-type nodes each have two NVIDIA Tesla P100s. (Compute Capability 60)

You can include `nvidia-smi` in your jobscript to get information about the GPU your job ran on.

### Compute Capability

[Compute Capability](https://docs.nvidia.com/cuda/cuda-compiler-driver-nvcc/index.html#gpu-generations) is how NVIDIA categorises its generations of GPU architectures. 
When code is compiled, it targets one or multiple of these and so it may only be able 
to run on GPUs of a specific Compute Capability.

If you get an error like this:

```
CUDA runtime implicit initialization on GPU:0 failed. Status: device kernel image is invalid
```
then the software you are running does not support the Compute Capability of the GPU
you tried to run it on, and you probably need a newer version.

### Requesting multiple and specific types of GPU

You can request a number of GPUs by adding them as a resource request to your jobscript: 

```
# For 1 GPU
#$ -l gpu=1

# For 2 GPUs
#$ -l gpu=2

# For 4 GPUs
#$ -l gpu=4
```

If you ask for one or two GPUs your job can run on any type of GPU since it can fit on
any of the nodetypes. If you ask for four, it can only be a node that has four. 
If you need to specify one node type over the others because you need a particular 
Compute Capability, add a request for that type of node to your jobscript:

```
# request a V100 node only
#$ -ac allow=EF

# request an A100 node only
#$ -ac allow=L
```

The [GPU nodes](../Supplementary/GPU_Nodes.md) page has some sample code for running GPU jobs if you need a test example.

### Submitting a job
Create a jobscript for non-interactive use and submit your jobscript using qsub. Jobscripts must begin #!/bin/bash -l in order to run as a login shell and get your login environment and modules.

### Memory requests

Note: the memory you request is always per core, not the total amount. If you ask for 192GB RAM and 40 cores, that may run on 40 nodes using only one core per node. This allows you to have sparse process placement when you do actually need that much RAM per process.

Young also has high memory nodes, where a job like this may run.

If you want to avoid sparse process placement and your job taking up more nodes than you were expecting, the maximum memory request you can make when using all the cores in a standard node is 4.6G.

### Requesting software installs

To request software installs, email us at the [support address below](#support) or open an issue on our
[GitHub](https://github.com/UCL-ARC/rcps-buildscripts/issues). You can
see what software has already been requested in the Github issues and
can add a comment if you're also interested in something already
requested.


### Installing your own software

You may install software in your own space. Please look at
[Compiling Your Code](../Supplementary/Compiling_Your_Code.md) for tips.


## Suggested job sizes

The target job sizes for Young are 2-5 nodes. Jobs
larger than this may have a longer queue time and are better suited to
ARCHER, and single node jobs may be more suited to your local
facilities.

## Maximum job resources

| Job type                  | Cores | GPUs | Max wallclock |
| ------------------------- | ----- | ---- | ------------- |
| Gold CPU job, any         | 5120  | 0    | 48hrs         |
| Free CPU job, any         | 5120  | 0    | 24hrs         |
| Free GPU job, any         | 320   | 40   | 48hrs         |
| Free GPU fast interactive | 64    | 8    | 6hrs          |
| HBM CPU job, any          | 2048  | 0    | 48hrs         |

CPU jobs or [GPU jobs](#gpu-nodes) can be run on Young, and there are 
different [nodes](#node-types) dedicated for each.

These are numbers of physical cores: multiply by two for virtual cores 
with [hyperthreads](#hyperthreading) on the CPU nodes.

On Young, interactive sessions using qrsh have the same wallclock limit
as other jobs.

CPU jobs on Young **do not share nodes**, whereas GPU jobs do. 
This means that if you request less than 40 cores for a CPU job, 
your job is still taking up an entire node and no
other jobs can run on it, but some of the cores are idle. Whenever
possible, request a number of cores that is a multiple of 40 for full
usage of your CPU nodes.

There is a superqueue for use in exceptional circumstances that will
allow access to a larger number of cores outside the nonblocking
interconnect zones, going across the interconnect between blocks. A
third of each CU is accessible this way, roughly approximating a 1:1
connection. Access to the superqueue for larger jobs must be applied
for: contact the support address below for details.

Some normal multi-node jobs will use the superqueue - this is to make it
easier for larger jobs to be scheduled, as otherwise they can have very
long waits if every CU is half full.


### Preventing a job from running cross-CU

If your job must run within a single CU, you can request the parallel environment as `-pe wss` instead of `-pe mpi` (`wss` standing for 'wants single switch'). This will increase your queue times. It is suggested you only do this for benchmarking or if performance is being greatly affected by running in the superqueue.


## Node types

Young has five types of node: standard nodes, big memory nodes, really big memory nodes, 
GPU nodes and HBM nodes. Note those last three have different processors and number of 
CPU cores per node.

| Type  | Cores per node | RAM per node | tmpfs | Nodes | Memory request necessary | GPU |
| ----- | -------------- | ------------ | ----- | ----- | ------------------------ | --- |
| C     | 40             | 192G (188G usable) | None  | 576   | Any | None |
| Y     | 40             | 1.5T         | None  | 3     | mpi: mem >=19G, smp: >186G total | None |
| Z     | 36             | 3.0T         | None  | 3     | mpi: mem >=42G, smp: >1530G total | None |
| X     | 64             | 1T           | 200G  | 6     | Any | 8 x Nvidia 40G A100 |
| W     | 64             | 503G usable | 3.5T  | 32    | Any | None |

These are numbers of physical cores: multiply by two for virtual cores with
hyperthreading. 

The 'memory request necessary' column shows what memory requests a job needs to 
make to be eligible for that node type. For MPI jobs it looks at the memory per 
slot requested. For SMP jobs they will go on the node that their total memory 
request (slots * mem) fits on.

Here are the processors each node type has:

  - C: Intel(R) Xeon(R) Gold 6248 CPU @ 2.50GHz 
  - Y: Intel(R) Xeon(R) Gold 6248 CPU @ 2.50GHz
  - Z: Intel(R) Xeon(R) Gold 6240M CPU @ 2.60GHz
  - X: dual AMD EPYC 7543 32-Core Processor
  - W: Intel (R) Xeon(R) CPU Max 9462

(If you ever need to check this, you can include `cat /proc/cpuinfo` in your jobscript so 
you get it in your job's .o file for the exact node your job ran on. You will get an entry
for every core).

## GPU nodes

Now available for general use, for Free jobs only. There will be separate GPU Gold budgets in 
future.

[How to use the GPU nodes](../Supplementary/Young_GPU_Nodes.md).


## High Bandwidth Memory nodes

The HBM nodes have 64GB of integrated High Bandwidth Memory per socket and two sockets per node.

HBM nodes can be set on the system level in two modes. 

* HBM cache mode: In cache mode, HBM functions as a memory-side cache for contents of DDR memory. 
  In this mode, HBM is transparent to all software because the HBM cache is managed by hardware 
  memory controllers. No code changes are required.

* HBM flat mode: In flat mode, both DDR and the HBM address spaces are visible to software. 
  Applications may need to be modified or tuned to be aware of the additional memory hierarchy.

At present, we have the nodes set in cache mode. We will be re-evaluating this after the 
operating system is upgraded and will have full support for flat mode - at this point we 
may have some nodes in each mode to allow you to experiment.

There are more details about HBM and the modes at [Enabling High Bandwidth Memory for HPC and AI Applications for Next Gen Intel Xeon Processors](https://community.intel.com/t5/Blogs/Products-and-Solutions/HPC/Enabling-High-Bandwidth-Memory-for-HPC-and-AI-Applications-for/post/1335100)

### Requesting HBM nodes

You need to request these nodes explicitly in your job.

```
# Request HBM nodes
#$ -ac allow=W
```


## Restricting to one node type

The scheduler will schedule your job on the relevant nodetype 
based on the resources you request, but if you really need to specify 
the nodetype yourself, use:

```
# Only run on Z-type nodes
#$ -ac allow=Z
```

## Hyperthreading

Young has hyperthreading enabled and you can choose on a per-job basis 
whether you want to use it.

Hyperthreading lets you use two virtual cores instead of one physical 
core - some programs can take advantage of this.

If you do not ask for hyperthreading, your job only uses one thread per core as normal.

The `-l threads=` request is not a true/false setting, instead you are telling the scheduler
you want one slot to block one virtual cpu instead of the normal situation where it blocks two.
If you have a script with a threads request and want to override it on the command line or set
it back to normal, the usual case is `-l threads=2`. (Setting threads to 0 does not disable
hyperthreading!)

```
# request hyperthreading in this job
#$ -l threads=1

# request the number of virtual cores
#$ -pe mpi 160

# request 2G RAM per virtual core
#$ -l mem=2G

# set number of OpenMP threads being used per MPI process
export OMP_NUM_THREADS=2
```

This job would be using 80 physical cores, using 80 MPI processes each of 
which would create two threads (on Hyperthreads).

Note that memory requests are now per virtual core with hyperthreading enabled. 
If you asked for `#$ -l mem=4G`on a node with 80 virtual cores and 192G RAM then 
you are requiring 320G RAM in total which will not fit on that node and so you 
would be given a sparse process layout across more nodes to meet this requirement.

```
# request hyperthreading in this job
#$ -l threads=1

# request the number of virtual cores
#$ -pe mpi 160

# request 2G RAM per virtual core
#$ -l mem=2G

# set number of OpenMP threads being used per MPI process
# (a whole node's worth)
export OMP_NUM_THREADS=80
```

This job would still be using 80 physical cores, but would use one MPI 
process per node which would create 80 threads on the node (on Hyperthreads).


The A-type nodes have hyperthreading enabled and you can choose on a per-job basis whether you want to use it.

Hyperthreading lets you use two virtual cores instead of one physical core - some programs can take advantage of this.

If you do not ask for hyperthreading, your job only uses one thread per core as normal.

The -l threads= request is not a true/false setting, instead you are telling the scheduler you want one slot to block one virtual cpu instead of the normal situation where it blocks two. If you have a script with a threads request and want to override it on the command line or set it back to normal, the usual case is -l threads=2. (Setting threads to 0 does not disable hyperthreading!)

```
# request hyperthreading in this job
#$ -l threads=1

# request the number of virtual cores
#$ -pe mpi 160

# request 2G RAM per virtual core
#$ -l mem=2G

# set number of OpenMP threads being used per MPI process
export OMP_NUM_THREADS=2
```

This job would be using 80 physical cores, using 80 MPI processes each of which would create two threads (on Hyperthreads).

Note that memory requests are now per virtual core with hyperthreading enabled. If you asked for #$ -l mem=4Gon a node with 80 virtual cores and 192G RAM then you are requiring 320G RAM in total which will not fit on that node and so you would be given a sparse process layout across more nodes to meet this requirement.
```
# request hyperthreading in this job
#$ -l threads=1

# request the number of virtual cores
#$ -pe mpi 160

# request 2G RAM per virtual core
#$ -l mem=2G

# set number of OpenMP threads being used per MPI process
# (a whole node's worth)
export OMP_NUM_THREADS=80
```
This job would still be using 80 physical cores, but would use one MPI process per node which would create 80 threads on the node (on Hyperthreads).

### Job deletion

If you `qdel` a submitted Gold job, the reserved Gold will be made
available again. This is done by a cron job that runs every 15 minutes,
so you may not see it back instantly.

## Support

Email <rc-support@ucl.ac.uk> with any support queries. It will be helpful
to include Young in the subject along with some descriptive text about
the type of problem, and you should mention your username in the body.

## Acknowledging the use of DSH in publications

All work arising from this facility should be properly acknowledged in
presentations and papers with the following text:

"We are grateful to the UK Materials and Molecular Modelling Hub for
computational resources, which is partially funded by EPSRC
(EP/T022213/1, EP/W032260/1 and EP/P020194/1)"


