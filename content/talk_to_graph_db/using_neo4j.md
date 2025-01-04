+++
title = 'Using Neo4j as Graph Database'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 3
+++

### Using `neo4j` as Graph Database

#### Installing `neo4j` with Docker

We would need to install `neo4j` with docker and persist the data to the local disk.

```sh
docker run --restart always --name=neo4j \
    --publish=7474:7474 --publish=7687:7687 \
    --env NEO4J_AUTH=neo4j/neo4j_password \
    --volume /home/USER/neo4j_storage/data:/data \
    --volume /home/USER/neo4j_storage/logs:/logs \
    --volume /home/USER/neo4j_storage/import:/import \
    neo4j:latest
```

> Note: we're going to import the dataset into the database from CSV files, which would be stored in the `/home/USER/neo4j_storage/import` directory. Therefore, we need to create this directory before running the container. And copy the CSV files into this directory.

After the container is running, we can access the `neo4j` dashboard at `http://IP_ADDRESS:7474`.

> Security Note: The `neo4j` dashboard is not secure, so we should not use it in production environment. Even in the local environment, we should change the default password.

You would see the following screen after logging in with the default credentials (username: `neo4j`, password: `neo4j_password`). 

![](images/2024-12-31-18-14-52.png)

All the data would be stored in the `/home/USER/neo4j_storage/data` directory permanently. In order to make this document simple, I'm going to use the default database.

#### Importing Data

There are multiple ways to import data into the database. We can use the `neo4j` dashboard to import the data, or use the `cypher` script to import the data. I list the simple steps to import the data into the database from dashboard.

Make sure you have copied the CSV files into the `/home/USER/neo4j_storage/import` directory.

From the dashboard, perform the following steps:

1. Import Income Data:
```sh
LOAD CSV WITH HEADERS FROM 'file:///income.csv' AS row
CREATE (:Person {name: row.Name, age: toInteger(row.Age), gender: row.Gender, income: toInteger(row.Income)});
```

2. Import Education Data:
```sh
LOAD CSV WITH HEADERS FROM 'file:///education.csv' AS row
CREATE (:Education {name: row.Name, school: row.School, major: row.Major, degree: row.Degree});
```

3. Create Relationships:
```sh
MATCH (p:Person), (e:Education)
WHERE p.name = e.name
CREATE (p)-[:EDUCATED_AT]->(e);
```
