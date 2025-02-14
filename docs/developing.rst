.. _development:

Development
=====================================

Adding new games can be done without recompiling Gym Retro, but if you need to work on the C++ code or make changes to the UI, you will want to compile Gym Retro from source.

Install Retro from source
--------------------------------------

Building Gym Retro requires at least either gcc 5 or clang 3.4.

Prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To build Gym Retro you must first install CMake.
You can do this either through your package manager, download from the `official site <https://cmake.org/download/>`_ or ``pip3 install cmake``.
If you're using the official installer on Windows, make sure to tell CMake to add itself to the system PATH.

Mac prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Since LuaJIT does not work properly on macOS you must first install Lua 5.1 from homebrew:

.. code-block:: shell

    brew install pkg-config lua@5.1

Windows prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Install docker

Linux prerequisites
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: shell

    sudo apt-get install zlib1g-dev

Building Linux and Mac
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block:: shell

    git clone https://github.com/openai/retro.git gym-retro
    cd gym-retro
    pip3 install -e .

Building Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Run the following

.. code-block:: shell

    docker/build_windows.bat

Once complete use docker cp to copy the whl file out of the container.

Then you may pip install

.. code-block:: shell

    pip3 install -e <path to whl>

Install Retro UI from source
--------------------------------------

First make sure you can install Retro from source, after that follow the instructions for your platform:

macOS
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Note that for Mojave (10.14) you may need to install ``/Library/Developer/CommandLineTools/Packages/macOS_SDK_headers_for_macOS_10.14.pkg``

.. code-block:: shell

    brew install pkg-config capnp lua@5.1 qt5
    cmake . -DCMAKE_PREFIX_PATH=/usr/local/opt/qt -DBUILD_UI=ON -UPYLIB_DIRECTORY
    make -j$(sysctl hw.ncpu | cut -d: -f2)
    open "Gym Retro Integration.app"


Linux
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


.. code-block:: shell

    sudo apt-get install capnproto libcapnp-dev libqt5opengl5-dev qtbase5-dev zlib1g-dev
    cmake . -DBUILD_UI=ON -UPYLIB_DIRECTORY
    make -j$(grep -c ^processor /proc/cpuinfo)
    ./gym-retro-integration

Windows
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The Retro UI is not currently supported in Windows.
