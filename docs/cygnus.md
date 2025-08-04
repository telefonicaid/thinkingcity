Cygnus is a connector in charge of persisting certain sources of data in certain configured third-party storages, creating a historical view of such data.

Internally, Cygnus is based on [Apache Flume](http://flume.apache.org/), a technology addressing the design and execution of data collection and persistence *<i>agents</i>*. An agent is basically composed of a listener or source in charge of receiving the data, a channel where the source puts the data once it has been transformed into a Flume event, and a sink, which takes Flume events from the channel in order to persist the data within its body into a third-party storage.

Cygnus is designed to run a specific Flume agent per source of data.

Current stable release is able to persist the following sources of data in the following third-party storages:

* NGSI-like context data in:

  * [MongoDB](https://www.mongodb.org/), the NoSQL document-oriented database.
  * [Kafka](http://kafka.apache.org/), the publish-subscribe messaging broker.
  * [DynamoDB](https://aws.amazon.com/dynamodb/), a cloud-based NoSQL database by [Amazon Web Services](https://aws.amazon.com/).
  * [PostgreSQL](http://www.postgresql.org/), the well-known relational database manager.

* Twitter data in:

  * [MongoDB](https://www.mongodb.org/), the NoSQL document-oriented database.

## Documentation and API

FIWARE Cygnus:

* [Documentation](https://github.com/telefonicaid/fiware-cygnus/blob/master/README.md)
* [Source code](https://github.com/telefonicaid/fiware-cygnus)
