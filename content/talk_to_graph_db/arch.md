+++
title = 'Architecture'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 2
+++

### Architecture

#### Proposed Solution for Data Management and Visualization

To address the client's needs, I propose implementing an approach that combines the following elements:

- Utilizing `neo4j` as a Graph Database and Vector Store: We will leverage `neo4j` not only as a graph database but also as a Vector Store to import the client's datasets. This will facilitate advanced graph visualizations, allowing for a clearer understanding of data relationships.

- Running `neo4j` as a Service in Docker: By deploying Neo4j within a Docker container, we can provide a reliable and scalable graph database service. This setup will ensure that the database is easily accessible and manageable, enhancing performance and security.

- Integrating the `langchain_neo4j` library: To enable seamless communication between large language models (LLMs) and the graph database, we will install and integrate the `langchain_neo4j` library. This integration will allow the LLM to interact with the database using natural language queries, making data retrieval intuitive for users with limited technical skills.

- Using `ollama` to Orchestrate LLM Models: We will employ `ollama` to orchestrate the LLM models effectively. This tool will help manage interactions between the LLM and the Neo4j database, ensuring smooth operation and efficient processing of user queries.


```plantuml
{{< plantuml >}}

actor User
node LLM
database Neo4j

User -> LLM: Ask a question
LLM -> Neo4j: Query the graph database \nthrough `langchain_neo4j`
Neo4j -> LLM: Return the result
LLM -> User: Answer the question

note top of Neo4j: source data imported from \n`income.csv` \n`education.csv`
note bottom of Neo4j: vectorStore
note bottom of LLM: orchstrated by ollama

{{< /plantuml >}}
```

Figure 7.1: The architecture of the application


### Preparing DataSet

<!-- Ref > https://gitlab.com/digiits/larklex/-/blob/main/docs/240815_fushun.md -->

To ensure the confidentiality of client data, I have opted to simulate a dataset that represents profiles of individuals. This simulated dataset includes key attributes such as `names`, `ages`, `genders`, and `incomes`. Additionally, I have created a corresponding list of educational backgrounds that aligns with the first dataset, detailing each individual's education about the `schools` they attended, `majors`, and `degrees`. 

I'm using Perplexity.ai to generate the data set, with the following `prompt`

```
Generate a dataset of 20 rows, with the following columns: Name, Age, Gender, Income. The data should be realistic and diverse, and the income should be between 50000 and 120000.
```

```csv
Name,Age,Gender,Income
Alice Johnson,28,Female,55000
Bob Smith,34,Male,72000
Catherine Lee,22,Female,48000
David Brown,45,Male,95000
Eva Green,31,Female,60000
Frank White,29,Male,52000
Grace Chen,38,Female,78000
Henry Adams,50,Male,120000
Ivy Patel,27,Female,49000
James Wilson,40,Male,85000
Katherine Davis,33,Female,67000
Liam Thompson,25,Male,53000
Mia Garcia,30,Female,62000
Nathan Martinez,36,Male,74000
Olivia Taylor,24,Female,50000
Paul Robinson,47,Male,110000
Quinn Harris,29,Female,58000
Ryan Clark,39,Male,90000
Sophia Lewis,26,Female,51000
Thomas Walker,42,Male,99000
```

Then I use the following `prompt` to generate the education dataset

```
Generate a dataset of 20 rows, with the following columns: Name, School, Major, Degree. The data should be realistic and diverse, and the degree should be between Bachelor's, Master's, and Doctor's.
```

```csv
Name,School,Major,Degree
Alice Johnson,Havard University,Psychology,Bachelor's
Bob Smith,Yale University,Business Administration,Bachelor's
Catherine Lee,UCLA,Biology,Bachelor's
David Brown,Cambridge University,Literature Master's 
Eva Green,Northeastern University,Chemistry,Bachelor's 
Frank White,Penn State University,Civil Engineering,Bachelor's 
Grace Chen,UChicago,Economics,Bachelor's 
Henry Adams,MIT Computer Science,Bachelor's 
Ivy Patel,Duke University,Nursing,Bachelor's 
James Wilson,Cornell University,Agriculture,Bachelor's 
Katherine Davis,UCBerkeley,Sociology,Bachelor's 
Liam Thompson,Rice University,Aerospace Engineering,Bachelor's 
Mia Garcia,Texas A&M University,Psychology,Bachelor's 
Nathan Martinez,UCLA,Cultural Studies,Bachelor's 
Olivia Taylor,Wisconsin-Madison University,Linguistics,Bachelor's 
Paul Robinson,UVA,Higher Education Master's 
Quinn Harris,NW University,Psychiatry Master's 
Ryan Clark,UConn,Chemistry Bachelor's 
Sophia Lewis,Nebraska University,Chemistry Bachelor's 
Thomas Walker,Wisconsin-Madison University,Law Bachelor's 
```

Save the two datasets into two separate CSV files, with the following names:

- `income.csv`
- `education.csv`

<!-- 
#### Hidden Appendix

```plantuml

actor User
node LLM
database Neo4j

User -> LLM: Ask a question
LLM -> Neo4j: Query the graph database \nthrough `langchain_neo4j`
Neo4j -> LLM: Return the result
LLM -> User: Answer the question

note top of Neo4j: source data imported from \n`income.csv` \n`education.csv`
note bottom of Neo4j: vectorStore
note bottom of LLM: orchstrated by ollama

``` -->
