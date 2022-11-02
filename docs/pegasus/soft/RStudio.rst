RStudio on Pegasus
============

Rstudio is available as a software module on Pegasus utilizing R version 4.1.0. RStudio graphical jobs can be submitted to 
the LSF scheduler via the interactive queue.


Forwarding X11
-------

In order to launch an RStudio interactive job, you will need to login to Pegasus with X11 forwarding enabled.

You will also need to install an X11 server on your local machine such as Xming for Windows or XQuartz for Mac.

Please see the following guide on how to achieve this: 
https://acs-docs.readthedocs.io/services/1-access.html?highlight=x11#connect-with-x11-forwarding


Loading the Module
-------
The RStudio module is dependent on the gcc/8.3.0 and R/4.1.0 software modules. These will come pre-loaded once the RStudio module has been loaded

::

    [nra20@login4 ~]$ module load rstudio
    [nra20@login4 ~]$ module list
     Currently Loaded Modulefiles:
       1) perl/5.18.1(default)   3) gcc/8.3.0
       2) R/4.1.0                4) rstudio/2022.05.999
       
First Time configurations
-------
If this is the first time you are using the RStudio module you will need to configure the rendering engine to run in software mode by editing /nethome/caneid/.config/RStudio/desktop.ini

::

    [nra20@login4 ~]$ vi /nethome/nra20/.config/RStudio/desktop.ini
    
Add the following line under [General]

    desktop.renderingEngine=software



Launching RStudio jobs through LSF 
-------
To launch RStudio jobs to the LSF scheduler, you will need to pass the X11 **-XF** parameter and submit to the **interactive** queue through the command line. 

::

    [nra20@login4 ~]$ bsub -Is -q interactive -P hpc -XF rstudio
    Job is submitted to <hpc> project.
    Job <27157788> is submitted to queue <interactive>.
    <<ssh X11 forwarding job>>
    <<Waiting for dispatch ...>>
    Warning: Permanently added '10.10.104.5' (ECDSA) to the list of known hosts.
    <<Starting on n131>>

The RStudio graphical interface will then appear, from which you can utilize and install any needed packages. 

More information on submitting graphical interactive jobs: https://acs-docs.readthedocs.io/pegasus/jobs/5-interactive.html

If you run into any issues with package installations, please send an email to hpc@ccs.miami.edu 


