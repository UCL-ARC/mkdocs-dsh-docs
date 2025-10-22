# Machine Learning workflows

For many ML workflows, we use conda environments to simplify setup and reproducibility (link to conda page).
Where possible, for each new project we recommend building a new environment from scratch, then gradually adding functionality to it as you scale up your testing (i.e. start with making an environment that can see and use gpu, then add ML libraries and test, and finally start debugging your ML code). In the DSH, GPU libraries like CUDA are pre-installed and accessible for all users (i.e., we don't need to load their software modules), so all we have to do is install software that utilises these GPU's libraries. 

For reference, the commands below can be used to create a conda environment that provides pytorch with cuda capability:

First we'll create a new conda environment called `gpu-env`, install `python` and `pip` in it, and activate:
```
conda create --name gpu-env python=3.10 pip
conda activate gpu-env
```
*(If you have not used conda before, it may get you to run `conda init` once at the start, which is expected — you'll then need to restart the shell for changes to take effect)*
Once the new gpu-env is activated you should see your command line start with `(gpu-env) username@hostname`, which tells you it's working as expected.

Next we'll use `pip` to install torch and other libraries (though you could be using `conda install` instead).
```
pip install torch pandas numpy
```
Once the new `gpu-env` has torch installed, you can create a new test script with `nano ~/<yourfolder>/test.py`, and then add the following lines:

> **test.py**
> ```
> import torch
> import pandas as pd
> import numpy as np
> 
> print(f"Torch version: {torch.__version__}")
> print(f"Torch cuda is available: {torch.cuda.is_available()}")
> print(f"Torch cuda device count: {torch.cuda.device_count()}")
> 
> x = torch.rand(5, 3)
> print(x)

To run your script as a test job:
- create an example script (e.g. `nano gpu-test-run.sh`)
- add the lines show below (making sure to revise `<yourusername>` and paths to `<yourfolder>` with python script)
- Once saved, submit it with `qsub gpu-test-run.sh`

> **gpu-test-run.sh**
> ```
> #!/bin/bash -l
> 
> # job name
> #$ -N gpu-test-run
> 
> # set RAM (increase after testing)
> #$ -l h_vmem=16G
> 
> # request 1 GPU
> #$ -l gpu=1
> 
> # Request ten minutes compute time (h:m:s)
> #$ -l h_rt=0:10:0
> 
> # Set the working directory to where you saved your test.py script
> #$ -wd /hpchome/<yourusername>.IDHS.UCL.AC.UK/<yourfolder>
> 
> # activate the conda gpu environment
> conda activate gpu-env
> 
> # run the test script
> python test.py

Lastly, it's also worth mentioning that you can do a lot of testing/debugging with interactive jobs, which you can request on a gpu node with `qlogin -l gpu`. This interactive job should let you run sanity checks like `nvidia-smi`, which gives you gpu card info if one is available, and test basic functionality of your gpu-env environment before you run jobs with it.
