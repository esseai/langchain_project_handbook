+++
title = 'Configuring LLM'
date = 2025-01-03T22:04:12-05:00
draft = false
weight = 4
+++


### Configuring the Large Language Model (LLM)

When it comes to configuring a Large Language Model (LLM), I recommend two primary approaches: using Ollama or directly connecting to Hugging Face’s LLM model.

#### Using Ollama
For detailed instructions on utilizing Ollama, please refer to Chapter 4, titled "Document Summarization - Software Environment." This chapter provides comprehensive guidance on setting up and integrating Ollama into your workflow, ensuring a smooth implementation process.

Please refer to Chapter 4 - Document Summarization - Software Environment for more details.

#### Using Hugging Face’s LLM Model

If you prefer to use Hugging Face’s LLM model, there are a few essential steps to follow:

1. Obtain an API Token: Before you can access Hugging Face's LLM model, you must first acquire an API token. This token is necessary for authenticating your requests and ensuring secure access to the model.
2. Sign Up for an Account: If you do not already have an account with Hugging Face, you will need to create one. This process typically involves providing your email address and creating a password.
3. Generate the API Token: Once your account is set up, navigate to the API settings section on the Hugging Face website. Here, you can generate your unique API token, which will be used in your application to connect to the LLM.
4. Integrate the Token into Your Application: After obtaining the API token, make sure to integrate it into your application code. This step is crucial for enabling your application to communicate with Hugging Face's services effectively.

Here is an example of how to integrate HuggingFace's LLM model into your application:

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
