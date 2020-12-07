R Package installations on Triton 
==============================

Introduction
------------
Currentlly some R packages may require aditional steps for installation while others can be installed with a simple
install.packages('nameOfPackage') command within R. 


Installing readr/tidyverse Packages
-----------------------------------
-  Create a .R directory within your home on Triton: $ ``mkdir .R``
-  Move into your new .R directory and open a new file called Makevars: $ ``vi .R/Makevars``
-  Include the following lines within your Makevars file to set the specified C-flags and C-compiler to C99 mode:

    ``CC = gcc -std=c99``

    ``CFLAGS += -D_BSD_SOURCE -D_POSIX_C_SOURCE=200809L``
-  Save and quit, go back to your home directory and open a new .Rprofile file: $ ``vi .Rprofile``
-  Include your library path in the .Rprofile: 

    ``.libPaths("/home/yourCaneID/.R_Library")``
-  Save and quit, then login to rStudio or load & open the R module on your terminal: 
    rStudio: http://triton.ccs.miami.edu:8787/auth-sign-in

    R module: 

    $ ``ml R``

    $ ``R``

-  You can now install readr/tidyverse packages with the following commands:

    ``install.packages("readr", dependencies=TRUE, INSTALL_opts = c('--no-lock'))``

    ``install.packages("tidyverse")``

-  Check that the R packages have been installed:

    ``library(readr)`` 

    ``library(tidyverse)``
