.. _transfer: 

Transferring Files
==================

IDSC systems support multiple file transfer programs such as FileZilla and
PSFTP, and common command line utilities such as ``scp`` and ``rsync``.
Use cluster head nodes (login nodes) for these types of file transfers.
For transferring large amounts of data from systems outside the
University of Miami, IDSC ACS also offers a gateway server that supports
SFTP and Globus.

Using command line utilities
----------------------------

Use ``cp`` to copy files within the same computation system. Use
``scp``, ``sftp``, or ``rsync`` to transfer files between computational
systems (e.g., scratch space to Visx project space). When executing
multiple instantiations of command line utilities like rsync and scp,
please ***limit your transfers to no more than 2-3 processes at a
time.***

scp
~~~

An example transfer might look like this:

::

    [localmachine: ~]$ scp /local/filename \
                username@pegasus.ccs.miami.edu:/scratch/projectID/directory

To transfer a directory, use the ``-r`` flag (recursive):

::

    [localmachine: ~]$ scp -r /local/directory \
                username@pegasus.ccs.miami.edu:/scratch/projectID/directory

Consult the Linux man pages for more information on scp.

rsync
~~~~~

The rsync command is another way to keep data current. In contrast to
scp, rsync transfers only the changed parts of a file (instead of
transferring the entire file). Hence, this selective method of data
transfer can be much more efficient than scp. The following example
demonstrates usage of the rsync command for transferring a file named
"firstExample.c" from the current location to a location on Pegasus.

::

    [localmachine: ~]$ rsync firstExample.c \
                username@pegasus.ccs.miami.edu:/scratch/projectID/directory

An entire directory can be transferred from source to destination by
using rsync. For directory transfers, the options ``-atvr`` will
transfer the files recursively (``-r`` option) along with the
modification times (``-t`` option) and in the archive mode (``-a``
option). Consult the Linux man pages for more information on rsync.

Using FileZilla
---------------

FileZilla is a free, user friendly, open source, cross-platform FTP,
SFTP and FTPS application.

Download the FileZilla client here:
https://filezilla-project.org/download.php?show_all=1 and follow the
installation instructions for the appropriate platform
(http://wiki.filezilla-project.org/Client_Installation).

Launch FileZilla and open **File : Site Manager**.

Click the "New Site" button and name the entry.  Pegasus example::

    Host:       pegasus.ccs.miami.edu  or triton.ccs.miami.edu
    Protocol:   SFTP
    Logon Type: Normal
    enter your username and password

Selecting Logon Type: **Ask for password** will prompt for a password
each connection.\ |FileZilla Site Manager|

Click the "Connect" button. Once connected, drag and drop files or
directories between your local machine and the server.

Using the gateway server
------------------------

To transfer large amounts of data from systems outside the University of
Miami, use the gateway server. This server supports SFTP file
transfers. Users ***must be a member of a project*** to request access
to the gateway server. E-mail hpc@ccs.miami.edu to request access.

SFTP
~~~~

::

    Host:  xfer.ccs.miami.edu
    protocol:  SFTP
    user:    caneid
    pw:  [UM caneid passwd]  
    Folder: download/<projectname>

Open an SFTP session to the gateway server using your IDSC account
credentials: ``xfer.ccs.miami.edu``

::

    [localmachine: ~]$ sftp username@xfer.ccs.miami.edu
    sftp> cd download
    sftp> mkdir <project>
    sftp> cd project
    sftp> put newfile


.. |FileZilla Site Manager| image:: assets/fz_sm1.png

