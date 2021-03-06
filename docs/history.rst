.. _history:

===============
Project History
===============

Work on PyOxidizer started in November 2018 by Gregory Szorc.

Blog Posts
==========

* `Building Standalone Python Applications with PyOxidizer <https://gregoryszorc.com/blog/2019/06/24/building-standalone-python-applications-with-pyoxidizer>`_ (2019-06-23)
* `PyOxidizer Support for Windows <https://gregoryszorc.com/blog/2019/01/06/pyoxidizer-support-for-windows>`_ (2019-01-06)
* `Faster In-Memory Python Module Importing <https://gregoryszorc.com/blog/2018/12/28/faster-in-memory-python-module-importing>`_ (2018-12-28)
* `Distributing Standalone Python Applications <https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications>`_ (2018-12-18)

Version History
===============

Next
----

*Not yet released.*

Backwards Compatibility Notes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
* Applications are now built into an ``apps/<appname>/(debug|release)``
  directory instead of ``apps/<appname>``. This allows debug and release
  builds to exist side-by-side.

Bug Fixes
^^^^^^^^^

* Extracted ``.egg`` directories in Python package directories should now have
  their resources detected properly and not as Python packages with the name
  ``*.egg``.
* ``site-packages`` directories are now recognized as Python resource package
  roots and no longer have their contents packaged under a ``site-packages``
  Python package.

New Features
^^^^^^^^^^^^

* ``pyoxidizer init`` now accepts a ``--pip-install`` option to pre-configure
  generated ``pyoxidizer.toml`` files with packages to install via ``pip``.
  Combined with the ``--python-code`` option, it is now possible to create
  ``pyoxidizer.toml`` files for a ready-to-use Python application!
* ``pyoxidizer`` now accepts a ``--verbose`` flag to make operations more
  verbose. Various low-level output is no longer printed by default and
  requires ``--verbose`` to see.

All Other Relevant Changes
^^^^^^^^^^^^^^^^^^^^^^^^^^

* Cargo packages updated to latest versions.

0.1.3
-----

Released on June 29, 2019.

Bug Fixes
^^^^^^^^^

* Fix Python refcounting bug involving call to ``PyImport_AddModule()`` when
  ``mode = module`` evaluation mode is used. The bug would likely lead to
  a segfault when destroying the Python interpreter. (#31)
* Various functionality will no longer fail when running ``pyoxidizer`` from
  a Git repository that isn't the canonical ``PyOxidizer`` repository. (#34)

New Features
^^^^^^^^^^^^

* ``pyoxidizer init`` now accepts a ``--python-code`` option to control which
  Python code is evaluated in the produced executable. This can be used to
  create applications that do not run a Python REPL by default.
* ``pip-install-simple`` packaging rule now supports ``excludes`` for excluding
  resources from packaging. (#21)
* ``pip-install-simple`` packaging rule now supports ``extra_args`` for adding
  parameters to the pip install command. (#42)

All Relevant Changes
^^^^^^^^^^^^^^^^^^^^

* Minimum Rust version decreased to 1.31 (the first Rust 2018 release). (#24)
* Added CI powered by Azure Pipelines. (#45)
* Comments in auto-generated ``pyoxidizer.toml`` have been tweaked to
  improve understanding. (#29)

0.1.2
-----

Released on June 25, 2019.

Bug Fixes
^^^^^^^^^

* Honor ``HTTP_PROXY`` and ``HTTPS_PROXY`` environment variables when
  downloading Python distributions. (#15)
* Handle BOM when compiling Python source files to bytecode. (#13)

All Relevant Changes
^^^^^^^^^^^^^^^^^^^^

* ``pyoxidizer`` now verifies the minimum Rust version meets requirements
  before building.

0.1.1
-----

Released on June 24, 2019.

Bug Fixes
^^^^^^^^^

* ``pyoxidizer`` binaries built from crates should now properly
  refer to an appropriate commit/tag in PyOxidizer's canonical Git
  repository in auto-generated ``Cargo.toml`` files. (#11)

0.1
---

Released on June 24, 2019. This is the initial formal release of PyOxidizer.
The first ``pyoxidizer`` crate was published to ``crates.io``.

New Features
^^^^^^^^^^^^

* Support for building standalone, single file executables embedding Python
  for 64-bit Windows, macOS, and Linux.
* Support for importing Python modules from memory using zero-copy.
* Basic Python packaging support.
* Support for jemalloc as Python's memory allocator.
* ``pyoxidizer`` CLI command with basic support for managing project
  lifecycle.
