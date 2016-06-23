.. bashSTScI documentation master file, created by
   sphinx-quickstart on Mon Jun  6 17:35:21 2016.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Anaconda at STScI - A Walkthrough
=================================
`Anaconda <https://www.continuum.io/downloads>`_ is a distribution platform that uses the Python programming language.  The Anaconda Python distribution uses the Conda package manager to keep track of a user's Python libraries and secondary software packages in a very automated way.  The user is able to interact at the top level with the Conda package manager, and all installs and environment setup is controlled by Conda. Anaconda has been widely adopted by the Python community, and provides easy access to many of the most popular scientific Python packages (`Numpy <http://www.numpy.org/>`_, `Astropy <http://www.astropy.org/index.html>`_, `SciPy <https://www.scipy.org/>`_, etc).

For these reasons, among others, SSB has chosen to change the way we will be distributing STScI software packages and tools.  This new STScI Conda package is called Astroconda, and in order to install these packages the user must install the Anaconda Python distribution platform.  Here you will find a guide for how to install Anaconda and the Astroconda package on STScI machines.  We will go over the following steps:

1. Set up your ``bash`` shell (not always straightforward on STScI machines)
2. Install Anaconda
3. Add the STScI Conda channel
4. Install the STScI Conda software
5. Activate/test the new installation



###############
Note about bash
###############

Anaconda requires the ``bash`` shell. If you have no shell preference, we highly recommend switching over to ``bash`` as your default shell.  The institute sets up your default shell as ``tcsh`` (this will most likely change in the future).  This means that when you start up a terminal you are automatically put into a ``tcsh`` terminal.  

You can temporarily switch to the ``bash`` shell by typing in ``bash`` or ``bash -l``.  We will come back to this later in the guide.  While it is an option to temporarily switch to the ``bash`` shell whenever you want to use Anaconda, this option is much more inefficient and error prone, so once again, we recommend switching over to ``bash`` as your default unless you have extenuating circumstances.  You should never run ``anaconda`` from a ``tcsh`` terminal.  **Anaconda is designed to run in the ``bash`` shell only.**  You will find directions for both options in this guide.


####################
Note For Linux Users
####################

There is one change you will need to make when following this guide. Anaconda’s default install location is your home directory, but on Linux machines at STScI the home directory has a 10GB quota.  To work around this we recommend installing Anaconda into your ``/user/username/`` folder.  

To do this you can use the ``-p`` option when installing Anaconda. At this time you can provide whatever directory path you would like, but keep in mind the final directory in the path must not exist, as the installer will want to create this folder. For example:

.. code:: sh
   
   $ sh Anaconda2-4.0.0-Linux-x86_64.sh -p /user/username/anaconda2

Here you can change the folder name ``anaconda2`` to correspond to whichever version you chose to install, i.e. ``anaconda3``, ``miniconda2``, or ``miniconda3``.


.. toctree::
   :maxdepth: 2
   :titlesonly:

   bash_setup
   installing_anaconda
   anaconda_linux_servers
