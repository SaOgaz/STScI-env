##################################
Installing Anaconda and AstroConda
##################################

.. note::

   If you already have ``Anaconda`` on your machine and are familiar with it, you can skip ahead to Step 3.

Step 1: Install
---------------
There are several flavors of Anaconda for download. Anaconda contains the full ``anaconda`` software suite, while Miniconda contains only Conda and Python.  You also have the choice of Python 3 or Python 2.7 as your default Python version.  Please note, you can still access Python 3 from the Anaconda Python 2.7 version, and vice versa.  This just sets up your default to be one or the other.  Further details and installation instructions are available on the `Anaconda webpage <https://www.continuum.io/downloads>`_.

As previously mentioned, Anaconda works with the ``bash`` shell, so please make sure you are running install commands, etc. in a ``bash`` environment.  To do this before you have switched to ``bash`` as your default terminal, please use

.. code-block:: sh

    bash -l

Step 2: Make sure Anaconda was set up correctly
-----------------------------------------------

To test that your ``PATH`` variable was correctly set for Anaconda after installation, check for the following line in your ``~/.bashrc`` file. It should be similar to the following:

.. code-block:: sh

    Mac:
    export PATH="$HOME/anaconda3/bin:$PATH"

    Linux:
    export PATH="/user/username/anaconda2/bin"

If this line is missing please add it, making sure to use your Anaconda folder name. This varies depending on which version of Anaconda/Miniconda you downloaded. The default install location of Anaconda/Miniconda is in your home directory.  So if you’ve run the Anaconda/Miniconda install with the default settings you should now see a directory similar to this in your home directory: ``~/anaconda2`` (If you grabbed Anaconda2), ``~/miniconda3`` (if you grabbed Miniconda3), etc.


Let's talk about Conda environments...
--------------------------------------

Creating and switching Conda environments is just like switching ``Ureka`` environments, but *even better*!  We’ll cover it in a nutshell here, but for full details please see the `Anaconda documentation <http://conda.pydata.org/docs/using/envs.html>`_.  What so much better about it, you might ask?  Well, Conda environments give you complete freedom to:

* Make as many different custom environments as you want 
* Use different versions of different packages in each environment
* You decide when to update packages
* Can share your environment setup easily

Conda environments give you all the freedom to pick and choose what versions and which packages are included in that environment, without any of the hassle of having to manually install everything.   It also does a great job of keeping all your different environments separate from each other.  You can use Python 2.7 and an older version of ``Numpy`` in one environment, and another where you’re using Python 3 and the cutting edge version of your favorite Python libraries.  This makes creating a testing environment extremely easy.  Want that new ``Astropy`` function but not sure if that version of ``Astropy`` will break other parts of your code? Just make a new environment with the new ``Astropy`` version to test with.  You can still keep your working environment just where you left it.  Another great benefit is the ability to share an exact copy of your environment with others.  

So how do you make a new Conda environment? This can be done in two simple statements.  To make a new environment just use the following commands:

**Example 1:**

This installs a base version of a new environment.  Containing just the basic Python libraries.  Here we’re specifying to use Python 2 (2.7).

.. code-block:: sh

    conda create -n myenvironment python=2


**Example 2:**

Here we’re creating a new environment that will be populated with the basic Python libraries and adding in the Python ``bokeh`` library.

.. code-block:: sh

    conda create -n bokehenv python=2 bokeh


**Example 3:**

Alternatively, I could have omitted ``bokeh`` as an argument, or any specific packages, and populated my environment manually.

.. code-block:: sh

    conda create -n bokehenv
    source activate bokehenv
    conda install bokeh

**Example 4:**

It is also possible to install packages into a named environment without the need to activate it first.  The ``bokeh`` environment must already exist for this work

.. code-block:: sh

    conda install -n bokehenv bokeh
    source activate bokehenv


You’ll see these commands again as you walk through the AstroConda installation.


Step 3: Get AstroConda
----------------------

AstroConda is a package repository that is built to hook into the Anaconda distribution.  You can think of Anaconda (using Conda) as your environment manager, and AstroConda as an extra repository of packages and software (called a “channel” in Conda).  It contains many of the tools that were built into ``Ureka``.  For more information on the AstroConda packages please see the `AstroConda doc page <http://astroconda.readthedocs.io/en/latest/installation.html>`_. You will also want to reference this page if you need to include ``iraf`` in your AstroConda install.

The next step is to add the ``astroconda`` channel. 

.. code-block:: sh

    conda config --add channels http://ssb.stsci.edu/astroconda

Now we will create a new environment that contains AstroConda's ``stsci`` metapackage

.. code-block:: sh

    conda create -n astroconda stsci

and activate this new environment.

.. code-block:: sh
 
    source activate astroconda

Make sure you are installing the ``stsci`` metapackage into a new environment and not your root Anaconda environment.  If this has happened, please see the `AstroConda FAQ page <http://astroconda.readthedocs.io/en/latest/faq.html#i-installed-astroconda-into-my-anaconda-root-environment-what-now>`_ for instructions.


Step 3B: Add the Astropy channel
--------------------------------
The Astropy Project also has a Anaconda channel which contains all of the ``astropy`` affiliated packages.  While some of these are already included in ``astroconda``, if you think you might want some that aren’t you can use the following command

.. code-block:: sh

    conda config --add channels astropy

and you now have the ``astropy`` channel included by default.


Step 4: Quick test to see if your setup was succesful
-----------------------------------------------------

.. note::

    For instructions on how to keep your AstroConda package updated, please see the `AstroConda docs <http://astroconda.readthedocs.io/en/latest/updating.html>`_.


.. note::
   For a easy to use Conda reference sheet the Anaconda website has a helpful `Conda cheat sheet <http://conda.pydata.org/docs/using/cheatsheet.html>`_, or you can pick up a hardcopy right outside the IT helpdesk room in Muller 330.

Were going to simulate a fresh new bash shell for testing, so open a new terminal window and use the following commands.  You can start from a ``tcsh`` terminal.


.. code-block:: sh

    /grp/hst/ssb/blackhole/interactive.sh
    source ~/.bash_profile

If successful, the PS1 variable, responsible for controlling the look and feel of your shell prompt, will be reset to the system default; often ``[user@host: directory]$``. From here we will test Anaconda and your AstroConda install.
   

.. code-block:: sh

    source activate astroconda
    which python
    
``which python`` should return ``/path/to/astroconda/bin/python``, where ``/path/to/`` will be the path to your Anaconda installation. If this test returns unexpcted results, you can contact support@stsci.edu for assistance.


