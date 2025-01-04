+++
title = 'Configuring LLM'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 4
+++

### Configuring LLM

I recommend to either use `ollama` or directly connect to HuggingFace's LLM model.

#### Using `ollama`

Please refer to Chapter 4 - Document Summarization - Software Environment for more details.

#### Using HuggingFace's LLM model

Before using HuggingFace's LLM model, you need to get the API token from HuggingFace.

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
