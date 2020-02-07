Pegasus FAQs - Frequently Asked Questions
=========================================

Detailed information for FAQ topics is available here and in our `ACS
Policies <https://ccs.miami.edu/ac/policies>`__ webpage.

If you are new to Pegasus and HPC clusters, review this documentation on
the Pegasus system, the job scheduler, and modularized software. 

.. note :: CCS ACS does not install, provide support for, or provide documentation on how to code in your preferred software. ACS documentation contains information on using software in a Linux cluster environment.


Pegasus Projects
----------------

:ref:`Projects on Pegasus <projects>`

How do I join a project?
~~~~~~~~~~~~~~~~~~~~~~~~

Contact the project owner. Details can be found on the CCS Portal:
https://portal.ccs.miami.edu/forms-access/

How do I request a new project?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Any PI or faculty member may request a new project via the CCS Portal:
https://portal.ccs.miami.edu/accounts/new/group/

When will my project be created?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When the allocations committee has reviewed and approved it. Check your
request status via the CCS Portal under My Pegasus -> My Requests.

Scratch requests over 2TB can take a month for the allocations committee
to review as availability is limited.

How do projects work?
~~~~~~~~~~~~~~~~~~~~~

:ref:`Projects on Pegasus <projects>`, `CCS Portal
Projects <https://portal.ccs.miami.edu/forms-access/>`__

How can I manage my Projects and Groups?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Manage owned Projects and Groups via the CCS Portal:
https://portal.ccs.miami.edu

Click on My Pegasus -> My Projects or My Groups

See `CCS Portal Projects <https://portal.ccs.miami.edu/forms-access/>`__
for more information.

Pegasus Software
----------------

:ref:`Software on Pegasus <p-soft>`

What software is available?
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Software Modules list on the CCS Portal:
https://portal.ccs.miami.edu/resources/software/

Software Modules from the command line: ``$ module avail``

How do I view my currently loaded modules?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

``$ module list``

How do I use software modules?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

:ref:`Software on Pegasus <p-soft>`

May I install software?
~~~~~~~~~~~~~~~~~~~~~~~

Yes! Pegasus users are free to compile and install software in their
respective home directories by following the software’s source code or
local installation instructions. See our :ref:`Software
Installation <soft-install>` guide for more information.


.. note :: CCS ACS does not install user software. For global installations on Pegasus, submit a Software Request via the CCS Portal (below).


How do I request global software installation on Pegasus?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Request new global software via the CCS Portal:
https://portal.ccs.miami.edu/resources/soft/new

We only globally install software when we receive multiple requests for
the software.

When will my global software request be approved/installed?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

When a minimum of 20 users require it, software requests will be
approved. Software requests are reviewed and installed quarterly.

How can I increase Java memory on Pegasus?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Load the java module, then change the value of \_JAVA_OPTIONS.

::

    [username@pegasus ~]$ module load java
    [username@pegasus ~]$ echo $_JAVA_OPTIONS
    -Xmx512m
    [username@pegasus ~]$ export _JAVA_OPTIONS="-Xmx4g"

Pegasus Job Scheduling
----------------------

:ref:`Scheduling Jobs <p-jobs>`

May I run resource-intensive jobs on Pegasus login nodes?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No. Resource-intensive jobs must be submitted to LSF.

How do I submit jobs to Pegasus?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With ``bsub`` :ref:`command <lsf-commands>` : :ref:`LSF <p-jobs>`

How do I check on my submitted jobs?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With ``bjobs`` :ref:`command <lsf-commands>` : :ref:`LSF <p-jobs>`

How do I monitor job progress?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With ``bpeek`` :ref:`command <lsf-commands>` : :ref:`LSF <p-jobs>`

Is there a limit on how many jobs I can run?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No. Users are limited by number of simultaneous CPUs used. Individual
users can run on up to 512 CPUs at a time, projects on up to 1000 CPUs
at a time.

How can I see pending and running job counts for Pegasus queues?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With ``bqueues`` :ref:`command <lsf-commands>` : :ref:`LSF <p-jobs>`

Why is my job still pending?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Jobs wait for enough resources to satisfy requirements. When the cluster
is under heavy user load, jobs will wait longer. Use
``$ bjobs -l jobID`` to see PENDING REASONS. Check your resource
requirements for accuracy and feasibility.

The Pegasus job scheduler operates under Fairshare scheduling. Fairshare
scheduling divides the processing power of the cluster among users and
queues to provide fair access to resources, so that no user or queue can
monopolize the resources of the cluster and no queue will be starved.

If your job has been pending for more than 24 hours *and is not
requesting exclusive access or all cores on a node*, you may e-mail
`hpc@ccs.miami.edu <mailto:hpc@ccs.mami.edu>`__ for assistance.

Are other users’ pending jobs slowing my job?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

No. The number of pending jobs is irrelevant to job performance in LSF.
The scheduler can handle hundreds of thousands of jobs.

How do I submit jobs to my Project?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With the ``-P`` flag : :ref:`LSF jobs <p-jobs>`

How do I submit an interactive job?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With the ``-Is -q interactive`` flags : :ref:`LSF interactive jobs <p-interactive>`

How do I submit an interactive X11 job?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

With the ``-Is -q interactive -XF`` flags : :ref:`LSF interactive jobs <p-interactive>`

Why was my job killed?
~~~~~~~~~~~~~~~~~~~~~~

Jobs are killed to protect the cluster and preserve system performance.

Common reasons include:

-  running on a login node
-  using more memory than reserved
-  using all the memory on a compute node
-  using more CPUs than reserved
-  needing more time to complete than reserved
-  using more ``/tmp`` space than available on compute nodes

See :ref:`LSF <p-jobs>` for assistance with appropriate resource
reservations and :ref:`Pegasus Queues <p-queues>` for default wall
times.


What about jobs in UNKWN state?
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Re-queue your job in LSF : 

| ``$ bkill -r jobID`` 
| ``$ bkill -r jobID``   (a second time) 
| ``$ brequeue -e jobID``

