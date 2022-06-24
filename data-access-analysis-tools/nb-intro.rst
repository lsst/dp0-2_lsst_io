.. Review the README on instructions to contribute.
.. Review the style guide to keep a consistent approach to the documentation.
.. Static objects, such as figures, should be stored in the _static directory. Review the _static/README on instructions to contribute.
.. Do not remove the comments that describe each section. They are included to provide guidance to contributors.
.. Do not remove other content provided in the templates, such as a section. Instead, comment out the content and include comments to explain the situation. For example:
	- If a section within the template is not needed, comment out the section title and label reference. Do not delete the expected section title, reference or related comments provided from the template.
    - If a file cannot include a title (surrounded by ampersands (#)), comment out the title from the template and include a comment explaining why this is implemented (in addition to applying the ``title`` directive).

.. This is the label that can be used for cross referencing this file.
.. Recommended title label format is "Directory Name"-"Title Name" -- Spaces should be replaced by hyphens.
.. _Data-Access-Analysis-Tools-NB-Intro:
.. Each section should include a label for cross referencing to a given area.
.. Recommended format for all labels is "Title Name"-"Section Name" -- Spaces should be replaced by hyphens.
.. To reference a label that isn't associated with an reST object such as a title or figure, you must include the link and explicit title using the syntax :ref:`link text <label-name>`.
.. A warning will alert you of identical labels during the linkcheck process.

#######################################
Introduction to the RSP Notebook Aspect
#######################################

.. This section should provide a brief, top-level description of the page.

Most RSP users will find Jupyter Notebooks to be the most efficient and powerful way to interact with the LSST data sets.

**Always save and shutdown all notebooks and log out of JupyterLab when you are done your day's work.**
This is important to preserve resources for other users and to ensure you re-enter the RSP in a known state every time.
To help users avoid issues with stale instances, sessions will be automatically shut-down after 5 days of inactivity, or after 25 days.

This page focuses on the basic instructions for using the RSP Notebook Aspect, and a few FAQs and Troubleshooting Tips.
The full documentation for the RSP Notebook Aspect is available at `nb.lsst.io <https://nb.lsst.io/>`_.


.. _NB-Intro-Login:

How to log in, navigate, and log out of JupyterLab
==================================================

From the RSP landing page at `data.lsst.cloud <https://data.lsst.cloud/>`_ click on the central panel for Notebooks.

**Software Version and Server Size:**
The first page offers a choice of software environment version (left) and server size (right), as shown in the next figure.
Most users will choose the recommended software version and a medium server size.

.. figure:: /_static/RSP_NB_select_a_server.png
    :width: 400
    :name: RSP_NB_select_a_server

    Most users will choose the recommended software version and a medium size.

The term "image" atop the left box refers to a "Docker image" that defines the software packages and their versions which will be automatically loaded in the server environment.
The "recommended" image will be updated on a regular (monthly) basis to encourage users to adapt to using software that is in active development, and to benefit from the bug fixes and updates made by Rubin Observatory staff.
Older images will remain accessible to users.

RSP users who are doing a lot of image processing might need to select a large server, and those who are working with small subsets of catalog data can use a small server.

**Start the Server:**
Pressing the orange "Start" button to start the server returns this page with a blue progress bar:

.. figure:: /_static/RSP_NB_progress_bar.png
    :width: 400
    :name: RSP_NB_progress_bar

    Be patient. Sometimes it takes a couple of minutes to start a server.

**Navigating the JupyterLab Interface:**
The JupyterLab landing page in the figure below is the launch pad for all JupyterLab functionality (e.g., Notebook, Terminal, Python console).
Return to this launch pad at any time by clicking the plus symbol at upper-left.

.. figure:: /_static/RSP_NB_launcher_options.png
    :width: 400
    :name: RSP_NB_launcher_options

    The JupyterLab landing page from which several tools can be launched and the file system can be browsed (left sidebar).

In the very left-most vertical sidebar of icons, the top icon is a file folder, and that is the default view.
The left sidebar lists folders in the user's home directory (e.g., DATA, WORK, and notebooks).
Launching a terminal (the default is a linux bash terminal) and using the command "ls" will return the same list.
Navigate the file system and open files by double-clicking on folders and files in the left sidebar.

Although the file browser is a handy way to navigate your user home space, it does not allow you to navigate to, e.g., the shared data space.
One way to make other spaces available in the file browser is to create a `symbolic link <https://en.m.wikipedia.org/wiki/Symbolic_link>`_ using the Terminal to the desired space somewhere in your home directory.

Jupyter Notebooks can be identified by their file extension ".ipynb".
All users will find a set of tutorial notebooks provided in the "notebooks/tutorial-notebooks/" directory.

**Safely Log Out of JupyterLab:**
Use the "File" menu in the top menu bar.
To safely shut down a Notebook, choose "Close and Shutdown Notebook".
To safely shut down a JupyterLab server and log out of the RSP, choose "Save all, Exit, and Log Out".
It is recommended you log out every time you are finished with a session in order to both preserve resources for other users and to ensure you re-enter the RSP in a known state every time.
To help users avoid issues with stale instances, sessions will be automatically shut-down after 5 days of inactivity, or after 25 days.


.. _NB-Intro-Use-A-JL-terminal:

How to use the JupyterLab terminal
==================================

The :ref:`Data-Products-DP0-2-Data-Products` and the `LSST Science Pipelines <https://pipelines.lsst.io/>`_ tools can both be accessed from the command line of a JupyterLab terminal tab.
A terminal session can be started by clicking on the terminal icon in the Jupyterlab launch pad.
As described in the default message that appears in all newly-launched terminals, to create a Rubin Observatory environment in a JupyterLab terminal session and set up the full set of packages, users must first execute:

.. code-block:: bash

   source ${LOADSTACK}
   setup lsst_distrib

For example, to query and retrieve data sets using the Butler (see :ref:`NB-Intro-Use-A-NB-faq-butler`, below), command-line tools are available as `documented here <https://pipelines.lsst.io/v/weekly/modules/lsst.daf.butler/scripts/butler.html>`_.
Type "butler --help" in any terminal to see a list of available butler functionality.


.. _NB-Intro-Use-A-NB:

How to use a Jupyter notebook
=============================

The best way to learn how to use a Jupyter Notebook is to open the first of the tutorial notebooks which are provided in each user's home directory,
and also available in the `tutorial-notebooks <https://github.com/rubin-dp0/tutorial-notebooks>`_ repository in the "rubin-dp0" GitHub Organization (see also :ref:`DP0-2-Tutorials-Notebooks`).

**Executing code in a Notebook:**
Jupyter notebooks provide "cells" within which you type either Python code or markdown language (for formatted text).
Choose the cell to execute by clicking in it with your mouse (the cursor must be in the desired cell).
Hold down the `shift` key and press either `enter` or `return` (depending on your keyboard type), or click the 'Play' button in the notebook toolbar, and the contents of the cell will be executed.
If the cell type is code, and the cell contains python code, the code will be executed.
If the cell type is markdown, then it will be rendered upon execution to yield nicely formatted text.
For some handy markdown tips, see `this blog post <https://medium.com/analytics-vidhya/the-ultimate-markdown-guide-for-jupyter-notebook-d5e5abf728fd>`_.

.. figure:: /_static/notebook.png
    :name: notebook_aspect

    An example of what users see in the Notebook Aspect. The left panel is a file tree from which you can access your personal files,
    and which will come pre-populated with a handful of tutorial notebooks that users can execute on their own. The largest panel is the Jupyter notebook, where markdown and code can be entered and executed.
    You can also see that one can have multiple notebooks open in separate tabs.

**Opening Multiple Notebooks:**
You can have multiple notebooks and terminals open in your viewer at a time.
This is very handy, but you can also arrange both notebooks and terminals next to or on top of each other by dragging the notebook or terminal around by the top bar.
Arranging the windows can be convenient when working in both a terminal and notebook at the same time, or when using another notebook as a reference.

**JupyterLab Autosaves Notebooks:**
Note that JupyterLab autosaves your notebooks at a default rate of 2 minutes.


.. _NB-Intro-Use-A-NB-faq:

Jupyter notebook frequently asked questions
===========================================


.. _NB-Intro-Use-A-NB-faq-kernel:

What is a kernel?
-----------------

In the RSP Notebook Aspect, your notebooks will be operating in a kernel that has access to the full `LSST Science Pipelines <https://pipelines.lsst.io/>`_, including the Butler (see :ref:`NB-Intro-Use-A-NB-faq-butler`, below).
Many standard Python libraries and modules will be available, and users can `install <https://nb.lsst.io/environment/python.html>`_ additional Python tools they wish to use.
See also `this tutorial on installing python packages <https://packaging.python.org/en/latest/tutorials/installing-packages/>`_
(which includes, e.g., use of "pip install").
To view a list of packages available to you, type "pip list" in a terminal.


.. _NB-Intro-Use-A-NB-faq-python:

Is all the code in Python?
--------------------------

Yes, the RSP Notebook Aspect will only have python environments for DP0.

To access data from the Notebook Aspect, users will need to use Python commands and code.
Much of the `LSST Science Pipelines <https://pipelines.lsst.io/>`_ code is in Python, and the DP0 :ref:`DP0-2-Tutorials-Notebooks` use Python as well.
These tutorials contain executable examples of the commands required to access and analyze data.
All DP0 delegates should feel free to copy and paste from the provided tutorials.

Anyone new to Python and looking to learn more might benefit from this `Python for Beginners <https://www.python.org/about/gettingstarted>`_ website (which includes links to tutorial in a variety of languages),
or this Community Forum thread where DP0 delegates can share `resources for python beginners <https://community.lsst.org/t/5975>`_.
Web searches for "python *(thing you want to do)*" are usually pretty successful too.


.. _NB-Intro-Use-A-NB-faq-github:

Do I need to know git?
----------------------

Although use of git and GitHub are not neccessary for DP0 participation, most Rubin Observatory staff and LSST Science Collaborations use git and GitHub, and it is highly recommended by the Community Engagement Team for all RSP users.
Git is free open-sourced software for change-tracking and version control of any set of files that are edited by one or more contributors.
GitHub is a web-based provider for git functionality, plus it offers a few of its own features.
In this Community Forum thread, everyone can find and share `resources for learning about git and GitHub <https://community.lsst.org/t/resources-for-github/6153>`_.
A few of the :ref:`NB-Intro-Use-A-NB-tips` below involve the use of git.


.. _NB-Intro-Use-A-NB-faq-butler:

What is the Butler?
-------------------

The Butler is a middleware component of the Data Management System (DMS) for persisting and retrieving datasets.
The third generation "Gen3" Butler is the version being used for DP0.2.
Full `Butler documentation <https://pipelines.lsst.io/modules/lsst.daf.butler/index.html>`_ is available, and several of the :ref:`DP0-2-Tutorials-Notebooks` demonstrate Butler use as well.


.. _NB-Intro-Use-A-NB-faq-questions:

How do I ask questions about Notebooks?
---------------------------------------

Keep in mind that if you are not experienced at accessing data via Jupyter notebooks, or using a Science Platform more generally, you are not alone!
Most of the DP0 delegates are new to this environment, and all of your questions and feedback will help us improve both the documentation and the tools.

The `DP0 Delegate Homepage <https://dp0-2.lsst.io>`_ provides information about :ref:`Delegate-Homepage-Getting-Support` at any time via the `Rubin Observatory Community Forum <https://community.lsst.org/>`_ or via GitHub Issues.
Another option is to attend the biweekly :ref:`Delegate-Homepage-DP0-Delegate-Assemblies` which will feature live tutorials and question-and-answer time with Rubin Observatory staff.

Beginner-level questions are very welcome, both in the Community Forum and during the Delegate Assemblies.
To encourage questions in the Forum, a couple of beginner-level topics have been started to share resources for
learning `python <https://community.lsst.org/t/resources-for-python-beginners/5975>`_ and `SQL <https://community.lsst.org/t/sql-adql-beginner-resources/6051>`_.
People new to the Rubin Community Forum might appreciate `this video demonstrating how to navigate and post topics to the forum <https://www.youtube.com/watch?v=d_Z5xmkR4P4&list=PLPINAcUH0dXZSx2aY6wTIjLCWiexs3dZR&index=10>`_.


.. _NB-Intro-Use-A-NB-tips:

Troubleshooting tips
====================

How to recover from package import errors (ImportError)
-------------------------------------------------------

**The Problem:** In this case the problem manifests when a package cannot be properly imported.
This leads to an ImportError for which the last line of the traceback actually points to the file it is trying to import from, and it is in the users ".local" directory.

If a user sees a mention of ".local" anywhere in the exception, there is a chance they have installed packages that are polluting stack environments, and this is a big red flag that following the solution below will be necessary.

However, this is not the only way this problem can manifest, as issues with user-installed packages can be hard to track down. E.g., it might import fine, but then not be able to find an attribute or method on a particular object.

**The Solution:** Users should exit the RSP and then clear their ".local" file when they log back in to the Notebook Aspect by checking the box "Clear .local directory (caution!)"
on the Hub spawner page (see the "Server Options" image at the top of this page).
This option is simple and effective, and also helps in cases where the user-installed packages are keeping JupyterLab from starting.

**An Alternative Solution:** The user should first close and shutdown the notebook (or, e.g., ipython session) which is experiencing the error, and then launch a terminal in the Notebook Aspect
and move their ".local" file out of the way by renaming it as something else, such as:

.. code-block:: bash

   mv ~/.local ~/.local_[YYYY][MM][DD]

There will be no need to recreate the ".local" directory after this.
The user should then restart the notebook (or, e.g., ipython session) and try to import the packages.

What to do if Notebooks do not automatically update
---------------------------------------------------

New versions of the tutorial notebooks will be periodically released by the Community Engagement Team (CET).
The contents of your "notebooks/tutorial-notebooks/" directory should automatically update when a new version of a tutorial notebook is released.
There are several reasons why this might not occur, and, correspondingly, several ways for you to update the contents of your "notebooks/tutorial-notebooks/" directory.

All of the options below require that you first configure git for your GitHub account using the terminal in the RSP Notebook Aspect.
First, check whether your GitHub user name and email are configured correctly in the ".gitconfig" file in your home directory.
To do this, use the following command in the terminal window of the RSP Notebook Aspect:

.. code-block:: bash

   egrep 'email|name' ~/.gitconfig

If nothing is returned, then your GitHub email and user name have not been set up.
You may set them up by typing in the following commands (remember to use the same GitHub account information you use to access the RSP):

.. code-block:: bash

   git config --global user.email yourEmail@yourdomain
   git config --global user.name GItUsername

From here, you have three options to update the contents of your "notebooks/tutorial-notebooks/" directory.

**Option 1** (if you have not saved changed versions of the notebooks) - Fully log out, stop the server, and log back in again.
This will automatically refresh the contents of your "notebooks/tutorial-notebooks/" directory.
To fully stop your server, use the control panel at `data.lsst.cloud/nb/hub/home <https://data.lsst.cloud/nb/hub/home>`_.
Click the red button that says "Stop My Server".

**Option 2** (if you have saved changed versions of the notebooks that you want to keep) - The first option, above, will not result in you having the most up-to-date versions of all the notebooks if you have made and saved changes to any of the notebooks.
To check if files have been modified, use this command from a terminal in the "notebooks/tutorial-notebooks/" directory.

.. code-block:: bash

   git status

If it says in red text, e.g., "both modified: 01_Intro_to_DP0_Notebooks.ipynb", then changes have been made to this file (recall that executing the notebook counts as making changes,
and note that Jupyter auto-saves changes on a ~2 minute cadence), but Rubin Observatory staff have also updated it (e.g., bug fixes).
Since the file has been twice modified, git has gone ahead and annotated file with all the conflicting lines between the two versions.
This essentially ruins a ".ipynb" file's functionality (but it is a very useful built-in git feature for, e.g., ascii and code files).
A git-annotated ".ipynb" file might not even load or run for you anymore.
On the command line, do

.. code-block:: bash

   git diff 01_Intro_to_DP0_Notebooks.ipynb
   
and all the differences will be listed.

Use the following commands in the terminal window to restore the version in which you made changes (this takes it out of 'staged' status and will avoid future errors),
copy your version into a different directory and rename it, and then restore the new version of the notebook that was updated by Rubin Observatory staff.

.. code-block:: bash

   git restore --staged 01_Intro_to_DP0_Notebooks.ipynb
   cp 01_Intro_to_DP0_Notebooks.ipynb ~/my-notebooks/01_my_version.ipynb
   git restore 01_Intro_to_DP0_Notebooks.ipynb

Now your notebooks/tutorial-notebooks directory only contains the most up-to-date versions of the tutorial notebooks, with none of your changes.

**Option 3** (if you don't care about keeping changed versions of the notebooks) - To get a completely new version of all the tutorial notebooks in your "notebooks/tutorial-notebooks/" directory, use the following commands:

.. code-block:: bash

   git reset --hard origin/prod
   git pull

Using any of the above options is the preferred method to update your tutorial notebooks, but as a last resort, you can delete the entire "tutorial-notebooks/" directory, log out and stop the server, and then log back in again.


How to make git stop asking for my password
-------------------------------------------

It is recommended that all git users working in the RSP to configure git and set up an SSH key.
First, using a terminal in the Notebook aspect, set the global git configurations.

.. code-block:: bash

   git config --global user.email yourEmail@yourdomain
   git config --global user.name GItUsername

Then, using a terminal in the Notebook aspect, follow these instructions for `generating a new SSH key and adding it to the ssh-agent <https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent>`_.
Be sure to follow the instructions for the Linux environment (i.e., the RSP environment), regardless of your personal computer's environment, because you are generating an SSH key *for your account in the RSP*.

When you `git clone` new repositories, use the SSH link.
If successful, you will be able to git fetch and push without entering your git password.
