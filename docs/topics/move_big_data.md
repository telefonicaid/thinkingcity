# <a name="top"></a>How to massively move data from/to the platform (Big Data)
Moving massive data from or to the ThinkingCity platform involves interacting with [**MongoDB**](https://www.mongodb.com).

MongoDB is a document-oriented NoSQL database that stores data in flexible, JSON-like documents. It provides native support for bulk insertions, querying, and aggregation, making it suitable for scalable Big Data processing within the ThinkingCity platform.

In this architecture, data is stored as collections in MongoDB databases. For high-throughput data ingestion and export, MongoDB supports various tools and APIs, such as the native `mongoimport/mongoexport`, `mongodump/mongorestore`, and Python-based pipelines using `pymongo`.

There are several ways to interact with the MongoDB-based storage. Below are the methods supported by the ThinkingCity platform.


## Methods
### Using MongoDB Compass
This method is mainly oriented to **non-automated integrators** (i.e. human operators), since [MongoDB Compass](https://www.mongodb.com/products/compass) is a GUI client for MongoDB.

Compass provides a visual interface to browse, query, and modify documents. It is particularly useful for quickly uploading or downloading datasets, inspecting collection structures, and managing indexes.

Typical I/O operations—such as inserting new records, exporting query results, or deleting collections—can be done via Compass with no need to write manual queries.

Accessing Compass requires valid credentials, typically provided by the ThinkingCity platform administrators. These user accounts are tenant-specific and have restricted access to the collections relevant to each client.

[Top](#top)

### Using a ETL process
ETL stands for Extract, Transform, and Load. It refers to processes responsible for moving and transforming data before it is stored or after it is extracted.

The ThinkingCity platform provides access to a processing environment where **integrators** can deploy ETL jobs written in **Python** (or other languages), typically using the `pymongo` library to interface with MongoDB.

Here’s a simplified example in Python:

```python
from pymongo import MongoClient

client = MongoClient("mongodb://user:pass@host:27017/")
db = client["iot_data"]
collection = db["measurements"]

# Insert sample data
collection.insert_many([
    {"device_id": "sensor01", "timestamp": 1721820200, "value": 42},
    {"device_id": "sensor02", "timestamp": 1721820260, "value": 38}
])
```
Data can also be loaded from external sources (e.g., CSV files, SQL databases, APIs) and pushed to MongoDB using similar patterns.

Please contact the ThinkingCity platform team to request access to the ETL server, including necessary authentication details and configuration files.

[Top](#top)
