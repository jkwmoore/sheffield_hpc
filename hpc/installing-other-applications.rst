.. _installing-other-applications:

Installing other applications on Bessemer and ShARC
===================================================

Bessemer and ShARC, being general purpose HPC clusters, we provide and maintain only the most essential and most popular applications on it.

However, we are aware of our users' need to run applications that are specific to their own subject areas of research.

Multi-user software install: we have put in place a mechanism for competent users to download and install applications of their own choice on the Bessemer and ShARC clusters.

This option should be seen as a service without support as we will expect such users to be able to tackle the problems encountered during the installation on their own. We will however help make such software available to other iceberg and ShARC users by copying/installing scripts to shared locations.

Here are a few highlights of this service:

Some software installation procedures require running a command called configure that sets up the installation in a default location which is usually a system area where users do not have write access. If you do need to run configure to install a program on iceberg under your area you can use the following parameter to configure to install the software on a specified location.

::
    ./configure --prefix /home/csxyz

We shall make available an area ( under /usr/local/extras ) with necessary disk space for the work,
we shall give the principle installer full access rights to this area for installation work,
if and when necessary we shall help install the execution scripts to a commonly accessible area and create module files.

The fact that during the installation there will be no (write access) to some system areas should not present any major problems.

Here are some technical hints;

Extra libraries that may be needed can be installed under the programs own directory and
the LD_LIBRARY_PATH system variable can be altered to add this directory to it;
i.e. LD_LIBRARY_PATH=$LD_LIBRARY_PATH:location_of_your_own_library
Similarly PATH variable can be altered either by
PATH=$PATH:location_of_your_own_executables
or
by using the addpath locally written command. Just type addpath for further info.
the above changes can be inserted into your own .bashrc file to automate it all
Finally we can create a module that implements these so that anyone can use the module load command to access the software. If you like to take advantage of this option contact research-it@sheffield.ac.uk .

Single user software install: users can install software in their /home or /data directories as follows:

1) binary installs - copy the relevant binary files to a folder of
your choice (in general create a folder with the software name e.g.
plink_install). The path to this folder is:  ::

    /home/username/plink_install

The executable can then be run in 2 ways: ::

    cd /home/username/plink_install

If the binary is called plink then run it using: ::

    ./plink

OR, from anywhere in your directory structure run using

/home/username/plink_install/plink

2) build & install source code - copy the source code (normally a .zip
or .tar.gz) to your /home or /data areas. Extract the files using
unzip or tar xf, & then cd into the source code directory. It is
important to read the README file here since this will give details on
how to build the code & any dependencies etc. However in general the
build process is as follows:

Source code is for an application called wobble.

Install the software in a directory called wobble_install in /data:

mkdir /data/username/wobble_install

#cd into the source code directory which we extracted
cd wobble
module load dev/gcc/4.9.4 (altho the README file may suggest a
different gcc version &/or cmake)
./configure --prefix=/data/username/wobble_install
make install

if the wobble executable is called wobble, located in
/data/username/wobble_install/bin, then it can be run using:

/data/username/wobble_install/bin/wobble

Note for both (1) & (2) above you can add the directories containing the executables to the PATH variable so that to run the executables you just type their names i.e. plink or wobble:

export PATH=path_to_executable_folder:$PATH

NOTE on Library dependencies - sometimes during a build you will get errors related to missing libraries or other dependencies (these
should be specified in the README file). However before you trigger a
help desk call check to see if the library or other dependency is
available on ShARC. Do this using: ::

    module avail

or: ::

    module avail |& grep -i name_of_dependency

If it is available on ShARC then load it using:

    module load name_module
