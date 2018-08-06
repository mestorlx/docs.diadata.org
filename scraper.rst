Write your own Scraper
======================


Add your own scraper
--------------------
In order to add your own scraper for a new data source, you must adhere to our format.
We use Go modules for our scrapers.
A scraper must have a function ``ScrapePair(pair priceCollection.Pair)`` that can be called from our system.
It returns a ``PairScraper``.
A simple example looks like this:
::

  func (s *BitfinexScraper) ScrapePair(pair priceCollection.Pair) (PairScraper, error) {
    // scraper code here
  }
