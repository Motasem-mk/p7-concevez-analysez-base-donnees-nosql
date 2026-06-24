# P7 — NoSQL Database Design and Analysis

## Project Overview

This project was completed as part of the **OpenClassrooms Data Engineer path**.

The objective was to restore, analyze, and design a NoSQL database using **MongoDB** for a fictional non-profit organization called **NosCités**.

NosCités monitors short-term rental platforms in French cities in order to measure their impact on housing availability and provide transparency for public debate.

The project focuses first on short-term rental listings in **Paris during summer 2024**, in the context of the Olympic Games, and then extends the architecture to a multi-city setup involving **Paris** and **Lyon**.

---

## Business Context

NosCités experienced a major crash of its Paris rental database. A backup was available, but its reliability had to be verified before the Paris team could resume its analysis.

The project had three main objectives:

* restore the MongoDB database from a backup;
* analyze the integrity and consistency of the data;
* design a more resilient and scalable NoSQL architecture using replication and sharding.

The final goal was to help the organization recover from the incident and prevent similar problems in the future.

---

## Repository Structure

```text
p7-nosql-database-design-analysis/
├── README.md
├── presentation/
│   └── MotasemAbualqumboz_Concevez_et_analysez_une_base_de_donnees_NoSQL_090525.pptx
└── notebooks/
    └── polars.ipynb
```

---

## Main Deliverable

The official deliverable for this project was the PowerPoint presentation.

The presentation includes:

* the project context;
* the benefits of using NoSQL and MongoDB;
* MongoDB data restoration;
* document structure analysis;
* simple MongoDB queries and results;
* advanced analysis with PyMongo and Polars;
* BI connection with Tableau;
* replica set design;
* sharding strategy;
* Paris/Lyon geo-distribution logic.

The notebook `polars.ipynb` is included as supporting material for the advanced analysis part.

---

## Part 1 — MongoDB Restoration and Exploration

The first part of the project focused on restoring the Paris short-term rental dataset into MongoDB.

Main tasks:

* importing the Paris dataset into MongoDB;
* checking the structure of the documents;
* identifying the fields and data types;
* running first MongoDB queries;
* counting the total number of documents;
* counting listings with availability.

Main results:

* 95,885 Paris listing documents imported;
* 76,747 listings with `availability_365 > 0`.

---

## Why MongoDB / NoSQL?

MongoDB was suitable for this project because short-term rental data is semi-structured and may contain nested fields, arrays, and variable attributes depending on the listing.

Main benefits:

* flexible document schema;
* native support for nested documents and arrays;
* no need for complex joins;
* efficient querying on nested fields;
* horizontal scalability with sharding;
* high availability with replica sets;
* good integration with analytics and BI tools.

---

## Part 2 — NoSQL Data Analysis

The second part of the project focused on producing indicators and statistics to validate the backup data with the Paris team.

Simple MongoDB queries were used to calculate:

* the number of listings by room type;
* the top 5 listings with the highest number of reviews;
* the total number of unique hosts;
* the number and proportion of instant-bookable listings;
* hosts with more than 100 listings;
* the number and proportion of superhosts.

Main results:

* 71,979 unique hosts;
* 24 hosts with more than 100 listings;
* around 14% of hosts were superhosts;
* around 23% of listings were instant-bookable.

---

## Advanced Analysis with PyMongo and Polars

More complex calculations were performed using Python, PyMongo, and Polars.

The notebook `polars.ipynb` supports this part of the project.

Advanced analyses included:

* average monthly reservation rate by room type;
* median number of reviews across all listings;
* median number of reviews by host category;
* listing density by Paris neighborhood;
* neighborhoods with the highest monthly reservation rate.

Polars was used to perform efficient in-memory calculations and advanced aggregations.

---

## BI Connection

The project also included a Business Intelligence connection.

The goal was to make MongoDB data available to the Paris team through a BI tool so that they could continue their analysis more easily.

The presentation shows the connection between MongoDB and Tableau, as well as dashboard screenshots.

---

## Part 3 — Robust NoSQL Architecture Design

The third part of the project focused on designing a more resilient and scalable architecture.

The architecture had to address two main needs:

* protect the database from future incidents;
* improve local query performance for Paris and Lyon teams.

---

## Replication with MongoDB Replica Set

A replica set strategy was designed to improve data availability.

The setup included:

* one primary node;
* one secondary node;
* one arbiter node;
* automatic failover in case the primary node becomes unavailable.

Replication helps ensure:

* better fault tolerance;
* data redundancy across multiple nodes;
* continued access to data during incidents;
* safer recovery after server failure.

---

## Distribution with MongoDB Sharding

A sharding strategy was designed to distribute the data between Paris and Lyon.

Paris and Lyon listings were stored in a single collection called `listings`, with a `city` field used to distinguish the origin of each document.

The selected shard key was:

```text
city
```

The distribution strategy was based on geographic locality:

* Paris listings are stored on the Paris shard;
* Lyon listings are stored on the Lyon shard.

This approach improves local query performance for each team.

Distribution results:

* 95,885 documents stored on the Paris shard;
* 9,973 documents stored on the Lyon shard;
* 0 orphan documents.

---

## Technologies Used

* MongoDB
* Mongosh
* MongoDB Compass
* MongoDB Replica Set
* MongoDB Sharding
* PyMongo
* Polars
* Python
* Tableau
* PowerPoint

---

## Skills Demonstrated

This project demonstrates the following skills:

* restoring a MongoDB database;
* understanding NoSQL benefits and trade-offs;
* analyzing semi-structured documents;
* writing simple and advanced MongoDB queries;
* using Python, PyMongo, and Polars for analytical calculations;
* connecting MongoDB to a BI tool;
* designing a replica set strategy;
* designing a sharding strategy;
* reasoning about high availability, scalability, resilience, and local data access.

---

## Note

The raw datasets are not included in this repository.

The official project deliverable was the PowerPoint presentation. The Polars notebook is included as complementary material to document part of the advanced analysis.

---

## Author

Motasem Abualqumboz
Data Engineer
