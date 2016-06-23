##########
Bash Setup
##########



Step 1: Removing references to Ureka
------------------------------------


Remove all references to ``Ureka`` (``SSB`` , ``SSBX``, ``SSBDEV``) in your shell files.  If you have never edited your ``bash`` setup files ``.profile``, or ``.bash*``), you can ignore these for now as we are going to delete them all later on, and just focus on your ``tcsh`` files, these could include: ``.cshrc``, ``.setenv``, or ``.scienv``.  You may or may not have some of these files depending on when your machine was set up originally. Accounts created after 2008 may have an additional ``.mysetenv`` file.

If you not sure what to look for, and haven’t edited your shell files before, look for references to ``ssbx``, ``ssbrel`` or ``ssbdev`` and remove those lines.  You can use the following listed commands to search for ``Ureka`` dependencies.  You may see a return from your ``$HOME/.ureka/.default`` file.  This is expected and can be ignored.


**linux**:

.. code-block:: sh

    find $HOME -maxdepth 1 -type f -name '.*' | xargs -I'{}' grep -n -H -E --color=auto 'ssbrel|ssbx|ssbdev' "{}"

**osx**: 

Darwin’s BSD find does not support -maxdepth (users can install gnu findutils if they wish to execute the linux-style command on OS X, however)

.. code-block:: sh
    
    find $HOME -type f -name '.*' | xargs -I'{}' grep -n -H -E --color=auto 'ssbrel|ssbx|ssbdev' "{}"


Step 2: Backup your current bash files
--------------------------------------

.. warning::

   Only follow this step if you have not added anything to your ITSD-provided ``bash`` setup files (``.profile``, or ``.bash*``).  If your ``bash`` files are configured already, you can skip steps 2 and 3.

Tar and zip your current bash setup files with the following command:

.. code-block:: sh

    tar cfz envbackup.tar.gz .profile .bash* 


Step 3: Rebuilding your bash startup files
------------------------------------------
Now that you have a backup of your ``bash`` files safely stored, wipe all ``bash`` startup files currently in your ``~home`` directory.

.. code-block:: sh

	
    >rm ~/.profile
    >rm ~/.bash*


Open up a new ``~/.bash_profile`` file.  Remember this should be a blank text file, since we just deleted the previous copy if it existed.  We will also set up a ``~/.bashrc`` file.  Below is an example of a standard ``~/.bash_profile`` and  ``~/.bashrc``.

.. code-block:: sh

    # File - ~/.bash_profile (or .profile)

    # Common shell aliases
    alias ls='ls -G'
    alias ll='ls -l'
    alias grep='--color=auto'

    if [ -f $HOME/.bashrc ]; then
	source $HOME/.bashrc

    # EOF

.. code-block:: sh

    # File - ~/.bashrc

    # Tune your profile…
    export PATH="$PATH:$LOCAL_CUSTOM/bin:$PATH"
    export MANPATH="$LOCAL_CUSTOM/share/man:$MANPATH"

    alias rdesktop='rdesktop -g 85%'

    # EOF


Using this line:

.. code-block:: sh

    if [ -f $HOME/.bashrc ]; then
	source $HOME/.bashrc


the ``~/.bashrc`` file will get sourced by ``~/.bash_profile``.

Now we can start to port the environment setup information that was in the ``tcsh`` startup files over to your ``bash`` files.  Most of these commands will either be ``setenv`` or ``alias`` commands.  **There is a syntax difference between ``tcsh`` and ``bash``**.  You can put these kinds of commands into your ``.bash_profile`` file.  Below are some examples of how to translate ``tcsh`` to ``bash`` syntax.




.. code-block:: sh

    setenv cdbs /grp/hst/cdbs/
    export cdbs="/grp/hst/cdbs/"

    setenv PATH $HOME/pybin:${PATH}
    export PATH="~/pybin:$PATH"

    alias emax 'open -a "Aquamacs"'
    alias emax='open -a "Aquamacs"'

A few ``bash`` commands are less straightforward to change over, such as default editor.

.. code-block:: sh

    setenv EMACS editor
    EDITOR=emacs; export EDITOR

Finally, you should now restart your terminal program so that these changes are applied.

    
.. note::

   **Regarding if statements:** Many of the statements originally in the ``tcsh`` files that were nested in ``if`` statement calls were set up to test if your machine was connected to the STScI network.  For example, if you set up an environment variable that links to a directory on ``/grp/hst/`` and try and access this directory from outside the institute network, it will fail.

   For ``if`` statements that you have written into your ``tcsh`` files yourself, please see this `bash guide <http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html>`_ for ``if`` statements in ``bash``.




Step 4: Bash as default, or temporary bash sessions
---------------------------------------------------

Switching to bash as your default shell
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. warning::

    You may want to wait to execute this step until after you have installed and tested Anaconda.

**For Mac**

To switch your default shell on Mac machines, open a terminal and use the following command

.. code-block:: sh

    > chsh -s /bin/bash

and enter your password. To verify that the change went through, restart your terminal program, and type the following:

.. code-block:: sh

    $ echo $SHELL

This command should return ``/bin/bash``


**For Linux**

To change the default shell on Linux machines (this includes the Linux servers at STScI) you will need to contact IT to switch your AD account settings.  The path to your default shell is controlled by Active Directory (AD), which can only be modified by ITSD.


Using bash from tcsh
^^^^^^^^^^^^^^^^^^^^

If you plan on using ``bash`` from ``tsch``, you can switch into ``bash`` using

.. code-block:: sh

   >bash -l

This call will inherit your environment setup from your ``tcsh``.  This means any environment variables you have set in your ``tsch`` will get transferred over. 

.. warning::

   If you have a call to ``ssbx/dev/rel`` in one of your ``tsch`` setup file ``Anaconda`` will not run properly!
