# Cluster Computing

## What is a cluster?

In this context, a cluster is a collection of computers (often referred to as "nodes"). 
They're networked together with some shared storage and a scheduling system that lets people 
run programs on them without having to enter commands "live".

The UCL Moodle course "ARC - Introduction to High Performance Computing at UCL" has a video explanation of this here: [(Moodle)](https://moodle.ucl.ac.uk/mod/page/view.php?id=4623810) (UCL users).

This video is also available here: [(mediacentral)](https://mediacentral.ucl.ac.uk/Play/96444) (non-UCL users).

## Why would I want to use one?

Some researchers have programs that require a lot of compute power, like simulating weather patterns or the quantum behaviour of molecules.

Others have a lot of data to process, or need to simulate a lot of things at once, like simulating the spread of disease or assembling parts of DNA into a genome.

Often these kinds of work are either impossible or would take far too long to do on a desktop or laptop computer, as well as making the computer unavailable to do everyday tasks like writing documents or reading papers.

By running the programs on the computers in a cluster, researchers can use many powerful computers at once, without locking up their own one.

## What is the Data Safe Haven high-performance computing (DSH HPC) cluster? 

The DSH HPC is a cluster that is isolated from the university network and the internet for security purposes. These restrictions allow our users to use the cluster to analyse data containing sensitive information in a secure environment. 

## How do I use the DSH HPC cluster?

Most people use something like the following workflow:
  
 - Connect to DSH Desktop through the Applications & Data Portal: <https://accessgateway.idhs.ucl.ac.uk/>
 - Connect to the DSH HPC cluster's "login nodes" using SSH ("ssh client").
 - Copy necessary data to your personal home space in the DSH HPC cluster from your existing DSH share or DSH Desktop environment using WinSCP ("scp client")
   - Note that data can only be copied to the DSH HPC cluster if it is already inside the DSH environment.
     - If the data is outside of the DSH, then it must first be copied into a DSH share using the File Transfer Portal: https://filetransfer.idhs.ucl.ac.uk/webclient/Login.xhtml
     - Also note that only some DSH user accounts have privileges for transferring data into and out of the DSH. Your project's Information Asset Owner (IAA) or Administrator (IAA) can request these privileges for their users as needed.
 - Create a script of commands to run programs
 - Submit the script to the scheduler
 - Wait for the scheduler to find available "compute nodes" and run the script
 - Look at the results in the files the script created

In order to connect to the cluster using SSH, you can use an application such as **GitBash** or **PuTTY** (both of these are available in DSH Desktop by default) to open a terminal where you can enter text commands to interact with the cluster.

If you need to copy data that is already inside the DSH onto the DSH HPC cluster, you can do so using the **SCP** text command, or in a more interactive way using WinSCP (which is available in DSH Desktop by default).

Please be aware that login nodes are shared resources, so users should not be running memory intensive jobs nor jobs with long runtimes in the login node. Doing so may negatively impact the performance of the login node for yourself and the other users. Any user processes that are identified as being disruptive to the normal operation of the login nodes may be killed without warning.
