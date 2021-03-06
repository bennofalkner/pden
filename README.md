--------------------------------------------------------------------------------

                          PDEN - Protein Density Tools

PDEN is offering tools and a C library to work on density files (typically pro-
teins). The entier library is using an object oriented approach, hiding al lot of 
optimizations. 
While optimizing DireX(http://www.schroderlab.org) density processing, it became 
helpful to extract the density handling from the original program and offer all 
functions in another module. The first approach was SplitFFT which just extracted 
functions operating on densities, today the entire datamanagment has been ex-
tracted. 

--------------------------------------------------------------------------------

INSTALL:

Installing PDEN is pretty straightforward on Unix or Unix-like (Linux, Mac OS X, 
BSD) systems with a C compiler, Make and GNU Build Tools (using GIT) installed. 
Installing on other platforms is not tested but should be possible on Windows 
using MinGW. 

PDEN depends on FFTW3 (see Dependencies).

Default Installation:

If you start from GIT, please run:

$ sh autogen.sh <configure args>

It will setup the buildscripts and directly call configure with the given 
arguments and make.

If you downloaded a package (tar.gz ...) please run:

$ sh configure

You can get information about available configuration options by running:

$ sh configure --help

If everything went okay, type 

$ make

to build the library and all tools.

Finally to install to a system-wide location you might need to become root or:

$ sudo make install

Important configuration options are:
    --enable-openmp/--disable-openmp       to build lib with openMP support 
                                           (default is yes) (in development)

    --enable-single/--disable-single       to build as single precision library
                                           this can be usefull if you plan to 
					   handle sets of densities to reduce 
					   memory footprint (default is double) 

--------------------------------------------------------------------------------

TOOLS:

The tested tools of PDEN. Especially if you start building from GIT there may be 
additional tools available. 

    pdnormalize      normalize a density map to mu=0.0 and sigma=1.0

    pdcalcsf         calculate the structur factor of a density (radial 
                     structure factor)

    pdapplysf        apply a structure factor correcting function (today only
                     Babinet's principal is supported

    pdrefinesf       refine coefficients for structure factor correction that 
                     can be used in 'pdapplysf'
	
--------------------------------------------------------------------------------

LIBRARY:

A documentation of the library can be created using Doxygen.

$ sh autogen.sh doxygen

All exported/pulic functions are listed in pden.h (double precision) and pdenf.h
(single prcision

--------------------------------------------------------------------------------

DEPENDENCIES:

Right now PDEN only depends on FFTW3 for Fourier transforms. The library is 
available at http://www.fftw.org.

On Linux most distributions offer the FFTW3 as a prebuild package. Use:

apt-get install fftw3

on Debian, Ubuntu etc. or 

yum install fftw3

on Fedora, Suse, Redhead ...

If you have to install FFTW3 it is suggested to install single and double 
precision libraries. Therefor you have to build fftw3 twice.

Change to FFTW3 source directory and run: 

$ sh configure 
$ sh make

and as root or sudo:

$ make install

Now you have to build the single precision library:

$ make clean
$ configure --enable-float
$ make
 and again as root/sudo:

$ make install

On newer Macs with OS X ( >= 10.7 ? ) there is a known problem with the library path, so if this 
problem appears please run:

$ echo "PATH=/usr/local/bin:$PATH export PATH" >> ~/.bash_profile

--------------------------------------------------------------------------------

KNOWN BUGS:

- compiling on linux with gcc version 4.6.3 (Ubuntu/Linaro 4.6.3-1ubuntu5) 
could causes problems during sfrefinement:
		"Armijo rule line search not converged"
	SOLUTION: could be removed because of some changes in the code
	seems to be connected to type qualifiers nd optimization 

- compiling with "-ffast-math" causes several functions to produce very 
large values 
	SOLUTION: do not use "-ffast-math" 


