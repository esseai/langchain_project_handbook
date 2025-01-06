+++
title = 'Configuring Neo4j with LangChain'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 5
+++

### Configuring `neo4j` with `langchain`

To communicate with a Neo4j graph database through a Large Language Model (LLM), you can leverage integration frameworks such as LangChain. Here’s how you can set up this interaction:

#### Integrate Neo4j with LangChain

LangChain provides a robust framework for integrating LLMs with various data sources, including Neo4j. You can install the necessary packages using pip:

```bash
# pip install langchain langchain-community langchain-neo4j neo
pip install neo4j langchain-neo4j
```

This installation will allow you to utilize Langchain's capabilities to interact with your Neo4j database.






#### Set Up Connection to Neo4j

You need to establish a connection between your application and the Neo4j database. This typically involves specifying the database URI and authentication credentials.

```python
from langchain_neo4j import Neo4jGraph, Neo4jVector, GraphCypherQAChain
graph = Neo4jGraph(
    url="bolt://NEO4J_HOST:7687",
    username="neo4j",
    password="neo4j_password",
)
```

<!-- 
#### Use Cypher Queries
Once connected, you can use Cypher queries to perform operations on your graph database. You can formulate queries based on user input or predefined templates.

```python
query = "MATCH (p:Person) RETURN p.name, p.income"
results = neo4j_graph.run(query)
``` -->

#### Incorporate LLM for Natural Language Processing
You can utilize an LLM (like Mistral's models from HuggingFace for 100% free and open-source) to process natural language queries from users and convert them into Cypher queries that can be executed against the Neo4j database.

> Note: You need to set up your HuggingFace API token in your environment variable before running the code.

```python
import os
HUGGINGFACEHUB_API_TOKEN = os.getenv("HUGGINGFACEHUB_API_TOKEN")

from langchain_huggingface import HuggingFaceEndpoint
repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
llm = HuggingFaceEndpoint(
    repo_id = repo_id,
    temperature = 0.5,
    huggingfacehub_api_token=HUGGINGFACEHUB_API_TOKEN,
    max_new_tokens = 250,
)
```

#### Implement Retrieval-Augmented Generation (RAG)
You can enhance the interaction by implementing Retrieval-Augmented Generation (RAG), which allows the LLM to ground its responses in the factual data stored in the graph. This helps reduce misinformation or "hallucinations" by ensuring that the model's outputs are based on verified data.

- Use vector search capabilities of Neo4j to find relevant nodes based on user queries.
- Combine results with LLM-generated content for comprehensive answers.

#### Explore Graph Data
You can also visualize and explore the graph data using tools like Neo4j Bloom or integrate it into your application for dynamic interactions.


#### The Complete Code

```py
from langchain_neo4j import Neo4jGraph, Neo4jVector, GraphCypherQAChain
graph = Neo4jGraph(
    url="bolt://NEO4J_HOST:7687",
    username="neo4j",
    password="neo4j_password",
)

import os
HUGGINGFACEHUB_API_TOKEN = os.getenv("HUGGINGFACEHUB_API_TOKEN")

from langchain_huggingface import HuggingFaceEndpoint
repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
llm = HuggingFaceEndpoint(
    repo_id = repo_id,
    temperature = 0.5,
    huggingfacehub_api_token=HUGGINGFACEHUB_API_TOKEN,
    max_new_tokens = 250,
)

chain = GraphCypherQAChain.from_llm(
    llm, 
    graph=graph,
    verbose=True,
    allow_dangerous_requests=True,
    )

print(chain.invoke("What is the income of Olivia Martinez?"))
```