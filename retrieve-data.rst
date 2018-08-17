Retrieve Data from DIA for your DApp
====================================

DIA provides several data sources that are mirrored into oracles.
These data points can also be retrieved using our REST API.
In the following we will show how to retrieve data through this API.

Read ECB data from our REST API
-------------------------------

The European Central Bank provides daily closing spot prices for the exchange rates between EUR and other important currencies worldwide.
To retrieve the latest data points collected by our system point a GET request at::

   https://api.diadata.org/v1/ecb

This results in the exchange price between EUR and the latest currency that was added::

   {"Result":{"offset":92,"messages":[[{"Symbol":"EURTHB","Value":37.822,"Name":"EURTHB","Time":"2018-08-16T00:00:00Z","Source":{"Name":"ECB"}}]]}}

The data format lisst the currency pair, the value of the other currency in EUR, its name, the time it was scraped by our database and a description of the original data source.
If you want to retrieve other currencies look at the ``offset`` value in the reply and ask the API::

   https://api.diadata.org/v1/ecb?offset=91

By that, you receive the second-to-last currency we added in our database.
