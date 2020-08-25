.. _t-soft:

Triton Software Modules
=======================

Triton software versions (and dependencies) are deployed through Lmod, an upgraded Environment Modules suite.

https://lmod.readthedocs.io/en/latest/010_user.html

Module Commands
---------------

Shortcut commands are also available :

+---------------------------+-----------------------+------------------+
| Command                   | Shortcut              | Description      |
+===========================+=======================+==================+
| module list               | ml                    | list currently   |
|                           |                       | loaded modules   |
+---------------------------+-----------------------+------------------+
| module avail              | ml av                 | list available   |
|                           |                       | modules, based   |
|                           |                       | on currently     |
|                           |                       | loaded           |
|                           |                       | hierarchies      |
|                           |                       | (compilers,      |
|                           |                       | libraries, etc.) |
+---------------------------+-----------------------+------------------+
| module avail pkgName1     | ml av pkgName1        | search available |
|                           |                       | modules, based   |
|                           |                       | on currently     |
|                           |                       | loaded           |
|                           |                       | hierarchies      |
+---------------------------+-----------------------+------------------+
| module is-avail pkgName1  | ml is-avail pkgName1  | check if         |
|                           |                       | module(s) can be |
|                           |                       | loaded, based on |
|                           |                       | currently loaded |
|                           |                       | hierarchies      |
+---------------------------+-----------------------+------------------+
| module spider             | ml spider             | list all modules |
+---------------------------+-----------------------+------------------+
| module spider pkgName1    | ml spider pkgName1    | search all       |
|                           |                       | modules          |
+---------------------------+-----------------------+------------------+
| module keyword word1      | ml keyword word1      | search module    |
|                           |                       | help and whatis  |
|                           |                       | for word(s)      |
+---------------------------+-----------------------+------------------+
| module spider             | ml spider             | show how to load |
| pkgName1/Version          | pkgName1/Version      | a specific       |
|                           |                       | module           |
+---------------------------+-----------------------+------------------+
| module load pkgName1      | ml pkgName1           | load module(s)   |
|                           |                       | by name (default |
|                           |                       | version)         |
+---------------------------+-----------------------+------------------+
| module load               | ml pkgName1/Version   | load module(s)   |
| pkgName1/Version          |                       | by name and      |
|                           |                       | version          |
+---------------------------+-----------------------+------------------+
| module unload pkgName1    | ml -pkgName1          | unload module(s) |
|                           |                       | by name          |
+---------------------------+-----------------------+------------------+
| module reset              | ml reset              | reset to system  |
|                           |                       | defaults         |
+---------------------------+-----------------------+------------------+
| module restore            | ml restore            | reset to user    |
|                           |                       | defaults, if     |
|                           |                       | they exist       |
+---------------------------+-----------------------+------------------+
| module help pkgName1      | ml help pkgName1      | show module help |
|                           |                       | info             |
+---------------------------+-----------------------+------------------+
| module whatis pkgName1    | ml whatis pkgName1    | show module      |
|                           |                       | version info     |
+---------------------------+-----------------------+------------------+
| module show pkgName1      | ml show pkgName1      | show module      |
|                           |                       | environment      |
|                           |                       | changes          |
+---------------------------+-----------------------+------------------+

Triton Standard Environment
---------------------------

The StdEnv on Triton contains the default configurations for the cluster.

-  show loaded modules with ``module list`` or ``ml``
-  show StdEnv settings with ``module show StdEnv`` or
   ``ml show StdEnv`` 

::

    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv

    [username@login1 ~]$ ml show StdEnv
    ----------------------------------------------------------------------------
       /share/mfiles/Core/StdEnv.lua:
    ----------------------------------------------------------------------------
    help([[  Lua Help for the Standard Environment module configurations on Triton
    ]])
    whatis("Description: loads standard environment modules")
    load("gcc/4.8.5")


Triton available modules
------------------------

Available modules at login include the compilers under “Compilers”, compiler-independent modules under “Core”, and modules dependent on the currently loaded compiler. 

***Note :*** some modulefiles are marked (E) for Experimental.  As with all software, please report any issues to `hpc@ccs.miami.edu <mailto:hpc@ccs.miami.edu>`_.

-  show loaded modules with ``module list`` or ``ml``
-  show module help info with ``module help NAME`` or ``ml help NAME``
-  show module whatis info with ``module whatis NAME`` or
   ``ml whatis NAME``
-  show available modules with ``module avail`` or ``ml av``
-  show module settings with ``module show NAME`` or ``ml show NAME``
-  load a module with ``module load NAME`` or ``ml NAME``

::

    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv


    [username@login1 ~]$ ml help gcc

	--------------------- Module Specific Help for "gcc/4.8.5" ---------------------
	Lua Help for Triton system gcc module



    [username@login1 ~]$ ml whatis gcc
	gcc/4.8.5           : GNU compiler suite
	gcc/4.8.5           : Version: 4.8.5
	gcc/4.8.5           : Category: compiler suite
	gcc/4.8.5           : Description: C, C++ and Fortran compilers


    [username@login1 ~]$ ml av

	----------------------- /share/mfiles/Compiler/gcc/4.8.5 -----------------------
	   hdf5/1.8.16   (E)    myGCCdependentProgram/1.0 (S)    openmpi/3.1.4
	   hwloc/1.11.11        openBLAS/0.3.7                   smpi/10.02

    --------------------------- /share/mfiles/Core ----------------------------
       R/3.6.1                              (E)      anaconda3/2019.07 (E,D)
       Single-Cell-Analysis/Cellranger-atac (E)      cp2k-gpu/7.0
       Single-Cell-Analysis/Cellranger-dna  (E)      cp2k/7.0
       Single-Cell-Analysis/Cellranger      (E,D)    cuda/10.1
       StdEnv                               (L)      java/8.0
       anaconda2/2019.07                    (E)      lammps/2019.08
       anaconda3/ccs-bio                    (E)

    ------------------------- /share/mfiles/Compilers -------------------------
       at/12.0    gcc/4.8.5 (L)   xl/16.1.1.4 (E)

    ..


    [username@login1 ~]$ ml show gcc
	----------------------------------------------------------------------------
	   /share/mfiles/Compilers/gcc/4.8.5.lua:
	----------------------------------------------------------------------------
	help([[Lua Help for Triton system gcc module
	]])
	whatis("GNU compiler suite")
	whatis("Version: 4.8.5")
	whatis("Category: compiler suite")
	whatis("Description: C, C++ and Fortran compilers")
	setenv("CC","gcc")
	setenv("CXX","g++")
	setenv("FC","gfortran")
	prepend_path("LD_LIBRARY_PATH","/usr/lib")
	prepend_path("MANPATH","/usr/man")
	prepend_path("PATH","/usr/bin")
	prepend_path("MODULEPATH","/share/mfiles/Compiler/gcc/4.8.5")
	family("compiler")

    [username@login1 ~]$ ml smpi
    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv   3) smpi/10.02


Triton module hierarchies
-------------------------

Switch to a different compiler with the ``module swap`` command. Any dependent modules should also swap, if both versions exist.  The SMPI module has both a gcc version, and an at/12.0 version.  

-  show currently loaded modules with ``ml``
-  show smpi module help with ``ml help smpi`` 
-  switch from gcc to at with ``ml swap gcc at`` or ``ml -gcc at``

   -  note the Lmod "reload" message for the smpi module 
   -  (confirm smpi is loaded with ``ml``)
   
-  show smpi module help with ``ml help smpi`` (a different smpi module)  
-  reset to Triton defaults with ``ml reset``


::

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) StdEnv   2) gcc/4.8.5   3) smpi/10.02
	  
	  
	[username@login1 ~]$ ml help smpi

	-------------------- Module Specific Help for "smpi/10.02" ---------------------
	  Lua Help file for IBM smpi 10.02 with Triton system gcc 4.8.5

	 sets OMPI_CC, OMPI_FC, and OMPI_CXX to GNU / gcc suite


    [username@login1 ~]$ ml -gcc at

    Due to MODULEPATH changes, the following have been reloaded:
      1) smpi/10.02

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv   3) smpi/10.02



    [username@login1 ~]$ ml help smpi

	-------------------- Module Specific Help for "smpi/10.02" ---------------------
	  Lua Help file for IBM smpi 10.02 with Triton IBM AT 12.0 gcc suite

	  gcc version 8.3.1

	  sets OMPI_CC, OMPI_FC, and OMPI_CXX to AT gcc suite


    [username@login1 ~]$ ml reset
    Resetting modules to system default. Reseting $MODULEPATH back to system default. All extra directories will be removed from $MODULEPATH.
    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv


More hierarchies and dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dependency modules can be loaded in the same command, without waiting for them to appear in the output for module list (``ml av``).

Example : cdo, nco, and netcdff depend on "netcdfc".  Netcdfc depends on "hdf5".  They can be loaded in sequence, starting with the first dependency, "hdf5". 

::

    [username@login1 ~]$ ml hdf5 netcdfc netcdff cdo nco
    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5         4) netcdfc/4.7.4 (E)   7) cdo/1.9.8 (E)
	  2) StdEnv            5) netcdff/4.5.3 (E)
	  3) hdf5/1.8.16 (E)   6) nco/4.9.3     (E)

To view dependent modules in ``ml av``, first load their prerequisites.


**"Behind the scenes"**

After an hdf5 module is loaded, any available netcdfc modules will show in ``ml av`` output :

-  load the default hdf5 module with ``ml hdf5`` 
-  show loaded modules with ``ml`` 
-  show available modules with ``ml av`` : netcdfc module now available to load
-  load the default netcdfc module with ``ml netcdfc``
-  show newly available modules with ``ml av`` : netcdff, nco, and cdo now available to load 

::

    [username@login1 ~]$ ml hdf5
    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv   3) hdf5/1.8.16 (E)


    [username@login1 ~]$ ml av

	------------------- /share/mfiles/Library/gcc485/hdf5/1.8.16 -------------------
	   netcdfc/4.7.4 (E)

	----------------------- /share/mfiles/Compiler/gcc/4.8.5 -----------------------
	   hdf5/1.8.16   (E,L)    myGCCdependentProgram/1.0 (S)    openmpi/3.1.4
	   hwloc/1.11.11          openBLAS/0.3.7                   smpi/10.02
	 	 
	 ...

    ..

Once both hdf5 and netcdfc are loaded, ``ml av`` shows the next set of dependent modules :

::


    [username@login1 ~]$ ml netcdf
    [username@login1 ~]$ ml

	Currently Loaded Modules:
	  1) gcc/4.8.5   2) StdEnv   3) hdf5/1.8.16 (E)   4) netcdfc/4.7.4 (E)

    [username@login1 ~]$ ml av

	------------ /share/mfiles/Library/gcc485/netcdfc/4.7.4/hdf5/1.8.16 ------------
	   cdo/1.9.8 (E)    nco/4.9.3 (E)    netcdff/4.5.3 (E)

	------------------- /share/mfiles/Library/gcc485/hdf5/1.8.16 -------------------
	   netcdfc/4.7.4 (E,L)

	----------------------- /share/mfiles/Compiler/gcc/4.8.5 -----------------------
	   hdf5/1.8.16   (E,L)    myGCCdependentProgram/1.0 (S)    openmpi/3.1.4
	   hwloc/1.11.11          openBLAS/0.3.7                   smpi/10.02
	 
	 ...

    ..
