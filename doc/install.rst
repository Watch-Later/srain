============
Installation
============

Srain is available on :ref:`install-packages-gnu-linux`,
:ref:`install-packages-windows`, :ref:`install-packages-macos` and
:ref:`install-packages-bsd`.

.. contents::
    :local:
    :depth: 3
    :backlinks: none

.. _install-dependencies:

Dependencies
============

=================== =================================================== =======
Name                Notes                                               Version
=================== =================================================== =======
coreutils           Only for building
make                Only for building
gcc                 Only for building
pkg-config          Only for building
gettext             Only for building
glib2
glib-networking     Optional, For TLS connection support
gtk+3                                                                   >= 3.18
libsoup
libsecret
openssl
=================== =================================================== =======

.. _install-building:

Building
========

You should install the aboved :ref:`install-dependencies` on your platform
before the following steps.

Firstly, download source code of srain,
you can get source code of latest release:

.. code-block:: console

    $ wget https://github.com/SrainApp/srain/archive/1.1.tar.gz
    $ tar -xvzf 1.1.tar.gz
    $ cd srain-1.1

Or get git version:

.. code-block:: console

    $ git clone https://github.com/SrainApp/srain.git
    $ cd srain

Setup build options and start building:

.. code-block:: console

   $ ./configure                     \
         --prefix=/usr/local         \
         --datadir=/usr/local/share  \
         --sysconfdir=/etc
   $ make

.. note::

    The ``configure`` script **DOES NOT** check any dependience.
    You should make sure that you have all dependencies installed.

Install(root privileges required):

.. code-block:: console

   # make install

Build and install documentation:

.. code-block:: console

   $ make doc
   # make install-doc

Distribution Packages
=====================

.. _install-packages-gnu-linux:

GNU/Linux
---------

Arch Linux
~~~~~~~~~~

Packages `srain`_ and `srain-git`_ (git version) are available on AUR,
it is quite easy to install using AUR helper(yay as an example):

.. code-block:: console

    $ yay -S srain
    $ yay -S srain-git # git version

If you are the user of `Arch Linux CN Repository`_, try:

.. code-block:: console

    # pacman -S archlinuxcn/srain
    # pacman -S archlinuxcn/srain-git # git version

.. _srain: https://aur.archlinux.org/packages/srain
.. _srain-git: https://aur.archlinux.org/packages/srain-git
.. _Arch Linux CN Repository: https://www.archlinuxcn.org/archlinux-cn-repo-and-mirror

.. _install-packages-debian:

Debian
~~~~~~

There is no srain package in the official repository yet. But you can package
it by yourself.

Copy the debian folder on `srain-contrib`_ to srain folder. Then type following
command on your terminal:

.. code-block:: console

    $ dpkg-buildpackage -b -us -uc

Note that the dependencies mentioned above also should be installed. The
details could be found on `debian/crontrol`_ file.

Then install the package (replace package name with the name of your package):

.. code-block:: console

    $ sudo apt-get install -f ../srain_1.0.1-1_amd64.deb 

.. _srain-contrib: https://github.com/SrainApp/srain-contrib/tree/master/pack/
.. _debian/crontrol: https://github.com/SrainApp/srain-contrib/blob/master/pack/debian/control

.. _install-packages-flatpak:

Fedora
~~~~~~

Srain now in `offical repository of fedora`_, use ``dnf`` to install it.

.. code-block:: console

   # dnf install srain

.. _offical repository of fedora: https://apps.fedoraproject.org/packages/srain

Flatpak
~~~~~~~

.. image:: https://flathub.org/assets/badges/flathub-badge-i-en.svg
   :width: 240
   :target: https://flathub.org/apps/details/im.srain.Srain

`cpba`_ is maintaining `Flatpak manifest for Srain`_ and The built package is
available on `Flathub`_, just execute the following commands to install if
you already have flatpak installed:

.. code-block:: console

    $ flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
    $ flatpak install flathub im.srain.Srain

.. _cpba: https://github.com/cpba
.. _Flatpak manifest for Srain: https://github.com/SrainApp/srain-contrib/tree/master/pack/flatpak
.. _Flathub: https://flathub.org

.. _install-packages-gentoo:

Gentoo
~~~~~~

Please refers to `gentoo portage overlays`_.

.. _gentoo portage overlays: https://gpo.zugaina.org/net-im/srain

.. _install-packages-opensuse:

openSUSE
~~~~~~~~

`alois`_ is maintaining `openSUSE package for Srain`_,
following this link to install it.

.. _alois: https://build.opensuse.org/user/show/alois
.. _openSUSE package for Srain: https://software.opensuse.org/package/Srain

.. _install-packages-windows:

Windows
-------

.. warning:: Windows support of Srain is still experimental.

Srain requires Windows 7 or later.

The easiest way to build/run Srain on Windows is using the toolchains provided
by `MSYS2 project`_.

Firstly install MSYS2, then open a MSYS2 shell, install the basic build tools:

.. code-block:: console

    $ pacman -S base-devel
    $ pacman -S mingw-w64-i686-toolchain     # For 32-bit Windows
    $ pacman -S mingw-w64-x86_64-toolchain   # For 64-bit Windows

Then download the package script from `MinGW PKGBUILD for Srain`_,
run the following commands at the directory of PKGBUILD:

.. code-block:: console

    $ MINGW_INSTALLS=mingw32 makepkg-mingw -fsi # For 32-bit Windows
    $ MINGW_INSTALLS=mingw64 makepkg-mingw -fsi # For 64-bit Windows

If everything goes well, Srain is installed under your MinGW prefix.

.. note::

   If you suffer the
   "error while loading shared libraries: xxxx.dll: cannot open shared object file: No such file or directory"
   problem when running, please run it in cmd but not msys2 shell,
   and it will show you real missing library. [#Alexpux-MINGW-packages-issue-3939]_


.. _MSYS2 project: http://www.msys2.org/
.. _MinGW PKGBUILD for Srain: https://github.com/SrainApp/srain-contrib/tree/master/pack/mingw
.. [#Alexpux-MINGW-packages-issue-3939] https://github.com/Alexpux/MINGW-packages/issues/3939#issuecomment-397988379

.. _install-packages-macos:

macOS
-----

.. warning:: macOS support of Srain is still experimental.

There is not a distribution package or package script for Srain on macOS,
you should build Srain by yourself.

Firstly install `Homebrew`_, run the following commands to install dependencies:

.. code-block:: console

   $ brew install coreutils gcc pkg-config # building
   $ brew install gettext glib-networking gtk+3 libsoup

.. _Homebrew: https://brew.sh/

Then follow the steps in :ref:`install-building`.

.. _install-packages-bsd:

BSD
---

OpenBSD
~~~~~~~

Please refers to `OpenBSD Ports`_.

.. _OpenBSD Ports: https://openports.se/net/srain
