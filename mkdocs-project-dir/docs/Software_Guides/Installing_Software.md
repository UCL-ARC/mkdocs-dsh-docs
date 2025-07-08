## Installing software

If you want to request that software be installed centrally, you can email us at 
rc-support@ucl.ac.uk. When you send in a request please address the following questions so 
that the install can be properly prioitised and planned,

* Can you provide some details as to why and give an idea of the timeline you would like us 
to build it in?
* Do you have an idea of the user base for this software within your community?
* If the software is only required by you would you be open to trying to install the software in 
your home space? We can provide some assistance here if you tell us what problems you are
encountering.

You can install software yourself in your space on the cluster. Below are some tips for 
installing packages for languages such as Python or R as well as compiling software.

### No sudo!

You cannot install anything using `sudo` (and neither can we!). If the instructions tell you to do that, read further to see if they also have instructions for installing in user space, or for doing an install from source if they are RPMs.

Alternatively, just leave off the `sudo` from the command they tell you to run and look for an alternative way to give it an install location if it tries to install somewhere that isn't in your space (examples for some common build systems are below).

### Download source code





### Automake configure

[Automake](http://www.gnu.org/software/automake/manual/automake.html)
will generate the Makefile for you and hopefully pick up sensible
options through configuration. You can give it an install prefix to tell
it where to install (or you can build it in place and not use make
install at all).

```
./configure --prefix=/home/username/place/you/want/to/install
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
cmake .. -DCMAKE_INSTALL_PREFIX=/home/username/place/you/want/to/install
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

## Installing additional packages for an existing scripting language

### Python

 These use a virtualenv, have a lot of Python packages installed already, 
like numpy and scipy (see [the Python package list](../Installed_Software_Lists/python-packages.md)) 
and have `pip` set up for you.

#### Install your own packages in the same virtualenv

This will use our central virtualenv and the packages we have already installed.

```
# for Python 2
pip install --user <python2pkg>
# for Python 3
pip3 install --user <python3pkg>
```
These will install into `.python2local` or `.python3local` in your home directory. 

If your own installed Python packages get into a mess, you can delete (or rename) the whole 
`.python3local` and start again.

#### Using your own virtualenv

If you need different packages that are not compatible with the centrally installed versions (eg. 
what you are trying to install depends on a different version of something we have already installed)
then you can create a new virtualenv and only packages you are installing yourself will be in it.

In this case, you do not want our virtualenv with our packages to also be active.
We have two types of Python modules. If you type `module avail python` there are 
"bundles" which are named like `python3/3.7` - these include our virtualenv and
packages. Then there are the base modules for just python itself, like `python/3.7.4`. 

When using your own virtualenv, you want to load one of the base python modules.

```
# load a base python module (you will always need to do this)
module load python/3.7.4
# create the new virtualenv, with any name you want
virtualenv <DIR>
# activate it
source <DIR>/bin/activate
```
Your bash prompt will change to show you that a different virtualenv is active.
(This one is called `venv`).
```
(venv) [uccacxx@login03 ~]$ 
```

`deactivate` will deactivate your virtualenv and your prompt will return to normal.

You only need to create the virtualenv the first time. 

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
export PYTHONPATH=/home/username/your/path/lib/python3.7/site-packages:$PYTHONPATH
# if necessary, create lib/pythonx.x/site-packages in your desired install location
mkdir -p /home/username/your/path/lib/python3.7/site-packages
# do the install
python setup.py install --prefix=/home/username/your/path
```
It will tend to tell you at install time if you need to change or create the `$PYTHONPATH` directory.

To use this package, you'll need to add it to your paths in your jobscript or `.bashrc`.
Check that the `PATH` is where your Python executables were installed.
```
export PYTHONPATH=/home/username/your/path/lib/python3.7/site-packages:$PYTHONPATH
export PATH=/home/username/your/path/bin:$PATH
```
It is very important that you keep the `:$PYTHONPATH` or `:$PATH` at the end of these - you
are putting your location at the front of the existing contents of the path. If you leave 
them out, then only your package location will be found and nothing else.


#### Troubleshooting: remove your pip cache

If you built something and it went wrong, and are trying to reinstall it with `pip` and keep 
getting errors that you think you should have fixed, you may still be using a previous cached version. 
The cache is in `.cache/pip` in your home directory, and you can delete it.

You can prevent caching entirely by installing using `pip3 install --user --no-cache-dir <python3pkg>`




