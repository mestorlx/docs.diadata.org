Write your own blockchain scraper
=================================


Add your own blockchain scraper
-------------------------------
In order to add your own scraper for a blockchain supply source, you must adhere to our format.
We use Go modules for our scrapers, so that each data provider is living as an independent module.

You must provide a Dockerfile for your blockchain client.
Add an entry into the docker-compose file so that your Dockerfile is automatically called.

A Go code sample similar to the bitcoin example in the ``cmd`` folder should be supplied.
For sending supply data to DIA, you can use ``SendSupply`` in the ``ApiClient.go`` file.

This is the basic structure of these files.
Run your Docker instance by calling::

   docker run <your instance>

from the main directory.
