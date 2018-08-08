Write your own Scraper
======================


Add your own scraper
--------------------
In order to add your own scraper for a new data source, you must adhere to our format.
We use Go modules for our scrapers, so that each data provider is living as an independent module.
A scraper for cryptocurrencies must have a function ``ScrapePair(pair priceCollection.Pair)`` that can be called from our system.
It returns a ``PairScraper``.

Let's assume you want to scrape a data source that provides trade information.
Create a new file in ``scrapers/`` and call it ``MyScraper.go``.
At first, its content looks like this::

  func (s *MyScraper) ScrapePair(pair priceCollection.Pair) (PairScraper, error) {
    // scraper code here
  }

The ``PairScraper`` interface is defined as a collection of methods.
The most important one is returning a channel which is filled with every trade the scraper witnesses::

  // PairScraper receives trades for a single pc.Pair from a single exchange.
  type PairScraper interface {
    io.Closer

    // Channel returns a channel that can be used to receive trades
    Channel() chan *priceCollection.Trade

    // Error returns an error when the channel Channel() is closed
    // and nil otherwise
    Error() error

    // Pair returns the pair this scraper is subscribed to
    Pair() priceCollection.Pair
  }
 
The other methods are mainly for Error handling, maintenance and shutdown.
Our system is running the data scraper on our premises as an example.
Of course, it is also possible to host your own data provider but in this simple example we assume that MyScraper is hosted on DIA servers.

For running the scraper, you have to create a go module located in the ``cmd/`` directory.
According to our naming convention, it will be called ``myScraperConnector`` and consist of a directory with that name containing a file also named like this and ending in ``.go``.
Its content at first is organized like this::

  package main
                                                                                
  import (
    "github.com/diadata-org/TODO/scrapers"
    "github.com/segmentio/kafka-go"
    "github.com/tkanos/gonfig"
    "log"
    "os"
    "sync"
  )
                                                                                  
  // handleTrades delegates trade information to Kafka
  func handleTrades(ps scrapers.PairScraper, wg *sync.WaitGroup, w *kafka.Writer) {
    for {
      t, ok := <-ps.Channel()
                                                                                  
      if !ok {
        // log error and return
        if ps.Error() != nil {
          log.Printf("Error: %s\n", ps.Error())
        } else {
          log.Printf("PairScraper for %s was shut down by user", ps.Pair())
        }
        wg.Done()
        return
      }
      priceCollection.WriteMessage(w, t)
    }
  }

This is the basic structure of these files.
Build your go package by calling::

  go install

from the directory the ``myScraperConnector`` is located in.
