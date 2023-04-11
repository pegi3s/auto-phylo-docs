What is auto-phylo?
*******************

**auto-phylo** is a pipeline maker software for phylogenetic studies. A Docker image is available at `this Docker Hub repository <https://hub.docker.com/r/pegi3s/auto-phylo>`_.

In order to run auto-phylo, Docker must be installed in a Linux system. 

How to run auto-phylo
*********************

To run **auto-phylo**, you should adapt and run the following command: 

.. code-block:: shell-session

   docker run --rm -v /your/data/dir:/data -v /var/run/docker.sock:/var/run/docker.sock pegi3s/auto-phylo

In this command, you should replace ``/your/data/dir`` to point to the directory that contains the input directory with the files that you want to analyze, as well as the pipeline and config files:

- In the pipeline file you must specify the auto-phylo modules to be invoked as well as the input and output directory names (one per line). 
- In the config file you must declare the path to the working directory as well as the SEDA version to be used, as well as any other parameters that are required by the modules being used.
