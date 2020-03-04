IBM WML CE (version 1.6.2) on Triton User Menu
==============================================

In this document

-  the dollar sign ($) indicates the ``text`` follows it is a
   command-line interface (CLI) command that you need to type in.
-  the angle brackets (< >) indicates the enclosed element is mandatory
   that needs to be replaced with the user-dependent information. For
   example, if your CaneID is ``abc123``, you need to replace
   ``ssh <your caneid>@triton.ccs.miami.edu`` with
   ``ssh abc123@triton.ccs.miami.edu``.

Introduction
------------

Each of Triton's compute nodes is an IBM POWER System AC922 with two
NVIDIA Tesla V100 GPUs, which is engineered to be `the most powerful
training
platform <https://www.ibm.com/us-en/marketplace/power-systems-ac922>`__.
In order to release the power of the advanced hardware, IBM provides
Watson Machine Learning Community Edition (WML CE) which is a set of
software packages for deep learning and machine learning development and
applications on the state-of-the-art POWER system equiped with the most
advanced NVIDIA GPUs. WML CE contains the popular open source deep
learning frameworks such as TensorFlow and PyTorch, IBM-optimized Caffe,
IBM's machine learning library (Snap ML) and software for distributed
training (DDL) and large model support (LMS).

Login
-----

-  $ ``ssh <your caneid>@triton.ccs.miami.edu``

Using Anaconda
--------------

The WML CE packages are distributed as conda packages in `an online
conda
repository <https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/>`__.
You can use Anaconda or Miniconda to install and manage the packages.

On Triton, you have two options:

-  Option 1. You can use the system-wise Anaconda installed specifically
   for using with WML CE v1.6.2. The version of the Anaconda is 2019.07
   which has been tested and supported for the v1.6.2 release of WML CE.
   The installation and configuration can be found at the end of this
   document. We recommend you use this system-wise Anaconda, since it
   will be easier for us to track down the problem if you need
   assistance.

-  Option 2. You can also install Anaconda or Miniconda at your home
   directory following `the WML CE system setup
   guide <https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/wmlce_setupAnaconda.html>`__,
   and handle it by yourself.

Conda general commands:
~~~~~~~~~~~~~~~~~~~~~~~

-  $ ``conda create -n <environment name> python=<version>`` to create
   an environment
-  $ ``conda env list`` to list all available environments
-  $ ``conda activate <environment name>`` to activate an environment

Inside an environment (after activating the environment):

-  $ ``conda list`` to list installed packages
-  $ ``conda install <package name>`` to install a package
-  $ ``conda install <package name>=<version>`` to install a package
   with a specific version
-  $ ``conda install -c <url> <package name>`` to install a package from
   a specific channel (repository)
-  $ ``conda remove <package name>`` to uninstall a package
-  $ ``conda deactivate`` to deactivate the environment

Details and more conda commands can be found at:
https://docs.conda.io/projects/conda/en/latest/commands.html#conda-general-commands

Installing WML CE packages
--------------------------

If you choose to use the system-wise Anaconda, you can activate the
conda functions by executing the conda shell script. (Since multiple
Anaconda configured for different applications have been installed in
the system, this needs to be done every time you log into the system and
wants to use the WML CE packages.)

-  $
   ``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``

Then,

-  $ ``conda create -n <your environment> python=<version>`` (The only
   valid Python versions with WML CE are Python 3.6 and 3.7)
-  $ ``conda activate <your environment>``

Installing all the WML CE packages at the same time in your environment:

-  (your environment)$ ``conda install powerai=1.6.2``

Or installing individual package:

-  (your environment)$ ``conda install <WML CE supported package>``

Notes:

-  The packages installed in this way come with specific versions which
   have been tested and supported by IBM. You can check the packages
   versions at
   https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/#/
   with Releases 1.6.2.

-  If you need another version, first check if it is supported by an
   earlier WML CE version by changing the Releases to 1.6.1 or 1.6.0. If
   it was supported, you can install the package with
   ``powerai-release=<version>``. For example: if you need PyTorch 1.1.0
   which is supported in WML CE v1.6.1, you can do
   ``conda install pytorch powerai-release=1.6.1``

-  If you need a non-supported version, check the section
   ``Installing packages not supported in WML CE``

Using WML CE packages
---------------------

Small testing on login node
~~~~~~~~~~~~~~~~~~~~~~~~~~~

You should only do small testing on the login node, the real job need to
be submitted to the compute nodes using LSF.

-  $
   ``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``
   if you haven't done it during this login
-  $ ``conda activate <your environment>``
-  (your environment)$
   ``python your_testing_code_using_installed_packages.py``
-  $ ``conda deactivate`` when you finish

Submitting jobs using LSF on Triton
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Please read `Scheduling Jobs on
Pegasus <https://acs-docs.readthedocs.io/pegasus/jobs/README.html>`__.

Use ``#BSUB -q normal`` to submit job to queue normal for testing on
Triton now (it will change in the future).

Add ``#BSUB -gpu "num=<number of GPUs>"`` if you need GPUs in your job.
You can use up to 2 GPUs if Distributed Deep Learning (DDL) is not
involved.

A job script example:

::

    #!/bin/bash
    #BSUB -J "MNIST_example"
    #BSUB -o "MNIST_example_%J.out"
    #BSUB -e "MNIST_example_%J.err"
    #BSUB -n 1 
    #BSUB -gpu "num=1"
    #BSUB -q "normal"
    #BSUB -W 00:10

    source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh
    conda activate wml_162_env
    cd /scratch/dl_examples/tensorflow_examples/mnist

    python ./mnist.py --data_dir=${HOME}/temp

If the above file is named mnist\_example.job, then

$ ``bsub < mnist_example.job`` to submit the job.

The output will show in the ``MNIST_example_<job id>.out``\ file after
the job is done.

Installing packages not supported in WML CE
-------------------------------------------

Caveat: you can try to install packages that are not supported in WML CE
from other resources, but you might encounter packages conflicts.

1. ``conda search <package>`` in a conda environment, if you find the
   version you need, you can do ``conda install <package>=<version>`` to
   install it. The system-wise Anaconda has been configured in the way
   that it will first look into the [IBM WML CE repo]
   (https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/),
   then look into the [official repository hosted by Anaconda]
   (https://repo.anaconda.com/pkgs/main/linux-ppc64le/) to find the
   packages for the linux-ppc64le architecture (POWER system).

2. Search in `Anaconda Cloud <https://anaconda.org/>`__ and choose
   Platform ``linux-ppc64le``, it will tell you a specific channel that
   you can use to install the package in your environment.
   ``conda install -c <a specific channel> <package>``

3. Use ``pip install <package>==<version>``

Using DDL (Testing)
-------------------

https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/wmlce_ddltf_tutorial.html
https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/wmlce_ddlpytorch_tutorial.html

A job script example:

::

   #BSUB -L /bin/bash
   #BSUB -J "MNIST_DDL"
   #BSUB -o "MNIST_DDL.%J"
   #BSUB -n 4
   #BSUB -R "span[ptile=2]"
   #BSUB -gpu "num=2"
   #BSUB -q "normal"
   #BSUB -W 00:10

   # Anaconda setup
   CONDA_ROOT=/share/apps/ibm_wml_ce/1.6.2/anaconda3
   source ${CONDA_ROOT}/etc/profile.d/conda.sh
   conda activate wml_162_env
   
   EXAMPLE_DIR=/scratch/dl_examples/tensorflow_examples/mnist

   # Workaround for GPU selection issue
   cat > launch.sh << EoF_l
   #! /bin/sh
   export CUDA_VISIBLE_DEVICES=0,1
   exec \$*
   EoF_l
   chmod +x launch.sh

   # Run the program
   export PAMI_IBV_ADAPTER_AFFINITY=0
   ddlrun \
     ./launch.sh \
     python \
       ${EXAMPLE_DIR}/mnist-env.py \
          --data_dir=${EXAMPLE_DIR}/data

   # Clean up
   /bin/rm -f launch.sh

-  ``#BSUB -n 4`` requests 4 CPU cores 
-  ``#BSUB -R "span[ptile=2]"`` asks for 2 cores per node, so 2 nodes (4 cores / 2 cores per node) will be involved.
-  ``#BSUB -gpu "num=2"`` requests 2 GPUs per node, and therefore 4 GPUs in total (2 GPUs per node * 2 nodes) are requested for this job.

Using LMS (Testing)
-------------------

https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/wmlce_getstarted_tflmsv2.html
https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/wmlce_getstarted_pytorch.html

How system-wise Anaconda was installed and configured
-----------------------------------------------------

Intallation
~~~~~~~~~~~

-  $ ``mkdir -p /share/apps/ibm_wml_ce/1.6.2``
-  $ ``cd /share/apps/ibm_wml_ce/1.6.2``
-  $
   ``wget https://repo.continuum.io/archive/Anaconda3-2019.07-Linux-ppc64le.sh``
-  $ ``bash Anaconda3-2019.07-Linux-ppc64le.sh``
-  Installing at location ``/share/apps/ibm_wml_ce/1.6.2/anaconda3``

Notes:

-  Answering ``no`` to not allow the installer to initialize Anaconda3.
   This is to avoid conflicts with other Anaconda installed.

Configuration
~~~~~~~~~~~~~

-  $
   ``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``
-  $ ``conda config --system --set channel_priority strict``
-  $
   ``conda config --system --add default_channels https://repo.anaconda.com/pkgs/main``
-  $
   ``conda config --system --add default_channels https://repo.anaconda.com/pkgs/r``
-  $
   ``conda config --system --prepend channels https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/``
-  $ ``conda config --system --set auto_activate_base false``

Notes:

-  Using ``--system`` writes to the .condarc file located at
   ``/share/apps/ibm_wml_ce/1.6.2/anaconda3/.condarc`` instead of
   ``/root/.condarc`` to avoid conflicts with other Anconda installed.

Installing all supported packages in one Conda environment
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  $ ``conda create -n wml_162_env python=3.7``
-  $ ``conda activate wml_162_env``
-  (wml\_162\_env)$ ``conda install powerai``

Notes:

-  The environment is created at
   ``/share/apps/ibm_wml_ce/1.6.2/anaconda3/envs``

References and Additional Resources
-----------------------------------

`Watson Machine Learning Community
Edition <https://developer.ibm.com/linuxonpower/deep-learning-powerai/releases/>`__

`IBM Watson Machine Learning Community Edition Version 1.6.2
documentation <https://www.ibm.com/support/knowledgecenter/SS5SF7_1.6.2/navigation/welcome.html>`__

`Deep learning and AI on Power Systems technical
resources <https://developer.ibm.com/linuxonpower/deep-learning-powerai/library/>`__

