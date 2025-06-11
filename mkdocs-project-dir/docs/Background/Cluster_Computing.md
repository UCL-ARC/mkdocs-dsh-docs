# Cluster Computing

## What is a cluster?

In this context, a cluster is a collection of computers (often referred to as "nodes"). 
They're networked together with some shared storage and a scheduling system that lets people 
run programs on them without having to enter commands "live".

The UCL Moodle course "ARC - Introduction to High Performance Computing at UCL" has a video explanation of this here: [(Moodle)](https://moodle.ucl.ac.uk/mod/page/view.php?id=4623810) (UCL users)

This video is also available here: [(mediacentral)](https://mediacentral.ucl.ac.uk/Play/96444) (non-UCL users)

## Why would I want to use one?

Some researchers have programs that require a lot of compute power, like simulating weather patterns or the quantum behaviour of molecules.

Others have a lot of data to process, or need to simulate a lot of things at once, like simulating the spread of disease or assembling parts of DNA into a genome.

Often these kinds of work are either impossible or would take far too long to do on a desktop or laptop computer, as well as making the computer unavailable to do everyday tasks like writing documents or reading papers.

By running the programs on the computers in a cluster, researchers can use many powerful computers at once, without locking up their own one.

## What is Data Save Haven (DSH) cluster? 

It is a cluster that is isolated from the university network for security purposes. It also doesn't have any connection to internet. This restrictions allow our users to use the cluster to analyse data containing sensitive information in a secure environment. 

## How do I use a cluster in DSH?

Most people use something like the following workflow:
  
 - Connect to the DSH desktop through the data portal : https://accessgateway.idhs.ucl.ac.uk/vpn/index.html
 - Connect to the cluster's "login nodes" using ssh ("ssh client").
 - If you need to copy data into the cluster, you can only do it if the data is already in the DSH desktop.
     - If the data is outside DSH it must be copied into the DSH desktop thorough the file transfer portal: https://filetransfer.idhs.ucl.ac.uk/webclient/Login.xhtml
 - Create a script of commands to run programs
 - Submit the script to the scheduler
 - Wait for the scheduler to find available "compute nodes" and run the script
 - Look at the results in the files the script created

In order to connect to the cluster using ssh, you can use both **Gitbash** or **PuTTY**. Both programs are already installed in DSH desktop. Both of them will open a terminal where you can enter text commands to intercat with the cluster.

If you need to copu data already in the DSH desktop to the cluster you can do it using **SCP** command or in a more interactive way using FileZilla, that is already inside DSH.

Please be aware that login nodes are shared resources, so users should not be running memory intensive jobs nor jobs with long runtimes in the login node. Doing so may negatively impact the performance of the login node for other users. Hence, identified culprit user processes are systematically killed.
