.. _p-soft:

Pegasus Software Modules
========================

IDSC ACS continually updates applications, compilers, system libraries, etc.
To facilitate this task and to provide a uniform mechanism for accessing
different revisions of software, ACS uses the modules utility. At login,
modules commands set up a basic environment for the default compilers,
tools, and libraries such as:  the ``$PATH``, ``$MANPATH``, and
``$LD_LIBRARY_PATH`` environment variables. There is no need to set them
or update them when updates are made to system and application software.

From Pegasus, users can view currently loaded modules with **module
list** and check available software with **module avail *package***
(omitting the package name will show all available modules). Some
modules are loaded automatically upon login:

::

    [username@pegasus ~]$ module list
    Currently Loaded Modulefiles:
      1) perl/5.18.1(default)    2) python/2.7.3(default)   3) gcc/4.4.7(default)      4) share-rpms65
    [username@pegasus ~]$ module avail R

    ---------------------- /share/Modules/general ----------------------
    R/2.15.2         R/3.1.2(default) R/3.3.1

    [username@pegasus ~]$ module load R
    [username@pegasus ~]$ module list
    Currently Loaded Modulefiles:
      1) perl/5.18.1(default)    2) python/2.7.3(default)   3) gcc/4.4.7(default)      4) share-rpms65            5) R/3.1.2(default)

Available software modules can also be viewed on the `CCS
Portal <https://portal.ccs.miami.edu>`__ including description, version,
and update date.

The table below lists commonly used modules commands.


.. list-table:: Pegasus Modules   
   :header-rows: 1
   
   * - Command 
     - Purpose 
   * - ``module avail`` 
     - lists all available modules 
   * - ``module list`` 
     - list modules currently loaded    
   * - ``module purge`` 
     - restores original setting by unloading all modules  
   * - ``module load package`` 
     - loads a module e.g., the python package  
   * - ``module unload package``
     - unloads a module e.g., the python package   
   * - ``module switch old new`` 
     - replaces old module with new module  
   * - ``module display package`` 
     - displays location and library information about a module


See our :ref:`Policies <policies>` page for minimum requirements and more information.
