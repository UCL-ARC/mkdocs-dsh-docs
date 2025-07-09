# Installing your own software

## Downloading software from Artifactory
You can install software available in Artifactory in your own space. **You can only access Artifactory from inside the DSH.**

To download and install software available in Artifactory, you must log in using your UCL credentials first, in the Artifactory website using DSH Desktop web browser (https://artifactory.idhs.ucl.ac.uk/):
![jFrog login](img/jFrog_login.png)

The main page will show the existent packages. Some of them have been scanned and other do not. For security purposes, only already scanned packages, without vulnerabilities can be installed. 
![jFrog download](img/jFrog_download.png)

If the package you want to install is one of them, then you can proceed to download it by pressing the download icon.
![jFrog packages](img/jFrog_packages.png)

## Downloading and installing packages with R, Conda and Pip.

You can download/install packages using R, Conda and Pip. We encourage our users to create a new virtualenvs for this purpose, where only packages you are installing yourself will be in it.

### Create a virtualenv using Conda.
```
# create the new virtualenv, with any name you want
conda create --name <my-env>
# activate it
conda activate ./<my-env>
```

Your bash prompt will change to show you that a different virtualenv is active.
(This one is called `venv`).

```
(venv) [uccacxx@login03 ~]$ 
```

`deactivate` will deactivate your virtualenv and your prompt will return to normal.

You only need to create the virtualenv the first time. 


## Installing packages.

Then, you can install the packages with:

    - For R: use the command install.packages("MYPACKAGE") in an R console to install MYPACKAGE to your cluster R library
    - For Conda: use the command conda install MYPACKAGE in a terminal to install MYPACKAGE to your current conda environment
    - For Pip: use the command pip install MYPACKAGE in a terminal to install MYPACKAGE to your current python environment

The installation will require the use of a **token** that must be generated using Artifactory. You can use the same token for all package types/configuration files, but this token will **need to be regenerated anytime you change your password**. Tokens should be treated similarly to passwords, in terms of keeping them secret. In DSH cluster you can use <Shift-Insert> to paste in Linux (Ctrl-V won't work!).

You also can create relevant configuration files inside your cluster home directory. In this config files you must copy your token, and paste it into the appropriate place. You must update this token **everytime you change your password**. Here you have some templates for the most common software: 

    - ~/.condarc (for Miniconda)

    
    - ~/.Rprofile (for R and Rstudio)


    - ~/.pip/pip.conf (for Pip)
       ```
       # for Python 2
       pip install --user <python2pkg>
       # for Python 3
       pip3 install --user <python3pkg>
       ```
       These will install into `.python2local ` or `.python3local` in your home directory. 


## Generating an Aryifactory token.

To generate an Artifactory token, visit the Artifactory website using DSH Desktop web browser (https://artifactory.idhs.ucl.ac.uk/), click "Artifacts" in the left panel, and then click "Set Me Up" in the top right.

![jFrog artifacts](img/jFrog_artifacts.png)

![jFrog setmeup](img/jFrog_setmeup.png)

Inside the "Set Me Up" interface, select a package type (doesn't matter which) and generate a personal Artifactory token by typing your password in the text box and clicking "Generate Token & Create Instructions".

![jFrog token](img/jFrog_token.png)

![jFrog token](img/jFrog_token2.png)


Now you can use your token!

## Installing software with no sudo.

You cannot install anything using `sudo`. If the instructions tell you to do that, read further to see if they also have instructions for installing in user space, or for doing an install from source if they are RPMs.

Alternatively, just leave off the `sudo` from the command they tell you to run and look for an alternative way to give it an install location if it tries to install somewhere that isn't in your space (examples for some common build systems are below).

### Automake configure

[Automake](http://www.gnu.org/software/automake/manual/automake.html)
will generate the Makefile for you and hopefully pick up sensible
options through configuration. You can give it an install prefix to tell
it where to install (or you can build it in place and not use make
install at all).

```
./configure --prefix=/hpchome/username/place/you/want/to/install
make
# if it has a test suite, good idea to use it
make test 
make install
```

If it has more configuration flags, you can use `./configure --help` to
view them.

Usually configure will create a config.log: you can look in there to
find if any tests have failed or things you think should have been
picked up haven't.

### CMake

[CMake](http://www.cmake.org/) is another build system. It will have a
CMakeFile or the instructions will ask you to use cmake or ccmake rather
than make. It also generates Makefiles for you. `ccmake` is a
terminal-based interactive interface where you can see what variables
are set to and change them, then repeatedly configure until everything
is correct, generate the Makefile and quit. `cmake` is the commandline
version. The interactive process tends to go like this:

```
ccmake CMakeLists.txt
# press c to configure - will pick up some options
# press t to toggle advanced options
# keep making changes and configuring until no more errors or changes
# press g to generate and exit
make
# if it has a test suite, good idea to use it
make test 
make install
```

The options that you set using ccmake can also be passed on the commandline to
cmake with `-D`. This allows you to script an install and run it again later.
`CMAKE_INSTALL_PREFIX` is how you tell it where to install.

```
# making a build directory allows you to clean it up more easily
mkdir build
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/hpchome/username/place/you/want/to/install
```

If you need to rerun cmake/ccmake and reconfigure, remember to delete the
`CMakeCache.txt` file first or it will still use your old options.
Turning on verbose Makefiles in cmake is also useful if your code
didn't compile first time - you'll be able to see what flags the
compiler or linker is actually being given when it fails.

### Make

Your code may come with a Makefile and have no configure, in which
case the generic way to compile it is as follows:

```
make targetname
```

There's usually a default target, which `make` on its own will use. `make all`
is also frequently used. 
If you need to change any configuration options, you'll need to edit those
sections of the Makefile (usually near the top, where the variables/flags are
defined).

Here are some typical variables you may want to change in a Makefile.

These are what compilers/mpi wrappers to use - these are also defined by
the compiler modules, so you can see what they should be. Intel would be
`icc`, `icpc`, `ifort`, while the GNU compiler would be `gcc`, `g++`, `gfortran`. 
If this is a program that can be compiled using MPI and only has a variable for CC, 
then set that to mpicc.

```
CC=gcc
CXX=g++
FC=gfortran
MPICC=mpicc
MPICXX=mpicxx
MPIF90=mpif90
```

CFLAGS and LDFLAGS are flags for the compiler and linker respectively,
and there might be LIBS or INCLUDE in the Makefile as well. When linking a library 
with the name libfoo, use `-lfoo`.

```
CFLAGS="-I/path/to/include"
LDFLAGS="-L/path/to/foo/lib -L/path/to/bar/lib"
LDLIBS="-lfoo -lbar"
```

Remember to `make clean` first if you are recompiling with new options. This will delete
object files from previous attempts. 

#### Installing via setup.py

If you need to install by downloading a package and using `setup.py`, you can use the `--user` 
flag and as long as one of our python module bundles are loaded, it will install into the same 
`.python2local` or `.python3local` as `pip` does and your packages will be found automatically.
```
python setup.py install --user
```

If you want to install to a different directory in your space to keep this package separate,
you can use `--prefix` instead. You'll need to add that location to your `$PYTHONPATH` and `$PATH`
as well so it can be found. Some install methods won't create the prefix directory you requested
for you automatically, so you would need to create it yourself first.

This type of install makes it easier for you to only have this package in your paths when you
want to use it, which is helpful if it conflicts with something else.
```
# add location to PYTHONPATH so Python can find it
export PYTHONPATH=/hpchome/username/your/path/lib/python3.7/site-packages:$PYTHONPATH
# if necessary, create lib/pythonx.x/site-packages in your desired install location
mkdir -p /hpchome/username/your/path/lib/python3.7/site-packages
# do the install
python setup.py install --prefix=/hpchome/username/your/path
```
It will tend to tell you at install time if you need to change or create the `$PYTHONPATH` directory.

To use this package, you'll need to add it to your paths in your jobscript or `.bashrc`.
Check that the `PATH` is where your Python executables were installed.
```
export PYTHONPATH=/hpchome/username/your/path/lib/python3.7/site-packages:$PYTHONPATH
export PATH=/hpchome/username/your/path/bin:$PATH
```
It is very important that you keep the `:$PYTHONPATH` or `:$PATH` at the end of these - you
are putting your location at the front of the existing contents of the path. If you leave 
them out, then only your package location will be found and nothing else.

#### Troubleshooting: remove your pip cache

If you built something and it went wrong, and are trying to reinstall it with `pip` and keep 
getting errors that you think you should have fixed, you may still be using a previous cached version. 
The cache is in `.cache/pip` in your home directory, and you can delete it.

You can prevent caching entirely by installing using `pip3 install --user --no-cache-dir <python3pkg>`




