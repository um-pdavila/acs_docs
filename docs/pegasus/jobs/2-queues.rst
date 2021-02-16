.. _p-queues:

Pegasus Job Queues
==================

Pegasus queues are organized using limits like job size, job length, job
purpose, and project. In general, users run jobs on Pegasus with equal
resource shares. Current or recent resource usage lowers the priority
applied when LSF assigns resources for new jobs from a user’s account.

Parallel jobs are more difficult to schedule as they are inherently
larger. Serial jobs can “fit into” the gaps left by larger jobs if
serial jobs use short enough run time limits and small enough numbers of
processors.

The **parallel** queue is available for jobs requiring 16 or more cores.
Submitting jobs to this queue ***requires*** resource distribution
``-R "span[ptile=16]".``

The **bigmem** queue is available for jobs requiring nodes with expanded
memory. Submitting jobs to this queue requires project membership. Do
not submit jobs that can run on the general and parallel queues to the
bigmem queue. 

.. warning:: Jobs using less than 1.5G of memory per core on the bigmem queue are in violation of acceptable use policies and the IDSC account responsible for those jobs may be suspended (:ref:`Policies <policies>`).

We are planning to perform a system upgrade on the Pegasus cluster to CentOS 7 on **Feb 12th, 2021** at 5pm.

It is important that you test your software under CentOS 7 prior to the upgrade on Feb 12th, to ensure compatibility in the new environment. You will find instruction for testing on CentOS 7 here : :ref:`Pegasus CentOS 7 test queue <centos7test>`

.. role:: raw-html(raw)
    :format: html

.. list-table:: Pegasus Job Queues  
   :header-rows: 1
   
   * - Queue Name
     - Processors (Cores)  
     - Memory
     - Wall time default \/ max 
     - Description 
   * - general 
     - 15- 
     - 25GB max 
     - 1 day \/ 7 days 
     - jobs up to 15 cores, up to 25GB memory 
   * - parallel 
     - 16+ 
     - 25GB max 
     - 1 day \/ 7 days 
     - parallel jobs requiring 16 or more cores, up to 25GB memory. :raw-html:`<br />` **requires resource distribution -R "span[ptile=16]"**
   * - bigmem 
     - 64 max 
     - 250GB max 
     - 4 hours \/ 5 days 
     - jobs requiring nodes with expanded memory 
   * - debug 
     - 64 max 
     - 25GB max 
     - 30 mins \/ 30 mins 
     - job debugging 
   * - interactive 
     - 15- 
     - 250GB max 
     - 6 hours \/ 1 day 
     - interactive jobs :raw-html:`<br />` only max 1 job per user
   * - gpu 
     - xx
     - 320 max 
     - 1 day \/ 7 days 
     - gpu debugging restricted queue 
   * - phi 
     - xx
     - 320 max 
     - 1 day \/ 7 days 
     - phi debugging restricted queue 


