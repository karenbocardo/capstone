# Capstone Project 2023

## Description

As a Data Engineer you will need to design and implement some part of the data platform for a data analytics team. Customers have some data journaled from a streaming application named Kafka. The data is saved into a file system every day. The requirement is that this data is enriched and then a snapshot is created and updated every day. 

The **journaled** data has the following JSON structure:

```json
{
    “Id”: 10000,
    “active”: true,
    “subscription”: “Premium”, 
    “customer_first_name” : “Juan”
    “customer_last_name”: “Sanchez”,
    “cost”: 100
    “start_date” : “2022-11-01”	
    “end_date” : “2023-11-02”	
}

```

**Enriched dataset** is in parquet with the following structure:

```
subscription String
numberOfChannels Long
extras Map<String, String>
```

## Stages

1. Create data generators : Create around 100 entries for journal data for 3 consecutive days. Id range should be between 1 and 250.
2. Create data for 10 types of subscriptions. 
3. Use Spark with airflow and execute a job every 10 minutes (simulating it runs every day), this job will create a **snapshot** of the data and will contemplate the current snapshot.
4. Save the snapshot dataset in a filesystem, it can be local or hdfs. In **parquet** format.  
5. You can use Docker or local installation, if you feel comfortable you can use a cloud provider.
6. Add test cases for the produced dataset.



## Snapshot description

1. If there is no previous snapshot it will execute all the journal data.
2. If there is a current snapshot it will build on top of that. 
3. A snapshot does not contain duplicate keys, this means that if an existing key is found in more recent journal data then the old one will be replaced.
4. A snapshot does not delete old keys.
5. The enrichment is performed with a join.

Think about:
- Is it convenient to ingest all fields to the data warehouse? **PII**?
- Is the source data going to be there forever?
- What about the data in kafka? **TTL**?
- What happens if you need to change the snapshot structure? Should you process everything?

## Concepts

- PII (personal identifiable information)
- TTL (time to live)
- Duplicates (remover / take last /**aggregate** both / etc) 
- **Backfill**
- **Null policy**

## Deliverable

Create a personal github project. Add readme with detailed description of the project. 

---
> Important definitions are highlighted in bold.