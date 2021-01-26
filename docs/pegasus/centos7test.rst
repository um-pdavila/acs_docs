Testing Centos 7 on Pegasus
===========================

On Feb 12th at 5pm Pegasus compute nodes in the parallel,  general and bigmem queues will be updated to Centos 7.

We encourage you to test your applications on Centos 7 prior to the update.

On Pegasus, a queue named 'Centos7' has been created.  You may submit jobs to this queue for the purpose of testing and validation on Centos7 prior to the scheduled upgrade.

.. important:: As a courtesy to others, please do not run jobs for more than 24 hours or use more than 64 cores in the Centos7 queue. 
.. important:: You must be sure to remove the share-rpms65 module from your .bashrc or .cshrc prior to login on the Centos7 headnode.

To submit jobs to the Centos7 queue you must first login to pegasus as usual:

.. code-block:: bash

    % ssh ccsuserid@pegasus.ccs.miami.edu

Then connect to the new head node:

.. code-block:: bash

    % ssh centos7test 
    
Here,  you can submit jobs to Centos7 test queue:

.. code-block:: bash

   -bash-4.2$ bsub -q Centos7 -P myprojectname -Is /bin/bash

Please contact us at hpc@ccs.miami.edu to report any problems.
