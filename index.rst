.. Decentralized Information Access documentation master file, created by
   sphinx-quickstart on Mon Aug  6 14:42:44 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Decentralized Information Access's documentation!
============================================================

.. toctree::
   :maxdepth: 2
   :caption: Contents:

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

Write your own Scraper
----------------------

We use a kafka database for processing all our data.
Every trade or other data point is stored as an element of the Kafka stream.
The database holds a collection of filters, that generate meaningful metrics from that raw data,
for example an average value over the last minute or an index over several currencies.

In order to add your own scraper for a new data source, you must adhere to our format.
We use Go modules for our scrapers.
A scraper must have a function ``ScrapePair(pair priceCollection.Pair)`` that can be called from our system.
It returns a ``PairScraper``.

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
