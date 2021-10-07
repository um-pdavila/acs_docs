Triton LSF Job Scripts
=======================

The command ``bsub < ScriptFile`` will submit the given script for
processing. Your script must contain the information LSF needs to
allocate the resources your job requires, handle standard I/O streams,
and run the job. For more information about flags, type ``bsub -h`` or
``man bsub`` at the Triton prompt. Example scripts and descriptions are
below.

You must be a member of a project to submit jobs to it. See
:ref:`Projects <projects>` for more information.

On submission, LSF will return the ``jobID`` which can be used to track
your job.

::

    [username@triton ~]$ bsub < test.job
    Job <4225> is submitted to the default queue <normal>.

Example script for a serial Job
-------------------------------

``test.job``

--------------

.. code:: bash

    #!/bin/bash
    #BSUB -J myserialjob
    #BSUB -P myproject
    #BSUB -o %J.out
    #BSUB -e %J.err
    #BSUB -W 1:00
    #BSUB -q normal
    #BSUB -n 1
    #BSUB -R "rusage[mem=128M]"
    #BSUB -B
    #BSUB -N
    #BSUB -u myemail@miami.edu
    #
    # Run serial executable on 1 cpu of one node
    cd /path/to/scratch/directory
    ./test.x a b c

Here is a detailed line-by-line breakdown of the keywords and their
assigned values listed in this script:

``ScriptFile_keywords``

--------------

.. code:: bash

    #!/bin/bash
    specifies the shell to be used when executing the command portion of the script.
    The default is Bash shell.

    BSUB -J serialjob
    assign a name to job. The name of the job will show in the bjobs output.

    #BSUB -P myproject
    specify the project to use when submitting the job. This is required when a user has more than one project on Triton.

    #BSUB -e %J.err
    redirect std error to a specified file

    #BSUB -W 1:00
    set wall clock run time limit of 1 hour, otherwise queue specific default run time limit will be applied.

    #BSUB -q normal
    specify queue to be used. Without this option, default 'normal' queue will be applied.

    #BSUB -n 1
    specify number of processors. In this job, a single processor is requested.

    #BSUB -R "rusage[mem=128M]"
    specify that this job requests 128 megabytes of RAM. You can use other units (K(kilobytes), M(megabytes), G(gigabytes), T(terabytes)).
    
    #BSUB -B
    send mail to specified email when the job is dispatched and begins execution.

    #BSUB -u example@miami.edu
    send notification through email to example@miami.edu.

    #BSUB -N
    send job statistics report through email when job finishes.

Example scripts for parallel jobs
---------------------------------

We recommend using IBM Advance Toolchain and SMPI unless you have specific reason for using OpenMP or OpenMPI. IBM's SMPI scales better and has better performance than both OpenMP or OpenMPI on Triton.

For optimum performance, use the ``#BSUB -R "span[ptile=40]"``. This requires the LSF job scheduler to allocate 40 processors per host, ensuring all processors on a single host are used by that job.

**Reserve enough memory for your jobs.** Memory reservations are per core. Parallel job performance may be affected, or even interrupted, by other badly-configured jobs running on the same host.


``mpi_hello_world.job``

--------------

.. code:: bash

    $ cat mpi_hello_world.job
    #!/bin/sh
    #BSUB -n 80
    #BSUB -J mpi_hello_world
    #BSUB -o logs/%J.out
    #BSUB -e logs/%J.err
    #BSUB -a openmpi
    #BSUB -R "span[ptile=4]"
    #BSUB -q normal

    # Use gcc/8.3.1 and openmpi/4.0.5
    # ml gcc/8.3.1 openmpi/4.0.5
    
    # Use the optimized IBM Advance Toolkit (gcc 8.3.1) and smpi
    ml at smpi

    echo "Testing the gcc/8.3.1 openmpi/4.0.5 module: \n" >> mpi_hello_world.log

    mpirun -n 80 ./mpi_hello_world >> logs/mpi_hello_world.log


``mpi_hello_world.c``

--------------

.. code:: bash

  $ cat mpi_hello_world.c
  #include <mpi.h>
  #include <stdio.h>

  int main(int argc, char** argv) {
    // Initialize the MPI environment
    MPI_Init(NULL, NULL);

    // Get the number of processes
    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size);

    // Get the rank of the process
    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank);

    // Get the name of the processor
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len);

    // Print off a hello world message
    printf("Hello world from processor %s, rank %d out of %d processors\n",
           processor_name, world_rank, world_size);

    // Finalize the MPI environment.
    MPI_Finalize();
  }



``Compile mpi_hello_world.c``

--------------

.. code:: bash

  $ ml gcc/8.3.1
  $ ml openmpi/4.0.5
  $ mpicc -o mpi_hello_world mpi_hello_world.c
  
  
``Run mpi_hello_world.job``

--------------

.. code:: bash

  $ bsub < mpi_hello_world.job 
  Job <981431> is submitted to queue <normal>.


``Get mpi_hello_world.job status``

--------------

.. code:: bash

  $ bjobs -l 981431
  
  Job <981431>, Job Name <openmpi_test>, User <pdavila>, Project <default>, Status <DONE> 
  ...                   

Thu Oct  7 11:25:07: Done successfully. The CPU time used is 9.7 seconds.
                     HOST: t088; CPU_TIME: 0 seconds
                     HOST: t061; CPU_TIME: 0 seconds
                     HOST: t042; CPU_TIME: 0 seconds
                     HOST: t052; CPU_TIME: 0 seconds
                     HOST: t029; CPU_TIME: 0 seconds
                     HOST: t077; CPU_TIME: 1 seconds
                     HOST: t072; CPU_TIME: 0 seconds
                     HOST: t058; CPU_TIME: 0 seconds
                     HOST: t039; CPU_TIME: 0 seconds
                     HOST: t041; CPU_TIME: 0 seconds
                     HOST: t065; CPU_TIME: 0 seconds
                     HOST: t036; CPU_TIME: 1 seconds
                     HOST: t087; CPU_TIME: 0 seconds
                     HOST: t048; CPU_TIME: 0 seconds
                     HOST: t081; CPU_TIME: 0 seconds
                     HOST: t054; CPU_TIME: 0 seconds
                     HOST: t073; CPU_TIME: 1 seconds
                     HOST: t070; CPU_TIME: 0 seconds
                     HOST: t083; CPU_TIME: 1 seconds
                     HOST: t047.triton; CPU_TIME: 0 seconds

   MEMORY USAGE:
   MAX MEM: 14 Mbytes;  AVG MEM: 9 Mbytes
   ...

--------------

.. code:: bash
  
  $ cat logs/981431.out
  Sender: LSF System <hpc@ccs.miami.edu>
  Subject: Job 981431: <openmpi_test> in cluster <triton> Done
  
  Job <openmpi_test> was submitted from host <login1> by user <pdavila> in cluster <triton> at Thu Oct  7 11:25:03 2021
  Job was executed on host(s) <4*t047>, in queue <normal>, as user <pdavila> in cluster <triton> at Thu Oct  7 11:25:03 2021
                              <4*t083>
                              <4*t087>
                              <4*t036>
                              <4*t065>
                              <4*t081>
                              <4*t054>
                              <4*t061>
                              <4*t029>
                              <4*t039>
                              <4*t088>
                              <4*t052>
                              <4*t070>
                              <4*t072>
                              <4*t073>
                              <4*t042>
                              <4*t058>
                              <4*t077>
                              <4*t048>
                              <4*t041>
  ...
  
  Your job looked like:
  
  ------------------------------------------------------------
  # LSBATCH: User input
  #!/bin/sh
  #BSUB -n 80
  #BSUB -J openmpi_test
  #BSUB -o logs/%J.out
  #BSUB -e logs/%J.err
  #BSUB -a openmpi
  #BSUB -R "span[ptile=4]"
  #BSUB -q normal
  
  # Use openmpi
  # ml gcc/8.3.1 openmpi/4.0.5

  # Use the optimized IBM Advance Toolkit (gcc 8.3.1) and smpi
  ml at smpi
  
  echo "Testing the gcc/8.3.1 openmpi/4.0.5 module: \n" >> logs/mpi_hello_world.log
  
  mpirun -n 80 ./mpi_hello_world >> logs/mpi_hello_world.log
  
  ------------------------------------------------------------
  
  Successfully completed.
  
  Resource usage summary:
  
    CPU time :                                   9.71 sec.
    Max Memory :                                 17 MB
    Average Memory :                             11.00 MB
    Total Requested Memory :                     -
    Delta Memory :                               -
    Max Swap :                                   -
    Max Processes :                              5
    Max Threads :                                9
    Run time :                                   4 sec.
    Turnaround time :                            5 sec.

  The output (if any) follows:

  PS:

  Read file <logs/981431.err> for stderr output of this job.
