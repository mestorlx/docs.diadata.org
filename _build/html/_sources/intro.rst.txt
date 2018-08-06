Introduction to the DIA technical architecture
==============================================

Overview
--------

DIA is split up in two architectural components:

1. The central off-chain database with all historical data
2. The on-blockchain oracles and verification mechanisms.

Central database
----------------
The central database collects financial data using its *scrapers* and stores them in a stream.
We use `Apache Kafka <https://kafka.apache.org/>`_ to provide a reliant, performance oriented, and redundant stream database.
A Kafka database is organized using *topics*.
These topics are used to consume data as an application.
Data producers write key-value messages into the database. Its message structure is simply defined::

  type KafkaMessage interface {                                                      
    KafkaKey() []byte                                                                
    KafkaValue() ([]byte, error)                                                     
  }

The database holds a collection of filters, that generate meaningful metrics from that raw data,
for example an average value over the last minute or an index over several currencies.

Blockchain oracles
------------------
The blockchain side of DIA uses oracles to supply any smart contract with financial data.
