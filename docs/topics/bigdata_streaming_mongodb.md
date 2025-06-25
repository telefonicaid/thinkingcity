Big data within [MongoDB](https://www.mongodb.com) clusters is mainly analyzed by means of the aggregation pipeline paradigm. Big Data analysis within the IoT Platform was previously handled using Hadoop clusters, primarily through the MapReduce paradigm and its integration with tools like Hue and Oozie. However, the platform has transitioned to a more agile and scalable architecture using MongoDB, eliminating the need for Hadoop and its ecosystem.

MongoDB allows developers and integrators to perform powerful data analysis using Python, leveraging libraries like pymongo and its native aggregation pipeline, which serves a similar purpose to MapReduce.

This document presents a step-by-step guide to creating Python-based data analysis tasks in MongoDB, simulating a word count example previously implemented with Hadoop Streaming.

# Setup
**IMPORTANT NOTE**: As an integrator, remember replacing the `admin` user appearing in the tutorial by your own user. Also replace `mongodb://localhost:27017` by the actual MongoDB connection string corresponding to your environment.

## Python code
You will need two Python scripts: one to insert sample data into MongoDB, and another to perform word count analysis using the aggregation pipeline.

```Python
$ cat insert_data.py
#!/usr/bin/env python

from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017")
db = client["demo_mongo"]
collection = db["text_data"]

# Insert sample documents
collection.insert_many([
    {"text": "Lorem ipsum dolor sit amet"},
    {"text": "Consectetur adipiscing elit"},
    {"text": "Dolore magna aliqua"},
    {"text": "Dolore sit amet dolor ipsum"}
])
print("Documents inserted.")
```

```Python
$ cat wordcount.py
#!/usr/bin/env python

from pymongo import MongoClient

client = MongoClient("mongodb://localhost:27017")
db = client["demo_mongo"]
collection = db["text_data"]

pipeline = [
    {"$project": {"words": {"$split": ["$text", " "]}}},
    {"$unwind": "$words"},
    {"$group": {"_id": "$words", "count": {"$sum": 1}}},
    {"$sort": {"count": -1}}
]

for doc in collection.aggregate(pipeline):
    print(f"{doc['_id']}: {doc['count']}")
```
These files should be executed from your Python environment. They replicate the logic of the classic WordCount MapReduce example, now using MongoDB’s aggregation pipeline.

## Data
You can insert any plain text into the text_data collection. Here’s how to run the data insertion script:

```
$ python insert_data.py
Documents inserted.
The inserted documents will follow this structure:
{"text": "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."}
```
You can inspect the collection using [MongoDB Compass](https://www.mongodb.com/es/products/tools/compass) or your preferred tool.

# Data Analysis with MongoDB Aggregation
Instead of defining a streaming MapReduce job in Hue, now you can run your analysis script locally or integrate it into modern orchestration tools.

Run the wordcount.py script:

```Python
$ python wordcount.py
```

Expected output:

```Python
Dolore: 2
amet: 2
ipsum: 2
dolor: 1
Lorem: 1
sit: 1
...
```
This output demonstrates how MongoDB can replicate MapReduce-like behavior more simply and efficiently.

# Advanced Workflows
More complex workflows—previously handled through Oozie or chained MapReduce jobs—can now be implemented using tools that better integrate with MongoDB:

* Python scripts orchestrated with tools like Airflow, Luigi, or custom schedulers to manage data ingestion, transformation, and export tasks

* MongoDB triggers and change streams to create event-driven workflows that react in real time to database changes

* Scheduled cron jobs to automate routine operations such as backups, aggregation rollups, or data archival

These tools provide flexibility and modularity without the need for Hadoop components.


# Conclusion
The transition from Hadoop to MongoDB streamlines Big Data processing and reduces infrastructure complexity. MongoDB’s aggregation pipeline, together with Python integrations, allows for real-time analysis, simpler deployments, and faster development cycles.
By replacing Hadoop and Hue with MongoDB and modern Python-based workflows, the IoT platform achieves greater scalability, maintainability, and performance in its Big Data module.
