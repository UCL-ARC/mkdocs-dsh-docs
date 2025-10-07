# Example jobscripts

On this page we describe some basic example scripts to submit jobs to DSH cluster. Our system does not have tmpfs (local hard disk space on the node) and our users will not need to specify a project in their jobscripts.

After creating your script, submit it to the scheduler with:

`qsub my_script.sh`

## Resources

The lines starting with `#$ -l` are where you are requesting resources like wallclock time (how long your job is allowed to run) and memory. In the case for array jobs, each job in the array is treated independently by the scheduler and are each allocated the same resources as are requested. For example, in a job array of 40 jobs requesting for 24 hours wallclock time and 3GB ram, each job in the array will be allocated 24 hours wallclock time and 3GB ram. Wallclock time does not include the time spent waiting in the queue. 
For more information related, please check our documentation: https://github.com/NicoleLabrAvila/mkdocs-dsh/blob/main/mkdocs-project-dir/docs/Running_jobs.md#asking-for-resources

Useful resources:

- [Resource requests (Moodle)](https://moodle.ucl.ac.uk/mod/page/view.php?id=4846681) (UCL users)
- [Resource requests pt.2 (Moodle)](https://moodle.ucl.ac.uk/mod/page/view.php?id=4846689) (UCL users)
- [Resource requests (mediacentral)](https://mediacentral.ucl.ac.uk/Play/98371) (non-UCL users)
- [Resource requests pt.2 (mediacentral)](https://mediacentral.ucl.ac.uk/Play/98393) (non-UCL users)

## Serial Job Script Example

The most basic type of job a user can submit is a serial job. These jobs run on a single processor (core) with a single thread. 

Shown below is a simple job script that runs /bin/date (which prints the current date) on the compute node, and puts the output into a file.

```bash
#!/bin/bash -l

# Batch script to run a serial job under SGE.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set the name of the job.
#$ -N Serial_Job

# Set the working directory to somewhere in your scratch space.  
#  This is a necessary step as compute nodes cannot write to $HOME.
# Replace "<your_UCL_id>" with your UCL user ID.
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/

# Run the application and put the output into a file called date.txt
/bin/date > date.txt
```

## Multi-threaded Job Example

For programs that can use multiple threads, you can request multiple processor cores using the `-pe smp <number>` option. One common method for using multiple threads in a program is OpenMP, and the `$OMP_NUM_THREADS` environment variable is set automatically in a job of this type to tell OpenMP how many threads it should use. Most methods for running multi-threaded applications should correctly detect how many cores have been allocated, though (*via* a mechanism called `cgroups`).

Note that this job script works directly in scratch instead of in the temporary `$TMPDIR` storage.

```bash
#!/bin/bash -l

# Batch script to run an OpenMP threaded job under SGE.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM for each core/thread 
# (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set the name of the job.
#$ -N Multi-threaded_Job

# Request 16 cores.
#$ -pe smp 16

# Set the working directory to somewhere in your scratch space.
# Replace "<your_UCL_id>" with your UCL user ID
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/output

# 8. Run the application.
$HOME/my_program/example
```

## Array Job Script Example

If you want to submit a large number of similar serial jobs then it may be easier to submit them as an array job. Array jobs are similar to serial jobs except we use the `-t` option to get Sun Grid Engine to run 10,000 copies of this job numbered 1 to 10,000. Each job in this array will have the same job ID but a different task ID. The task ID is stored in the `$SGE_TASK_ID` environment variable in each task. All the usual SGE output files have the task ID appended.

```bash
#!/bin/bash -l

# Batch script to run a serial array job under SGE.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set up the job array.  In this instance we have requested 10000 tasks
# numbered 1 to 10000.
#$ -t 1-10000

# Set the name of the job.
#$ -N MyArrayJob

# Set the working directory to somewhere in your scratch space. 
# Replace "<your_UCL_id>" with your UCL user ID :)
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/output

# Run the application.

echo "$JOB_NAME $SGE_TASK_ID"
```

## Array Job Script Example Using Parameter File

Often a user will want to submit a large number of similar jobs but their input parameters don't match easily on to an index from 1 to n. In these cases it's possible to use a parameter file. To use this script a user needs to construct a file with a line for each element in the job array, with parameters separated by spaces.

For example: 

```
0001 1.5 3 aardvark
0002 1.1 13 guppy
0003 1.23 5 elephant
0004 1.112 23 panda
0005 ...
```

Assuming that this file is stored in `~/Scratch/input/params.txt` (you can call this file anything you want) then the user can use awk/sed to get the appropriate variables out of the file. The script below does this and stores them in `$index`, `$variable1`, `$variable2` and `$variable3`.  So for example in task 4, `$index = 0004`, `$variable1 = 1.112`, `$variable2 = 23` and `$variable3 = panda`.

Since the parameter file can be generated automatically from a user's datasets, this approach allows the simple automation, submission and management of thousands or tens of thousands of tasks.

```bash
#!/bin/bash -l

# Batch script to run an array job.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set up the job array.  In this instance we have requested 1000 tasks
# numbered 1 to 1000.
#$ -t 1-1000

# Set the name of the job.
#$ -N array-params

# Set the working directory to somewhere in your scratch space.
# Replace "<your_UCL_id>" with your UCL user ID :)
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/output

# Parse parameter file to get variables.
number=$SGE_TASK_ID
paramfile=/hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/input/params.txt

index="`sed -n ${number}p $paramfile | awk '{print $1}'`"
variable1="`sed -n ${number}p $paramfile | awk '{print $2}'`"
variable2="`sed -n ${number}p $paramfile | awk '{print $3}'`"
variable3="`sed -n ${number}p $paramfile | awk '{print $4}'`"

# Run the program (replace echo with your binary and options).

echo "$index" "$variable1" "$variable2" "$variable3"
```

## Array Job Script with a Stride

If each task for your array job is very small, you will get better use of the cluster if you can combine a number of these so each has a couple of hours' worth of work to do. There is a startup cost associated with the amount of time it takes to set up a new job. If your job's runtime is very small, this cost is proportionately high, and you incur it with every array task.

Using a stride will allow you to leave your input files numbered as before, and each array task will run N inputs.

For example, a stride of 10 will give you these task IDs: 1, 11, 21...

Your script can then have a loop that runs task IDs from `$SGE_TASK_ID` to `$SGE_TASK_ID + 9`, so each task is doing ten times as many runs as it was before.

```bash
#!/bin/bash -l

# Batch script to run an array job with strided task IDs under SGE.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set up the job array.  In this instance we have requested task IDs
# numbered 1 to 10000 with a stride of 10.
#$ -t 1-10000:10

# Set the name of the job.
#$ -N arraystride

# Set the working directory to somewhere in your scratch space.
# Replace "<your_UCL_id>" with your UCL user ID :)
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/output

# Loop through the IDs covered by this stride and run the application if 
# the input file exists. (This is because the last stride may not have that
# many inputs available). Or you can leave out the check and get an error.
for (( i=$SGE_TASK_ID; i<$SGE_TASK_ID+10; i++ ))
do
  if [ -f "input.$i" ]
  then
    echo "$JOB_NAME" "$SGE_TASK_ID" "input.$i"
  fi
done
```

## GPU Job Script Example

To use NVIDIA GPUs with the CUDA libraries, you need to load the CUDA runtime libraries module or else set up the environment yourself. The script below shows what you'll need to unload and load the appropriate modules.

You also need to use the `-l gpu=<number>` option to request the GPUs from the scheduler.

```bash
#!/bin/bash -l

# Batch script to run a GPU job under SGE.

# Request a number of GPU cards, in this case 2 (the maximum)
#$ -l gpu=2

# Request ten minutes of wallclock time (format hours:minutes:seconds).
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM (must be an integer followed by M, G, or T)
#$ -l mem=1G

# Set the name of the job.
#$ -N GPUJob

# Set the working directory to somewhere in your scratch space.
# Replace "<your_UCL_id>" with your UCL user ID :)
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/output

# Run the application - the line below is just a random example.
mygpucode
```

## Example with R

Current R version available is 4.4.0. R can be run on a single core or multithreaded using many cores.
This script runs R using only one core.

```
#!/bin/bash -l

# Example jobscript to run a single core R job

# Request ten minutes of wallclock time (format hours:minutes:seconds).
# Change this to suit your requirements.
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM. Change this to suit your requirements.
#$ -l mem=1G

# Set the name of the job. You can change this if you wish.
#$ -N R_job_1

# Set the working directory to somewhere in your scratch space.  This is
# necessary because the compute nodes cannot write to your $HOME
# NOTE: this directory must exist.
# Replace "<your_UCL_id>" with your UCL user ID
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/R_output

# Run your R program
R --no-save < /home/username/Scratch/myR_job.R > myR_job.out
```

You will need to change the `-wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/R_output` location and the location of your R input file, called `myR_job.R` here.  `myR_job.out` is the file we are redirecting the output into.

If your jobscript is called `run-R.sh` then your job submission command would be:
```
qsub run-R.sh
``` 

## Example shared memory threaded parallel job

This script uses multiple cores on the same node. It cannot run across multiple nodes.

```
#!/bin/bash -l

# Example jobscript to run an OpenMP threaded R job across multiple cores on one node.
# This may be using the foreach packages foreach(...) %dopar% for example.

# Request ten minutes of wallclock time (format hours:minutes:seconds).
# Change this to suit your requirements.
#$ -l h_rt=0:10:0

# Request 1 gigabyte of RAM per core. Change this to suit your requirements.
#$ -l mem=1G

# Set the name of the job. You can change this if you wish.
#$ -N R_jobMC_2

# Select 12 threads. The number of threads here must equal the number of worker 
# processes in the registerDoMC call in your R program.
#$ -pe smp 12

# Set the working directory to somewhere in your scratch space.  This is
# necessary because the compute nodes cannot write to your $HOME
# NOTE: this directory must exist.
# Replace "<your_UCL_id>" with your UCL user ID
#$ -wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/R_output

# Run your R program
R --no-save < /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/myR_job.R > myR_job.out
```

You will need to change the `-wd /hpchome/<your_UCL_id>.IDHS.UCL.AC.UK/R_output` location and the location of your R input file, called `myR_job.R` here.  `myR_job.out` is the file we are redirecting the output into.

If your jobscript is called `run-R.sh` then your job submission command would be:
```
qsub run-R.sh
``` 







