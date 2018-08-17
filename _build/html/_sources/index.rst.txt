.. Decentralized Information Access documentation master file, created by
   sphinx-quickstart on Mon Aug  6 14:42:44 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to the DIA documentation!
=================================

.. toctree::
  :maxdepth: 3
  :numbered:
  :titlesonly:
  :caption: Contents:

  intro.rst
  setup.rst
  exchange-scrapers.rst
  blockchain-scrapers.rst
  retrieve-data.rst

Structure of this document
--------------------------
This document contains the documentation for DIA.
After a brief `Introduction to the DIA technical architecture` into the architecture of the system you can take a deep dive into.
both our `central database` that maintains an overview over financial data and
into our `system of oracles and other blockchain components`.
Finally, you can learn how to retrieve data from our system.

Features
--------

- Accurate pricing.
- Best execution.
- No middle men.

Installation
------------

We use docker for easy deployment.
Install a local version of our stack by running::

    $ docker-compose build

    $ docker-compose run


Indices and tables
==================

* :ref:`genindex`
* :ref:`search`
