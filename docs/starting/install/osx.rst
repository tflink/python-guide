.. _install-osx:

Installing Python on Mac OS X
=============================

The latest version of Mac OS X, Mountain Lion, **comes with Python 2.7 out of the box**.

You do not need to install or configure anything else to use Python. Having
said that, I would strongly recommend that you install the tools and libraries
described in the next section before you start building Python applications
for real-world use. In particular, you should always install Distribute, as it
makes it much easier for you to use other third-party Python libraries.

The version of Python that ships with OS X is great for learning, but it's not
good for development. It's slightly out of date, and Apple has made significant
changes that can cause hidden bugs.

Doing it Right
--------------

Let's install a real version of Python.

Before installing Python, you'll need to install GCC. GCC can be obtained
by downloading `XCode <http://developer.apple.com/xcode/>`_, the smaller
`Command Line Tools <https://developer.apple.com/downloads/>`_ (must have an
Apple account) or the even smaller `OSX-GCC-Installer <https://github.com/kennethreitz/osx-gcc-installer#readme>`_
package.

While Lion comes with a large number of UNIX utilities, those familiar with
Linux systems will notice one key component missing: a decent package manager.
`Homebrew <http://mxcl.github.com/homebrew/>`_ fills this void.

To `install Homebrew <https://github.com/mxcl/homebrew/wiki/installation>`_,
simply run

.. code-block:: console

    $ ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"

The script will explain what changes it will make and prompt you before the
installation begins.
Once you've installed Homebrew, insert the Homebrew directory at the top
of your ``PATH`` environment variable. You can do this by adding the following
line at the bottom of your ``~/.bashrc`` file

.. code-block:: console

    export PATH=/usr/local/bin:$PATH

Now, we can install Python 2.7: ::

    $ brew install python --framework

This will take a minute or two. Once that's complete, you'll have to add the
new Python scripts directory to your ``PATH``

.. code-block:: console

    export PATH=/usr/local/share/python:$PATH

The ``--framework`` option tells Homebrew to compile a Framework-style Python
build, rather than a UNIX-style build. The outdated version of Python that
Snow Leopard comes packaged with is built as a Framework, so this helps avoid
some future module installation bugs.


Distribute & Pip
----------------

The most crucial third-party Python software of all is Distribute, which
extends the packaging and installation facilities provided by the distutils
in the standard library. Once you add Distribute to your Python system you can
download and install any compliant Python software product with a single
command. It also enables you to add this network installation capability to
your own Python software with very little work.

Homebrew already installed Distribute for you. Its ``easy_install`` command is
considered by many to be deprecated, so we will install its replacement:
**pip**. Pip allows for uninstallation of packages, and is actively maintained,
unlike easy_install.

To install pip, simply open a command prompt and run

.. code-block:: console

    $ easy_install pip


Virtualenv
----------

After Distribute & Pip, the next development tool that you should install is
`virtualenv <http://pypi.python.org/pypi/virtualenv/>`_. Use pip

.. code-block:: console

    $ pip install virtualenv

The virtualenv kit provides the ability to create virtual Python environments
that do not interfere with either each other, or the main Python installation.
If you install virtualenv before you begin coding then you can get into the
habit of using it to create completely clean Python environments for each
project. This is particularly important for Web development, where each
framework and application will have many dependencies.

To set up a new Python environment, change the working directory to where ever
you want to store the environment, and run the virtualenv utility in your
project's directory

.. code-block:: console

    $ virtualenv --distribute venv

To use an environment, run ``source venv/bin/activate``. Your command prompt
will change to show the active environment. Once you have finished working in
the current virtual environment, run ``deactivate`` to restore your settings
to normal.

Each new environment automatically includes a copy of ``pip``, so that you can
setup the third-party libraries and tools that you want to use in that
environment. Put your own code within a subdirectory of the environment,
however you wish. When you no longer need a particular environment, simply
copy your code out of it, and then delete the main directory for the environment.


--------------------------------

This page is a remixed version of `another guide <http://www.stuartellis.eu/articles/python-development-windows/>`_,
which is available under the same license.
