JupyterHub on Triton User Menu
==============================
In this document

-  the dollar sign ($) indicates the ``text`` follows it is a
   command-line interface (CLI) command that you need to type in.
-  the angle brackets (< >) indicates the enclosed element is mandatory
   that needs to be replaced with the user-dependent information.

Introduction
------------

`JupyterHub <https://jupyterhub.readthedocs.io/en/stable/index.html>`__
provides Jupyter Notebook for multiple users.

Through JupyterHub on Triton, you can request and start a Jupyter
Notebook server on one of Triton's compute nodes (via the `IBM Platform
LSF <https://www.ibm.com/support/knowledgecenter/en/SSWRJV_10.1.0/lsf_welcome/lsf_welcome.html>`__
job scheduler on the back-end). In this way, you can interactively test
your Python or R programs through the Notebook with the supercomputer
resources.

Currently all requested Notebook servers are running in only one compute
node. It is recommended to use the Notebook as a testing tool for the
sample code and submit LSF jobs for big programs.

Using JupyterHub on Triton
--------------------------

Login
~~~~~

-  First you need to have access to Triton. (please check the `CCS AC Policies <https://ccs.miami.edu/ac/policies/>`__)
-  Connect with the UM network on campus or via
   `VPN <https://www.it.miami.edu/a-z-listing/virtual-private-network/index.html>`__.
-  Open the Login page https://jupyter.ccs.miami.edu:8000 on your
   browser.
-  Log in using your UM CaneID and the associated password.

Starting your Jupyter Notebook server
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Press the ``Start My Notebook Server`` button to launch the resource
   request page.
-  Choose the memory, number of CPU cores, time you want to run the
   Notebook server and whether or not you want to use a GPU.
-  Press the ``Request`` button to request and start a Notebook server.
   (It takes time to locate the resources and start the notebook server,
   so please be patient.)

Logout ( **IMPORTANT** )
~~~~~~~~~~~~~~~~~~~~~~~~

-  When using the JupyterHub, you need to be clear that there are three
   things you are dealing with:

   -  the hub
   -  the notebook server
   -  the individual notebooks (including the notebook files and the
      kernels)

-  The correct logout order should be:

   1. After saving the files, shutdown all the individual notebooks by
      pressing ``File`` in the menu bar and choosing ``Close and Halt``.
   2. Stop your notebook server by clicking the ``Control Panel`` button
      at the top-right corner and pressing ``Stop My Notebook Server``.
      (**IMPORTANT STEP**)
   3. Logout from the hub by clicking the ``Logout from JupyterHub``
      button at the top-right corner.

Using Jupyter Notebook
----------------------

After the notebook server starts, you will see the interface page
showing your home directory.

You can create notebook files, text files and folders, or open terminals
using the ``New`` button at the top-right corner under the menu bar.

Details can be found at the official `Jupyter Notebook User
Documentation <https://jupyter-notebook.readthedocs.io/en/stable/notebook.html>`__.

Using System-wise Kernels
~~~~~~~~~~~~~~~~~~~~~~~~~

The system-wise kernels installed by the system administrators contain
common packages. You can use them to test your code if you do not need
additional packages. On the Notebook Dashboard page, you can create a
new notebook file (.ipynb) with a selected kernel by clicking on the
``New`` button at the top-right corner under the menu bar. On the
Notebook Editor page, you can change kernel by clicking ``Kernel`` in
the menubar and choosing ``Change kernel``.

-  Anaconda2 Base (Python 2.7) and Anaconda3 Base (Python 3.7) kernels are the Anaconda base environments. Each of them has over 150 packages automatically installed. You can check the packages using the following commands after you login to Triton via SSH ($ ``ssh <caneid>@triton.ccs.miami.edu``).

   - For Anaconda2, $ ``source /share/apps/anaconda2/2019.10/etc/profile.d/conda.sh``
   - For Anaconda3, $ ``source /share/apps/anaconda3/2019.10/etc/profile.d/conda.sh`` 
   - $ ``conda activate base``
   - $ ``conda list``

-  Deep Learning (IBM WML CE v1.6.1) and Deep Learning (IBM WML CE
   v1.6.2) kernels The Deep Learning kernel has the `IBM Watson Machine
   Learning Community Edition
   packages <https://public.dhe.ibm.com/ibmdl/export/pub/software/server/ibm-ai/conda/#/>`__.
   (You can find the included packages for v1.6.1 or v1.6.2 by changing
   the ``Releases`` version in the ``Filters`` bar.)

   -  IBM WML CE v1.6.1 kernel is located at
      ``/share/apps/ibm_wml_ce/1.6.1/anaconda3/envs/wml_ce_env``
   -  IBM WML CE v1.6.w kernel is located at
      ``/share/apps/ibm_wml_ce/1.6.2/anaconda3/envs/wml_162_env``

-  R and 'R for RStudio' kernels The R kernel includes the `R Base
   Package <https://stat.ethz.ch/R-manual/R-devel/library/base/html/base-package.html>`__.
   The 'R for RStudio' kernel is compiled on Triton from source, and it
   is used for the RStudio on Triton. Both of them are version 3.6.1.

   -  R kernel is located at
      ``/share/apps/anaconda3/2019.07/envs/r_env``
   -  R for RStudio kernel is located at ``/share/apps/R/R361_static``

If you cannot find the packages you need through the system-wise
kernels, you can create your own kernels.

Creating Your Own IPython Kernel
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  $ ``ssh <caneid>@triton.ccs.miami.edu`` to login to Triton
-  $ If you do not need deep learning packages, do
   ``source /share/apps/anaconda3/2019.07/etc/profile.d/conda.sh``,
   otherwise use the other Anaconda specified for installing deep
   learning packages
   ``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``
   (see `IBM WML CE on Triton User
   Menu <https://acs-docs.readthedocs.io/triton/2-wmlce.html#installing-wml-ce-packages>`__)
-  $ ``conda create -n <your environment> python=<version>`` to create
   an environment at ``~/.conda/envs/``
-  $ ``conda activate <your environment>``
-  (your environment)$ ``conda install ipykernel`` to install the
   IPython kernel package
-  (your environment)$
   ``ipython kernel install --user --name <kernel name> --display-name "<the displayed name for the kernel>"``

Here is an example:

(Please press ``y`` on your keyboard when you see ``Proceed ([y]/n)?``)

::

    $ source /share/apps/anaconda3/2019.07/etc/profile.d/conda.sh
    $ conda create -n myenv python=3.6
    $ conda activate myenv
    (myenv)$ conda install ipykernel
    (myenv)$ ipython kernel install --user --name my_py36_kernel --display-name "My Python 3.6"

After these steps, every time you want to install a package for the
kernel, you can do:

-  $ ``source /share/apps/anaconda3/2019.07/etc/profile.d/conda.sh`` or
   for the deep learning packages
   ``source /share/apps/ibm_wml_ce/1.6.2/anaconda3/etc/profile.d/conda.sh``
   (if you haven't done it in the current login)
-  $ ``conda activate <environment>`` (if you haven't activated the
   environment)
-  $ ``conda install <package>``

If the package could not be found, you can search `Anaconda
Cloud <https://anaconda.org/>`__ and choose Platform ``linux-ppc64le``
(**IMPORTANT**). If the package exists, you can click on the entry and
follow the instructions. It is probably provided by a specific channel
and you do ``conda install -c <the specific channel> <package>`` to
intall it.

If Anaconda Cloud does not have the package neither, you can try
``pip install``. We found the default higher version openssl package
might cause some problem when using ``pip install``. You can downgrade
it to version 1.1.1c (``conda install openssl=1.1.1c``) to avoid the
issue.

After the package is installed, you can use it in your notebook by
typing and running ``import <package name>`` in a code cell.

Creating Your Own R kernel
~~~~~~~~~~~~~~~~~~~~~~~~~~

(While installing Python packages, press ``y`` on your keyboard when you
see ``Proceed ([y]/n)?``) (While installing R packages inside R, you can
type ``58``\ or any USA mirror when you are asked to select a CRAN
mirror.)

-  $ ``source /share/apps/anaconda3/2019.07/etc/profile.d/conda.sh`` (if
   you haven't done it in the current login).
-  $
   ``conda create -n <your r environemnt> -c powerai -c conda-forge r-base=3.6.1``
-  $ ``conda activate <your r environemnt>``
-  $
   ``ln -s /share/apps/jupyterhub/0.9.6/bin/jupyter ~/.conda/envs/<your r environemnt>/bin/jupyter``
-  (<your r environemnt>)$ ``cd /share/src_bins/R/dependencies``
-  (<your r environemnt>)$ ``R CMD INSTALL pbdZMQ_0.3-3.tar.gz``
-  (<your r environemnt>)$ ``R CMD INSTALL curl_4.0.tar.gz``
-  (<your r environemnt>)$ ``R``
-  (inside R) > ``install.packages(c('repr', 'IRdisplay', 'IRkernel'))``
-  (inside R) >
   ``IRkernel::installspec(name='<your r kernel name>', displayname = '<display name of your kernel>')``

After these steps, every time you want to install a R package for the
kernel, you can do:

-  $ ``source /share/apps/anaconda3/2019.07/etc/profile.d/conda.sh`` (if
   you haven't done it in the current login)
-  $ ``conda activate <your r environment>`` (if you haven't activated
   the environment)
-  (<your r environemnt>)$ ``R``
-  (inside R) > ``install.packages('<package name>')`` (the pacakge will
   be installed at /~/.conda/envs//lib/R/library by default)

Then you can use the package in your notebook by typing and running
``library('<package name>')`` in a code cell.


