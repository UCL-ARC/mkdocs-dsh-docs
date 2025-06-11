# DSH Cluster

DSH is designed for single-node jobs, it is not possible to run multi-node parallel jobs. It is also not connected to internet and it is not connected to the UCL network. 

## Accounts
DSH accounts can be applied for via the [DSH sign up process](../Account_Services.md).

## Logging in

You *must* log in to the cluster from inside DSH Desktop. The connection to the cluster is done by SSH connection. DSH Desktop has **PuTTY** and **Gitbash** installed for this purpose. 
To connect to the cluster using **Gitbash**, open a terminal and type the below command to secure shell (ssh) into the machine you wish to access. Replace <my_UCL_user> with your internal UCL user and <system_name> with the name of the machine you want to log in to, eg. dsh-sge2log01:

```
ssh <my_UCL_user>@<system_name>  
```

Your password will be requested. Enter it and press **Enter key** 

*The prompt will not show your password when you are typing it. This is expected and it is for security reasons. Be careful entering your password*

The first time you log in to an unknown server you will get a message like this:

    The authenticity of host 'IDSH.rc.ucl.ac.uk can't be established.
    ECDSA key fingerprint is SHA256:7FTryal3mIhWr9CqM3EPPeXsfezNk8Mm8HPCCAGXiIA.
    Are you sure you want to continue connecting (yes/no)?

Typing **yes** will allow you to continue logging in.

If you have a personal virtual machine in the cluster put the name of your machine in <my_UCL_user>.
Idle ssh sessions will be disconnected after 7 days.

PuTTY is a common SSH client on Windows and is available on DSH Desktop. If you prefer to use it, you will need to create an entry for the host you are connecting to with the settings below. If you want to save your settings, give them an easily-identifiable name in the "Saved Sessions" box and press "Save". Then you can select it and "Load" next time you use PuTTY.

![PuTTY screenshot](img/PuTTY.png)

You will then be asked to enter your username and password. Only enter your username, not @<my_UCL_user>.rc.ucl.ac.uk. The password field will remain entirely blank when you type in to it - it does not show placeholders to indicate you have typed something.

The first time you log in to a new server, you'll get a popup telling you that the server's host key is not cached in the registry - this is normal and is because you have never connected to this server before. If you want to, you can check the host fingerprint against our current key fingerprints.

### Login nodes

DSH cluster has 2 login nodes, dsh-sge2log01 and  dsh-sge2log02 and you can connect to any. The login nodes allow you to manage your files, compile code and submit jobs. Very short (< 15 mins) and non-resource-intensive software tests can be run on the login nodes, but anything more should be submitted as a job.

### Logging in to a specific node

You can access any of both, dsh-sge2log01 and dsh-sge2log02 login nodes with: 

```
ssh <my_UCL_user>@dsh-sge2log01
ssh <my_UCL_user>@dsh-sge2log02
```

### Login problems

If you experience difficulties with your login, please make sure that you are typing your UCL user ID and your password correctly. If you have recently updated your password, it takes some hours to propagate to all UCL systems.

If you still cannot get access but can access DSH desktop, please contact us on rc-support@ucl.ac.uk indicating you are working in the DSH Cluster.
If you cannot access anything in DSH, you may need to request a password reset for the DSH service from the Service Desk. Please, contact our support team - [Data Safe Haven - General DSH Enquiry](https://myservices.ucl.ac.uk/self-service/requests/new/provide_description?from=wizard&requested_for_id=187535&requestor_id=187535&service_id=1473&service_instance_id=3892&subject=Data+Safe+Haven+-+General+DSH+Enquiry%3A&template_id=3222)


## Copying data onto DSH Cluster

If you need to copy data into the cluster, you can only do it if the data is already in the DSH desktop.
If the data is outside DSH it *must* be copied into the DSH desktop thorough the file transfer portal: https://filetransfer.idhs.ucl.ac.uk/webclient/Login.xhtml

If you need to copy data already in the DSH desktop to the cluster you can do it using Secure Copy (SCP) protocol. The following template will copy a data file (preferably a single compressed file) from somewhere on your DSH machine to a specified location on the remote machine inside the DSH cluster (login node, etc) using the **SCP** command:

```
scp <local_data_file_path> <my_UCL_user>@<system_name>:<remote_path>
```

If you need to tranfer a folder with several files and directories inside, then use scp with the recursive option:

```
scp -r <local_data_file_path> <my_UCL_user>@<system_name>:<remote_path>
```

If you prefer to use a graphical interface, then you can use **WinSCP** or **Filezilla** that are already inside DSH.

## Transferring data with WinSCP








## Transferring data with Filezilla












## Data storage

Our clusters have local parallel filesystems consisting of your home where you can write data. They may also have local storage on the compute node that can be used during your job.

Home

Every user has a home directory. This is the directory you are in when you first log in.

    Location: /home/<username>
    May also be referred to as: ~, $HOME.

Many programs will write hidden config files in here, with names beginning with . (eg .config, .cache). You can see these with ls -al.

## Tips for use

- Use different directories for different jobs. Do not write everything to the same place.
- Clear up your work directory after your jobs. Keep the files you need, archive or delete the ones you do not.
- Archive and compress directory trees you aren't currently using. (`tar` command for example). This
  stores all their contents as one file, and compressing it saves space.
- Back up your important data to somewhere off the cluster regularly.
- If you haven't used particular files for some months and do not expect to in the near future, keep
  them off-cluster and delete the copies on the cluster.
- If you are no longer using the cluster, remove your data to maintain filesystem performance and allow
  the space to be used by current active users.
- Before you leave UCL, please consider what should happen to your data, and take steps to put it in
  a Research Data archive and/or ensure that your colleagues are given access to it.

  
## Quotas

The default quota on DSH are 15B for home, backed up, no increases available

These is a soft quotas: once you reach them, you will still be able
to write more data but try to Keep an eye on them in consideration to other users.

You cannot apply for quota increases.

Here are some tips for [managing your quota](../howto.md#managing-your-quota) and
finding where space is being used.

## Job sizes

| Cores   | Max wallclock   |
| ------- | --------------- |
| 1 to 40 | 48hrs suggested |

[Interactive jobs](../Interactive_Jobs.md) run with `qrsh` have the same
maximum wallclock time as other jobs.

## Node types


We can only do single-node jobs, they are simply higher spec than the DSH Desktop virtual machines -- I believe the DSH Desktop machines are 4 core, 32 GB ram, whereas our HPC nodes are 16 core, 128 GB RAM (and two nodes have 80 GB A100 GPUs).


Kathleen's compute capability comprises 192 diskless compute nodes each with two 20-core Intel Xeon Gold 6248 2.5GHz processors, 192 gigabytes of 2933MHz DDR4 RAM, and an Intel OmniPath network.

Two nodes identical to these, but with two 1 terabyte hard-disk drives added, serve as the login nodes.


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

# Acknowledging the Use of DSH Systems

To keep running our services, we depend on being able to demonstrate that
they are used in published research.

When preparing papers describing work that has used the DSH services, please use the terms below.

"The authors acknowledge the use of the Data Save Haven (DSH), and associated support services, in the
completion of this work."

# Acknowledging the Use of DSH Systems

To keep running our services, we depend on being able to demonstrate that
they are used in published research.

When preparing papers describing work that has used the DSH services, please use the terms below.

"The authors acknowledge the use of the Data Save Haven (DSH), and associated support services, in the
completion of this work."

