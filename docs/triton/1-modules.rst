.. _t-soft:

Triton Software Modules
=======================

Triton software versions (and dependencies) are deployed through Lmod,
an upgraded Environment Modules suite.

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

The StdEnv on Triton has the IBM Advance Toolchain for PowerLinux GNU
suite. This suite contains optimized gcc 8.3.1 for Power9 systems.

-  show loaded modules with ``module list`` or ``ml``
-  show StdEnv settings with ``module show StdEnv`` or
   ``ml show StdEnv`` (currently just the AT 12.0 module)

::

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv

    [username@login1 ~]$ ml show StdEnv
    ----------------------------------------------------------------------------
       /share/mfiles/Core/StdEnv.lua:
    ----------------------------------------------------------------------------
    help([[  Lua Help for the Standard Environment module configurations on Triton
    ]])
    whatis("Description: loads standard environment modules")
    load("at/12.0")

Triton available modules
------------------------

The default loaded compiler on Triton is IBM AT 12.0 with optimized GNU
gcc 8.3.1 for Power9 systems.

Available modules at login include the compilers under “Compilers”,
compiler-independent modules under “Core”, and modules dependent on the
AT 12.0 compiler under “Compiler/at/12.0”.

***Note :*** there are some experimental and place-holder modulefiles;
please pardon our dust

-  show loaded modules with ``module list`` or ``ml``
-  show module help info with ``module help NAME`` or ``ml help NAME``
-  show module whatis info with ``module whatis NAME`` or
   ``ml whatis NAME``
-  show available modules with ``module avail`` or ``ml av``
-  show module settings with ``module show NAME`` or ``ml show NAME``
-  load the at/12.0 smpi module with ``module load smpi`` or ``ml smpi``

::

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv



    [username@login1 ~]$ ml help at

    ---------------------- Module Specific Help for "at/12.0" ----------------------
      Lua Help for IBM Advance Toolchain 12.0 module on Triton in local /opt/at12.0

      gcc version 8.3.1 for Power9 systems


    [username@login1 ~]$ ml whatis at
    at/12.0             : IBM Advance Toolchain for PowerLinux
    at/12.0             : Version: 12.0-0
    at/12.0             : Category: compiler suite
    at/12.0             : Description: GNU/Linux toolchain update, IBM AT 12.0 gcc 8.3.1


    [username@login1 ~]$ ml av

    --------------------- /share/mfiles/Compiler/at/12.0 ----------------------
       fftw/3.3.8         myATgccDependentProgram/1.0        smpi/10.02
       hdf5/1.8.16 (D)    openBLAS/0.3.7
       hdf5/1.10.5 (E)    python/3.7.3                (E)

    --------------------------- /share/mfiles/Core ----------------------------
       R/3.6.1                              (E)      anaconda3/2019.07 (E,D)
       Single-Cell-Analysis/Cellranger-atac (E)      cp2k-gpu/7.0
       Single-Cell-Analysis/Cellranger-dna  (E)      cp2k/7.0
       Single-Cell-Analysis/Cellranger      (E,D)    cuda/10.1
       StdEnv                               (L)      java/8.0
       anaconda2/2019.07                    (E)      lammps/2019.08
       anaconda3/ccs-bio                    (E)

    ------------------------- /share/mfiles/Compilers -------------------------
       at/12.0 (L)    gcc/4.8.5    xl/16.1.1.4 (E)

    ..


    [username@login1 ~]$ ml show smpi
    ----------------------------------------------------------------------------
       /share/mfiles/Compiler/at/12.0/smpi/10.02.lua:
    ----------------------------------------------------------------------------
    help([[  Lua Help file for IBM smpi 10.02 with Triton IBM AT 12.0 gcc suite

      gcc version 8.3.1

      sets OMPI_CC, OMPI_FC, and OMPI_CXX to AT gcc suite
    ]])
    whatis("Name:        IBM Spectrum MPI")
    whatis("Version:     10.02")
    whatis("Category:    MPI implementation")
    whatis("Description: Message Passing Interface (MPI) implementation for IBM AT 12.0")
    whatis("Sets OMPI_CC, OMPI_FC, and OMPI_CXX to AT gcc suite")
    setenv("OMPI_FC","gfortran")
    setenv("OMPI_CC","gcc")
    setenv("OMPI_CXX","g++")
    setenv("MPI_ROOT","/share/compilers/ibm/smpi/10.02/")
    prepend_path("MANPATH","/share/compilers/ibm/smpi/10.02/man")
    prepend_path("PATH","/share/compilers/ibm/smpi/10.02/bin")
    prepend_path("MODULEPATH","/share/mfiles/MPI/at/12.0/smpi/10.02")

    [username@login1 ~]$ ml smpi
    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv   3) smpi/10.02

Triton module hierarchies
-------------------------

Switch to a different compiler with the ``module swap`` command. Any
dependent modules should also swap to their new versions.

-  show currently loaded modules with ``ml``
-  switch from at to gcc with ``ml swap at gcc`` or ``ml -at gcc``

   -  note the Lmod reload message for the smpi module

-  show smpi module help for gcc with ``ml help smpi``
-  reset to Triton defaults with ``ml reset``
-  (show currently loaded modules with ``ml``)

::

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv   3) smpi/10.02



    [username@login1 ~]$ ml -at gcc

    Due to MODULEPATH changes, the following have been reloaded:
      1) smpi/10.02

    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) StdEnv   2) gcc/4.8.5   3) smpi/10.02



    [username@login1 ~]$ ml help smpi

    -------------------- Module Specific Help for "smpi/10.02" ---------------------
      Lua Help file for IBM smpi 10.02 with Triton system gcc 4.8.5

     sets OMPI_CC, OMPI_FC, and OMPI_CXX to GNU / gcc suite


    [username@login1 ~]$ ml reset
    Resetting modules to system default. Reseting $MODULEPATH back to system default. All extra directories will be removed from $MODULEPATH.
    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv

More hierarchies and dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Dependency modules can be loaded in the same command, without waiting
for them to appear in ``ml av`` output.

Example : cdo and nco depend on netcdf, and netcdf depends on hdf5.

::

    [username@login1 ~]$ ml hdf5 netcdf cdo nco
    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   3) hdf5/1.8.16    5) cdo/1.9.7.1
      2) StdEnv    4) netcdf/4.7.1   6) nco/4.8.1

To view dependent modules in ``ml av``, first load their prerequisites.

**“Behind the scenes”**

After an hdf5 module is loaded, any available netcdf modules will show
in ``ml av`` output :

-  load the default hdf5 module with ``ml hdf5`` (hdf5/1.8.16)
-  show loaded modules with ``ml`` : at 12.0 compiler, hdf5 1.8.16
   library
-  show available modules with ``ml av`` : netcdf module is available to
   load
-  load the default netcdf module with ``ml netcdf`` (netcdf/4.7.1 –
   currently the only module)

::

    [username@login1 ~]$ ml hdf5
    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv   3) hdf5/1.8.16


    [username@login1 ~]$ ml av

    -------------------- /share/mfiles/Library/hdf5/1.8.16 --------------------
       netcdf/4.7.1

    --------------------- /share/mfiles/Compiler/at/12.0 ----------------------
       fftw/3.3.8           myATgccDependentProgram/1.0        smpi/10.02
       hdf5/1.8.16 (L,D)    openBLAS/0.3.7
       hdf5/1.10.5 (E)      python/3.7.3                (E)

    --------------------------- /share/mfiles/Core ----------------------------
       R/3.6.1                              (E)      anaconda3/2019.07 (E,D)
       Single-Cell-Analysis/Cellranger-atac (E)      cp2k-gpu/7.0
       Single-Cell-Analysis/Cellranger-dna  (E)      cp2k/7.0
       Single-Cell-Analysis/Cellranger      (E,D)    cuda/10.1
       StdEnv                               (L)      java/8.0
       anaconda2/2019.07                    (E)      lammps/2019.08
       anaconda3/ccs-bio                    (E)

    ------------------------- /share/mfiles/Compilers -------------------------
       at/12.0 (L)    gcc/4.8.5    xl/16.1.1.4 (E)

    ..

    [username@login1 ~]$ ml netcdf
    [username@login1 ~]$ ml

    Currently Loaded Modules:
      1) at/12.0   2) StdEnv   3) hdf5/1.8.16   4) netcdf/4.7.1

Once both hdf5 and netcdf are loaded, ``ml av`` shows dependent modules
CDO and NCO :

::

    [username@login1 ~]$ ml av

    ---------------- /share/mfiles/Library/netcdf/4.7.1/hdf5/1.8.16 ----------------
       cdo/1.9.7.1    nco/4.8.1

    ---------------------- /share/mfiles/Library/hdf5/1.8.16 -----------------------
       netcdf/4.7.1 (L)

    ------------------------ /share/mfiles/Compiler/at/12.0 ------------------------
       fftw/3.3.8           myATgccDependentProgram/1.0        smpi/10.02
       hdf5/1.8.16 (L,D)    openBLAS/0.3.7
       hdf5/1.10.5 (E)      python/3.7.3                (E)

    ------------------------------ /share/mfiles/Core ------------------------------
       R/3.6.1                              (E)      anaconda3/2019.07 (E,D)
       Single-Cell-Analysis/Cellranger-atac (E)      cp2k-gpu/7.0
       Single-Cell-Analysis/Cellranger-dna  (E)      cp2k/7.0
       Single-Cell-Analysis/Cellranger      (E,D)    cuda/10.1
       StdEnv                               (L)      java/8.0
       anaconda2/2019.07                    (E)      lammps/2019.08
       anaconda3/ccs-bio                    (E)

    --------------------------- /share/mfiles/Compilers ----------------------------
       at/12.0 (L)    gcc/4.8.5    xl/16.1.1.4 (E)

    ..

