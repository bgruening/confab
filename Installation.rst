Installation
============

Confab runs on Windows, Linux and MacOSX. For Windows, a binary release is available for download. On other systems, you need to compile it yourself.

Windows
-------

1. Download the Confab `zip file`_.

2. Unzip the file to a suitable location.

3. At the command line, run :file:`env.bat` to set some environment variables.

4. Try ``confab -h`` and ``calcrmsd -h`` to see help text.

.. _zip file: http://confab.googlecode.com/files/Confab-1.0.zip

Linux or MacOSX
---------------

Confab is essentially a modified version of Open Babel 2.3dev with additional components. The build instructions here are based on those for Open Babel 2.3.

.. _requirements:

Requirements
~~~~~~~~~~~~

To build Confab, you **need** the following:

* The `source code`_ for Confab
* A C++ compiler

    Compilation has been tested with GCC 4, but it should also work with Intel Compiler 11 (untested). 

* CMake 2.4 or newer

    Confab uses CMake as its build system. CMake is a open source cross-platform build system from KitWare.

    You need to install CMake 2.4 or newer. This is available as a binary package from the KitWare website; alternatively, it may be available through your package manager (on Linux). If necessary, you can also compile it yourself from the source code.

* :program:`Eigen` version 2

  Eigen may be available through your package manager (the *libeigen2-dev* package in Ubuntu). Alternatively, Eigen is available from http://eigen.tuxfamily.org. It doesn't need to be compiled or installed. Just unzip it and specify its location when configuring :program:`cmake` (see below) using ``-DEIGEN2_INCLUDE_DIR=whereever``.

.. _source code: http://confab.googlecode.com/files/Confab-1.0.tar.gz

The following are **optional** when compiling Confab, but if not available some features will be missing:

* :program:`libxml2` development headers are required to read/write CML files and other XML formats (the *libxml2-dev* package in Ubuntu) 
* :program:`zlib` development libraries are required to support reading gzipped files (the *zlib1g-dev* package in Ubuntu) 

Basic build procedure
~~~~~~~~~~~~~~~~~~~~~

The basic build procedure is the same for all platforms and will be described first. After this, we will look at variations for particular platforms.

.. highlight:: console

1. The recommended way to build Confab is to use a separate source and build directory; for example, :file:`confab-1.0` and :file:`build`. The first step is to create these directories::

        $ tar zxf confab-1.0.tar.gz   # (this creates confab-1.0)
        $ mkdir build

2. Now you need to run :program:`cmake` to configure the build. The following will configure the build to use all of the default options::

        $ cd build
        $ cmake ../confab-1.0

3. If you need to specify an option, use the ``-D`` switch to :program:`cmake`. For example, the following line sets the value of ``CMAKE_INSTALL_PREFIX`` and ``CMAKE_BUILD_TYPE``::

        $ cmake ../confab-1.0 -DCMAKE_INSTALL_PREFIX=~/Tools -DCMAKE_BUILD_TYPE=DEBUG

   We will discuss various possible options later.

4. At this point, it would be a good idea to compile Confab::

        $ make

5. And finally, as root (or using ``sudo``) you should install it::

        # make install

Local build
~~~~~~~~~~~

By default, Confab is installed in :file:`/usr/local/` on a Unix-like system. This requires root access (or ``sudo``). If instead you wish to install into a local directory, the following instructions should be followed:

1. To configure :program:`cmake` to install into :file:`~/Tools/confab-install`, for example, you would do the following::

        $ cmake ../confab-1.0 -DCMAKE_INSTALL_PREFIX=~/Tools/confab-install

2. Then you can run :command:`make` and :command:`make install` without needing root access::

        $ make && make install

Troubleshooting build problems
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. rubric:: CMake caches some variables from run-to-run. How can I wipe the cache to start from scratch?

Delete :file:`CMakeCache.txt`. This is also a very useful file to look into if you have any problems.

.. rubric:: How do I specify the location of the XML libraries?

CMake should find these automatically if they are installed system-wide. If you need to specify them, try using the ``-DLIBXML2_LIBRARIES=wherever`` option with CMake to specify the location of the DLL or SO file, and ``-DLIBXML2_INCLUDE_DIR=wherever`` to specify the location of the header files.

.. rubric:: How do I specify the location of the ZLIB libraries?

CMake should find these automatically if they are installed system-wide. If you need to specify them, try using the ``-DZLIB_LIBRARY=wherever`` option with CMake to specify the location of the DLL or SO file, and ``-DZLIB_INCLUDE_DIR=wherever`` to specify the location of the header files.
