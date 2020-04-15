Anaconda on Triton
==================

In this document

-  the dollar sign ($) indicates the ``text`` follows it is a
   command-line interface (CLI) command that you need to type in.
-  the angle brackets (< >) indicates the enclosed element is mandatory
   that needs to be replaced with the user-dependent information.

Introduction
------------

Anaconda is an open-source distribution of the Python and R programming
languages for scientific computing. The Anaconda distribution comes with
conda, which is a package manager and environment manager, and over 150
packages automatically installed (other 1,500+ packages could be
downloaded and installed easily from the Anaconda repository). In order to use Anaconda on Triton, you need to have access to Triton. Please check the `CCS AC Policies <https://acs-docs.readthedocs.io/policies/README.html>`__.

Conda Environment
-----------------

Conda environemnt is a directory that contains a specific collection of
conda packages and their dependencies, so they can be maintained and run
separately without interference from each other.

The basic procedures when using conda environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. $ ``source <anaconda installed path>/etc/profile.d/conda.sh``
2. $ ``conda activate <environment you created or base>``
3. $ ``conda install <package>`` (only for environment you created)
4. test your code or use the environment in LSF job script
5. $ ``conda deactivate``

Using Different Anaconda Installed on Triton
--------------------------------------------

Several Anaconda have been installed on Triton in the /share directory
and could be used by everyone. The easy way to use a different Anaconda
is to login to Triton from a new terminal ($ ``ssh <caneid>@triton.ccs.miami.edu``) and source the specific
Anaconda ``conda.sh`` file. 

$ ``source <anaconda installed path>/etc/profile.d/conda.sh``

(Note: currently, Anaconda does not work with the Environment Module system, and you are not able to 'unload' it. If you want to switch to another Anaconda, you need to login with a new shell and source the other Anaconda's conda.sh script.)

Anaconda 3
~~~~~~~~~~

Anaconda 3 is for Python 3.x. The latest Anaconda 3 is installed at
``/share/apps/anaconda3/2019.10/``. It uses the default configuration
which will search packages from ``https://repo.anaconda.com/pkgs/main``
and ``https://repo.anaconda.com/pkgs/r``. The conda version is 4.7.12.

In order to use it, run $
``source /share/apps/anaconda3/2019.10/etc/profile.d/conda.sh``

Anaconda 2
~~~~~~~~~~

Anaconda 2 is for Python 2.x. The latest Anaconda 2 is installed at
``/share/apps/anaconda2/2019.10/``. It uses the default configuration
which will search packages from ``https://repo.anaconda.com/pkgs/main``
and ``https://repo.anaconda.com/pkgs/r``. The conda version is 4.7.12.

In order to use it, run $
``source /share/apps/anaconda2/2019.10/etc/profile.d/conda.sh``

Anaconda for Deep Learning
~~~~~~~~~~~~~~~~~~~~~~~~~~

A separate Anaconda is installed for using with the Deep Learning
packages. The Anaconda 3 version 2019.10 for Deep Learning is installed
at ``/share/apps/ibm_wml_ce/1.6.2/anaconda3``. It is configured in the
way that it will first search packages from the deep learning channel
supported by IBM at
``https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/``,
and then the default ``main`` and ``r`` channels.

In order to use it, run $
``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``

More details can be found at `IBM WML on Triton User
Menu <https://acs-docs.readthedocs.io/triton/2-sw/wmlce.html>`__.

Using Anaconda Base Environment (Python)
----------------------------------------

Anaconda comes with over 150 packages automatically installed. You can
use them in the base environment.

After source the ``conda.sh`` file associated with the Anaconda you
choose, you can activate the base environment

$ ``conda activate base``

Then you can check the packages installed in this environment

(base)$ ``conda list``

If the base environment has all packages you needed, you can test your
code in the environment using Python it provides

(base)$ ``python <your file with the requested packages imported>``

When you do the testing, the python code runs on the login node which is
not recommended. The proper way to use the conda environment on Triton
is to integrate it in the LSF job script and submit the job to the
compute node.

An job script example:

::

    #!/bin/bash
    #BSUB -J "job_example"
    #BSUB -o "job_example_%J.out"
    #BSUB -e "job_example_%J.err"
    #BSUB -n 1
    #BSUB -R "rusage[mem=128]"
    #BSUB -q "normal"
    #BSUB -W 00:30
    #BSUB -B
    #BSUB -N
    #BSUB -u <my_email>@miami.edu

    source /share/apps/anaconda3/2019.10/etc/profile.d/conda.sh
    conda activate base
    cd <path to my_test.py>

    python ./<my_test.py> 

In my\_test.py, you can import any package that is provided by the base
environment. Details about job scheduling can be found at `Pegasus Job
Scheduling <https://acs-docs.readthedocs.io/pegasus/jobs/README.html>`_.
On Triton, using ``normal`` queue.

Creating Your Own Environment
-----------------------------

You cannot install extra packages in the system-wise base environment.
If you want other packages, you need to create your environment.

For Python
~~~~~~~~~~

If you are not sure what packages to be installed

$ ``conda create -n <environment name> python=<version>``

For example, ``conda create -n my_env python=3.6`` will create a conda
environment named ``my_env`` and conda will install the latest Python
3.6.x it can find.

If you know what packages you need for this environment

$
``conda create -n <environment name> python=<version> <package1> <package2> <...>``

For example, ``conda create -n my_env python=3.6 numpy scipy`` will
create a conda environment with the latest Python 3.6.x and two packages
numpy and scipy. It will resolve the dependencies altogether and avoid
further conflicts, so this is the recommended way to create the
environement.

The environement will be created at ``~/.conda/envs`` when using
``conda create -n ...``.

For R
~~~~~

$ ``conda create -n <r environemnt name> -c conda-forge r-base=3.6.1``

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

If conda finds the package from the channels configured, it will
download and install the package.

If the package is not found, you can search in `Anaconda
Cloud <https://anaconda.org/>`__ and choose Platform ``linux-ppc64le``.
Click on the name of the found package, the detail page will show you
the specific channel to install the package. Then you can do

(<environment>)$ ``conda install -c <channel> <package>``

If the package is still not found, try

(<environment>)$ ``pip install <package>``

Caveat: Issues may arise when using pip and conda together. When
combining conda and pip, it is best to use an isolated conda
environment. Only after conda has been used to install as many packages
as possible should pip be used to install any remaining software. If
modifications are needed to the environment, it is best to create a new
environment rather than running conda after pip.

Installing Your Own Anaconda
----------------------------

If you would like to manage your own Anaconda, you can install it in
your home directory following the `instruction of Installing Anaconda on
Linux
POWER <https://docs.anaconda.com/anaconda/install/linux-power8/>`__.
