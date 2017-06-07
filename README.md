![alt text](doc/source/images/portcullis_logo.png "Portcullis")

Portcullis
==========

Portcullis stands for PORTable CULLing of Invalid Splice junctions from pre-aligned 
RNA-seq data.  It is known that RNAseq mapping tools generate many invalid junction
predictions, particularly in deep datasets with high coverage over splice sites.
In order to address this, instead for creating a new RNAseq mapper, with a focus 
on SJ accuracy we created a tool that takes in a BAM 
file generated by an RNAseq mapper of the user's own choice (e.g. Tophat2, Gsnap, 
STAR2 or HISAT2) as input (i.e. it's portable).  It then, analyses and quantifies 
all splice junctions in the file before, filtering (culling) those which are unlikely 
to be genuine.  Portcullis output's junctions in a variety of formats making it
suitable for downstream analysis (such as differential splicing analysis and gene
modelling) without additional work.  Portcullis can also filter the original BAM file removing alignments 
associated with `bad` junctions.  Both the filtered junctions and BAM files are cleaner
and more usable resources which can more effectively be used to assist in downstream 
analyses such as gene prediction and genome annotation. 

Installation
------------

There are two ways to install portcullis from source, either by cloning the git 
repository, or by downloading a distributable package, the later method is generally 
recommended as it reduces the number of installation steps and dependencies required 
to be on your system.

When installing from distributable first confirm dependencies are installed and configured:

 - **GCC** V4.8+
 - **make**
 - **libtool** V2.4.2+
 - **zlib**
 - **pthreads**
 - **Boost** (system,filesystem,program_options,chrono,timer) V1.53+
 - **samtools** V1.2+
 - **Python3** (including python3 development libraries and the *numpy*, *scipy*, *matplotlib*, and *sklearn* packages)
 - **Sphinx-doc** V1.3+ (Optional: only required for building the documentation.  Sphinx comes with anaconda3, however if not using anaconda3 then install according to the instructions on the sphinx website: [http://www.sphinx-doc.org/en/stable/instructions](http://www.sphinx-doc.org/en/stable/instructions))
  
Then proceed with the following steps:

 - Download the latest tarball from here: [https://github.com/maplesond/portcullis/releases](https://github.com/maplesond/portcullis/releases).  NOTE: Please make sure not to download the github source code zips.  The portcullis distributables have the following filename format ```portcullis-<version>.tar.gz```.
 - Decompress and untar: ```tar -xvf portcullis-<version>.tar.gz```
 - Change into directory: ```cd portcullis-x.x.x```
 - Generate makefiles and confirm dependencies: ```./configure```
 - Compile software: ```make```
 - Run tests (optional) ```make check```
 - Install: ```sudo make install```

Should you wish to install from a cloned git repository instead, do the following:

  - Ensure these tools are correctly installed and available on your system:
      - **autoconf** V2.53+
      - **automake** V1.11+
  - Clone the git repository (For ssh: ```git clone git@github.com:maplesond/portcullis.git```; or for https: ```git clone https://github.com/maplesond/portcullis.git```), into a directory on your machine.
  - "cd" into root directory of the installation  
  - Create configuration script by typing: ```./autogen.sh```.
  - Follow all steps described in "Installing from a distributable" (except for the download and decompress tarball steps).


The configure script can take several options as arguments.  One commonly modified 
option is ```--prefix```, which will install portcullis to a custom directory.  By 
default this is "/usr/local", so the portcullis executable would be found at "/usr/local/bin" 
by default.  In addition, some options specific to managing portcullis dependencies 
located in non-standard locations are:

  - ```--with-boost``` - for specifying a custom boost installation directory
  - ```--with-zlib``` - for specifying a custom zlib installation directory

Type ```./configure --help``` for full details.


Operating Instructions
----------------------

After portcullis has been installed, the ```portcullis``` executable should be available.

Typing ```portcullis``` or ```portcullis --help``` at the command line will present you with the portcullis help message.

These modes are available:

 - **prep**    - Prepares input data so that it is suitable for junction analysis
 - **junc**    - Calculates junction metrics for the prepared data
 - **filter**  - Separates alignments based on whether they are likely to represent genuine splice junctions or not
 - **bamfilt** - Filters a BAM to remove any reads associated with invalid junctions
 - **full**    - Runs prep, junc, filter and optionally bamfilt as a complete pipeline

Typing ```portcullis <mode> --help``` will bring up help and usage information specific to that mode.

In addition to portcullis, we provide a tool-suite for manipulating junction files

An online version of the manual can be found here: [https://portcullis.readthedocs.org/en/latest/](https://portcullis.readthedocs.org/en/latest/).

Licensing
---------

GNU GPL V3.  See COPYING file for more details.


Authors
-------

 * Daniel Mapleson
 * Luca Venturini
 * David Swarbreck

See AUTHORS file for more details.


Acknowledgements
----------------

Affiliation: The Genome Analysis Centre (TGAC)
Funding: The Biotechnology and Biological Sciences Research Council (BBSRC)
