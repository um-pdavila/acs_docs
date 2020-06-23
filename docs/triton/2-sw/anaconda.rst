Anaconda on Triton
==================

Introduction
------------

Anaconda is an open-source distribution of the Python and R programming
languages for scientific computing. The Anaconda distribution comes with
conda, which is a package manager and environment manager, and over 150
packages automatically installed (other 1,500+ packages could be
downloaded and installed easily from the Anaconda repository). In order to use Anaconda on Triton, you need to have access to the UM network and the Triton system. 
Please check the `CCS AC Policies <https://acs-docs.readthedocs.io/policies/README.html>`__.

Conda Environment
-----------------

A Conda environment contains a specific collection of application software, frameworks and their dependencies that are maintained and run separately from software in another environment.

Using Conda environment on the command line
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``ml anaconda3/<version>`` or ``ml wml_anaconda3/<version>`` 
-  ``conda activate <your environment or system installed environment>``
-  Run test program which dependencies have been installed in the environment
-  ``conda deactivate``

.. note::
   Only small test program should be run on the command line. Formal job needs to be submitted via LSF.

Using Conda environment in the LSF job script
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An LSF job script example using Conda environment:

::

    #!/bin/bash
    #BSUB -J "job_example"
    #BSUB -o "job_example_%J.out"
    #BSUB -e "job_example_%J.err"
    #BSUB -n 4
    #BSUB -R "rusage[mem=2G]"
    #BSUB -q "normal"
    #BSUB -W 00:30
    #BSUB -B
    #BSUB -N
    #BSUB -u <my_email>@miami.edu

    ml anaconda3
    conda activate <my_environment>
    cd <path to my_program.py>

    python ./<my_program.py> 

In my\_program.py, you can import any package that has been installed in your environment.
Details about job scheduling can be found at `Pegasus Job
Scheduling <https://acs-docs.readthedocs.io/pegasus/jobs/README.html>`_.

.. note::
   On Triton, please use ``normal`` queue which is different from Pegasus.

Different Anaconda Installed on Triton
--------------------------------------

Several Anaconda have been installed on Triton. You can use ``module load`` (``ml`` as a shortcut)
to load different Anaconda. Loading the module does ``source <anaconda installed path>/etc/profile.d/conda.sh``
behind the scences.

Anaconda3
~~~~~~~~~

Anaconda3 has Python 3.x as its base Python version (although it can download Python 2.x as well). 
On Triton, different versions of Anaconda3 located at
``/share/apps/anaconda3/`` use the default configuration
which will search packages from ``https://repo.anaconda.com/pkgs/main``
and ``https://repo.anaconda.com/pkgs/r``. 

In order to use it, run ``ml anaconda3/<version>``.
``ml anaconda3`` will load the default version which is Anaconda3-2019.10 at the time the document is edited.

Anaconda2
~~~~~~~~~

Anaconda2 has Python 2.x as its base Python version.
On Triton, different versions of Anaconda2 located at
``/share/apps/anaconda2/`` use the default configuration
which will search packages from ``https://repo.anaconda.com/pkgs/main``
and ``https://repo.anaconda.com/pkgs/r``. 

In order to use it, run ``ml anaconda2/<version>``.
``ml anaconda2`` will load the default version which is Anaconda2-2019.07 at the time the document is edited.

Anaconda3 for Deep Learning
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Anaconda3 for Deep Learning is configured to first search packages from the deep learning channel
supported by IBM at
``https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/``,
and then the ``https://repo.anaconda.com/pkgs/main`` and ``https://repo.anaconda.com/pkgs/r`` channels.

In order to use it, run ``ml wml_anaconda3/<version>``.
``ml wml_anaconda3`` will load the default version which is Anaconda3-2019.10 at the time the document is edited.

More details can be found at `IBM WML on Triton User
Menu <https://acs-docs.readthedocs.io/triton/2-sw/wmlce.html>`__.


Creating An Conda Environment
-----------------------------

For Python
~~~~~~~~~~

If you are not sure what packages to be installed while creating the environment

$ ``conda create -n <environment name> python=<version>``

For example, ``conda create -n my_env python=3.7`` will create a Conda
environment named ``my_env`` and Conda will install the latest Python
3.7.x it can find.

If you know what packages you need for this environment

$
``conda create -n <environment name> python=<version> <package1> <package2> <...>``

For example, ``conda create -n my_env python=3.7 numpy scipy`` will
create a Conda environment with the latest Python 3.7.x and two packages
numpy and scipy. It will resolve the dependencies altogether and avoid
further conflicts, so this is the recommended way to create the
environment.

The environement will be created at ``~/.conda/envs`` when using
``conda create -n ...``.

For R
~~~~~

$ ``conda create -n <r environemnt name> -c conda-forge r-base``

``-c conda-forge`` guides conda to find the ``r-base`` package from
``conda-forge`` channel. Channels are locations for the repositories
where conda looks for packages. In the next section, we will discuss how
to find the public channels.

Installing Conda Packages
-------------------------

After creating your environment, you can install more packages. First
activate the environment

$ ``conda activate <environment name>``

Then install the package

(<environment>)$ ``conda install <package>`` or
``conda install <package>=<version>`` if you want a specific version.

If Conda finds the package from the channels configured, it will
download and install the package.

If the package is not found, you can do a search in the `Anaconda
Cloud <https://anaconda.org/>`__ and choose Platform ``linux-ppc64le``.
Click on the name of the found package, the detail page will show you
the specific channel to install the package. Then you can do

(<environment>)$ ``conda install -c <channel> <package>``

If the package is still not found, try

(<environment>)$ ``pip install <package>``

.. warning:: 
   Issues may arise when using pip and conda together.
   Only after conda has been used to install as many packages
   as possible should pip be used to install any remaining software. If
   modifications are needed to the environment, it is best to create a new
   environment rather than running conda after pip.

Installing Your Own Anaconda
----------------------------

If you would like to manage your own Anaconda, you can install it in
your home directory following the `instruction of Installing Anaconda on
Linux
POWER <https://docs.anaconda.com/anaconda/install/linux-power8/>`__.
