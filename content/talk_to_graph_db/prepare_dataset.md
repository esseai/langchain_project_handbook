+++
title = 'Preparing DataSet'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 2
+++

### Preparing DataSet

<!-- Ref > https://gitlab.com/digiits/larklex/-/blob/main/docs/240815_fushun.md -->

To ensure the confidentiality of client data, I have opted to simulate a dataset that represents profiles of individuals. This simulated dataset includes key attributes such as `names`, `ages`, `genders`, and `incomes`. Additionally, I have created a corresponding list of educational backgrounds that aligns with the first dataset, detailing each individual's education about the `schools` they attended, `majors`, and `degrees`. 

I'm using Perplexity.ai to generate the data set, with the following `prompt`

```
Generate a dataset of 20 rows, with the following columns: name, age, gender, income. The data should be realistic and diverse, and the income should be between 50000 and 120000. the final is in csv format
```

```csv
name,age,gender,income
Alice Johnson,34,Female,75000
Brian Smith,28,Male,58500
Carla Martinez,45,Female,92300
David Lee,30,Male,65000
Emily Chen,39,Female,85600
Frank Wilson,50,Male,110000
Grace Kim,26,Female,52400
Henry Brown,47,Male,78200
Isabella Garcia,31,Female,63700
James Rodriguez,29,Male,55900
Karen Davis,42,Female,95800
Liam Thompson,36,Male,70500
Mia Anderson,27,Female,59300
Noah Taylor,38,Male,88100
Olivia Martinez,33,Female,81400
Paul White,44,Male,105000
Quinn Harris,25,Female,54200
Ryan Clark,40,Male,66800
Sophia Lewis,35,Female,90500
Tyler Young,48,Male,115000
```

Then I use the following `prompt` to generate the education dataset

```
then generate a dataset of 20 rows, with the following columns: name, school, major, degree. the data must contain the above 4 columns. The data should be realistic and diverse, and the degree should be between Bachelor, Master, and Doctor.
```

```csv
name,school,major,degree
Alice Johnson,University of California, Berkeley,Computer Science,Bachelor
Brian Smith,Harvard University,Business Administration,Master
Carla Martinez,Stanford University,Psychology,Bachelor
David Lee,Yale University,Electrical Engineering,Doctor
Emily Chen,University of Michigan,Ann Arbor,Biology,Bachelor
Frank Wilson,Cornell University,Chemistry,Master
Grace Kim,University of Texas at Austin,Nursing,Bachelor
Henry Brown,Columbia University,Political Science,Master
Isabella Garcia,UCLA,Art History,Bachelor
James Rodriguez,Duke University,Literature,Doctor
Karen Davis,Northeastern University,Cybersecurity,Bachelor
Liam Thompson,Penn State University,Agricultural Science,Master
Mia Anderson,University of Florida,Environmental Science,Bachelor
Noah Taylor,Michigan State University,Mathematics,Bachelor
Olivia Martinez,Wisconsin-Madison University,Kinesiology,Master
Paul White,Rice University,Aerospace Engineering,Bachelor
Quinn Harris,Syracuse University,Sociology,Bachelor
Ryan Clark,Boston University,MBA (Business),Master
Sophia Lewis,Vanderbilt University,Nutrition Science,Bachelor
Tyler Young,Cleveland State University,Law,Doctor
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
