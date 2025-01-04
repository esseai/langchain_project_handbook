+++
title = 'Talk to Your GraphDB'
type = "chapter"
weight = 7
date = 2024-12-27T06:48:46-05:00
draft = false
+++

In summer of 2024, I received a request from our Sales, who manages the engagement with public service. The customer has multiple diementions of dataset and what they want is like

1. Link the different diementaional dataset together
2. Gives them a better graphical visualization of data relationships
3. As they don't have much technical skills, they can't handle SQL script and wish to "talk" to the database in their native language. Then the application responds the printable data-sheet

What I can think is to enable three things and combine them together

1. Use `neo4j` as graph database, in docker for easier operation management
2. Enable `cypher` script, which can be treated as a plugin of Large Language Model (LLM) with `neo4j`
3. Use `ollama` to orchestrate LLM model

### Business Scenario

I'm going to simulate and simplify the business scenario. For example, the customer has a dataset of `fushun` city, which contains multiple dimensions of data, such as `population`, `economy`, `education`, `transportation`, etc. I just simulate to use 2 kinds of data, `population` and `education`, in which `population` is a table of `name`, `age`, `gender`, `income`, etc. and `education` is a table of `name`, `school`, `major`, `degree`, etc.


