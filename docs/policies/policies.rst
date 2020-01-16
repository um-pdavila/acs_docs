CCS ACS Policies
================

CCS Advanced Computing Services resources are available to all University of Miami employees and students. Use of CCS resources is governed by `University of Miami Acceptable Use Policies <http://it.miami.edu/about-umit/policies-and-procedures/>`_ in addition to CCS ACS policies, terms, and conditions.


Accounts
--------

- To qualify for a CCS account, you must be affiliated with the University of Miami.
- All CCS accounts must be linked with a valid corresponding University of Miami account.
- Suspended accounts cannot submit jobs to the Pegasus cluster. 
- Suspended accounts will be disabled after 90 days.
- Disabled accounts cannot log into the Pegasus cluster.
- Disabled account data will be deleted after 30 days.

CCS Portal Links
----------------

- `CCS Account Registration <https://portal.ccs.miami.edu/accounts/new_account/>`_
- `CCS Project Request <https://portal.ccs.miami.edu/accounts/new/group/>`_
- `CCS Software Request <https://portal.ccs.miami.edu/resources/soft/new>`_

Pegasus Supercomputer
---------------------

- All users of the Pegasus supercomputer are required to have a CCS account.
- All SSH sessions are closed automatically after 30 minutes of inactivity.
- No backups are performed on Pegasus file systems.
- CCS does not alter user files.
- Jobs running on the Pegasus cluster may be terminated for:
  
  - using excessive resources or exceeding 30 minutes of CPU time on Pegasus login nodes
  - failing to reserve appropriate LSF resources
  - backgrounding LSF processes with the & operator
  - running on inappropriate LSF queues
  - running from data on ``/nethome``
    
  The CCS account responsible for those jobs may be suspended.

- Pegasus users with disabled CCS accounts must submit a request to `hpc@ccs.miami.edu <mailto:hpc@ccs.miami.edu>`_ for temporary account reactivation.


Allocations
-----------

- Active Pegasus users are allocated a logical **home** directory area ``/nethome/username``, limited to 250GB.
- Active projects can be allocated scratch directories:  ``/scratch/projects/projectID``, intended for compiles and run-time input & output files. 
- Disk allocations on Pegasus are only for data currently being processed.
- Data for running jobs must be staged exclusively in the ``/scratch`` file system. CCS accounts staging job data in the ``/nethome`` filesystem may be suspended.
- Both **home** and **scratch** are available on all nodes in the Pegasus cluster.
- Accounts exceeding the 250GB home limit will be suspended. Once usage is under 250GB, the account will be enabled in one business day.

Software
--------

- Users are free to install software in their home directories on Pegasus. More information about installing software onto ACS systems on `ReadTheDocs <https://acs-docs.readthedocs.io/>`_ : `https://acs-docs.readthedocs.io/ <https://acs-docs.readthedocs.io/>`_
- Pegasus software requests are reviewed quarterly. Global software packages are considered only when a minimum of 20 users require them.
