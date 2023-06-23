R on Pegasus
============

R is available on Pegasus through the ``module`` command. You can load 
R into your environment by typing the following on the commandline:

::

    [username@pegasus ~]$ module load R

This loads the default version of R, currently ``4.1.0``. To load a specific
version of R, say, ``3.6.3``, you can type the following:

::

    [username@pegasus ~]$ module load R/3.6.3


To see a list of available software, including R versions, use the command 
``module avail``. For more information about software available on Pegasus, 
see :ref:`Software on the Pegasus Cluster <p-soft>`.

Batch R
-------

To run a batch R file on the compute nodes on Pegasus, submit the file to LSF
with ``R CMD BATCH filename.R``, with ``filename`` being the name of your R script.
This can be done using the following (two) command:

::

    [username@pegasus ~]$ module load R/4.1.0
    [username@pegasus ~]$ bsub -q general -P projectID R CMD BATCH filename.R
    Job is submitted to <projectID> project.
    Job <6101046> is submitted to queue <general>.

Batch jobs can also be submitted to LSF with script files, such as 
``example.job`` shown below.

::

    example.job
    #!/bin/bash
    #BSUB -J R_job            # name of your job
    #BSUB -e filename.e%J     # file that will contain any error messages
    #BSUB -o filename.o%J     # file that will contain standard output
    #BSUB -R "span[hosts=1]"  # request run script on one node
    #BSUB -q general          # request run on general queue
    #BSUB -n 1                # request 1 core
    #BSUB -W 2                # request 2 minutes of runtime
    #BSUB -P projectID        # your projectID
    R CMD BATCH filename.R    # R command and your batch R file

When using such a script file, the batch job can be submitted by typing the 
following on the commandline

::

    [username@pegasus ~]$ bsub < example.job

Interactive R
-------------

R can also be run interactively by requesting resources on
the interactive queue. This can be done by first loading R into your 
environment

::

[username@pegasus ~]$ module load R/4.1.0

and then requesting an interactive R session by typing on the commandline

::

[username@pegasus ~]$ bsub -Is -q interactive R

or 

::

[username@pegasus ~]$ bsub -Is -P ProjectID R

making sure to replace ProjectID with the actual name of your project.

R packages
----------

To install R packages, you'll need to confirm that your package's 
pre-requisites are met, either in your local environment or through
loading the appropriate modules on the cluster. You will need to load any cluster modules that are pre-requisites, and install locally any other pre-requisites.  See :ref:`Pegasus Cluster Software Installation <soft-install>` for help with complex requirements.

From the R prompt, install any R package to your personal R library with
the standard ``install.package()`` R command. Choose ``y`` when asked
about using a personal library, and ``y`` again if asked to create one.

::

    >  install.packages("doParallel", repos="http://R-Forge.R-project.org")
    Warning in install.packages("doParallel", repos = "http://R-Forge.R-project.org") :
      'lib = "/share/opt/R/3.1.2/lib64/R/library"' is not writable
    Would you like to use a personal library instead?  (y/n) y
    Would you like to create a personal library
    ~/R/x86_64-unknown-linux-gnu-library/3.1
    to install packages into?  (y/n) y
    ...

Contact `IDSC ACS <mailto:hpc@ccs.miami.edu>`_ to review any core library pre-requisites & dependencies, for cluster-wide installation.  


R file examples
~~~~~~~~~~~~~~~

``example1.R``

--------------

.. code:: r

     # create graphical output file
    pdf("example1.pdf")

    # Define two vectors v1 and v2
    v1 <- c(1, 4, 7, 8, 10, 12)
    v2 <- c(2, 8, 9, 10, 11, 15)

    # Creat some graphs
    hist(v1)
    hist(v2)
    pie(v1)
    barplot(v2)

    # close the file
    dev.off() 

If you have forwarded your display, open the pdf from the Pegasus prompt
with evince.

::

    [username@pegasus ~]$ evince example1.pdf

.. figure:: assets/r_example1pdf-246x300.png
   :alt: example1.png

   example1.png
