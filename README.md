# retrieval-agent
An agentic RAG system for document retrieval, question rewriting, and answer generation.

## Overview
This project implements a retrieval-augmented generation (RAG) workflow that leverages LangChain and LangGraph to build an agentic system capable of retrieving relevant documents, refining user queries, and generating concise answers. The system is designed as a graph-based workflow, allowing conditional logic, dynamic tool usage, and flexible control over the response generation process.
This implementation is based on the [LangGraph RAG tutorial](https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph_agentic_rag/).
![RAG Workflow](https://langchain-ai.github.io/langgraph/tutorials/rag/assets/screenshot_2024_02_14_3_43_58_pm.png
)

## Key Features
1. **Document Fetching and Preprocessing**  
   - Collects web-based documents using loaders (e.g., `WebBaseLoader`) and converts them into LangChain Document objects.  
   - Preprocesses content for downstream semantic search, including cleaning and normalization.  

2. **Text Chunking for Semantic Search**  
   - Splits large documents into smaller chunks using `RecursiveCharacterTextSplitter`.  
   - Handles paragraphs, sentences, or fixed-size chunks to optimize vector-based retrieval and LLM input limits.  

3. **Retriever Tool Construction**  
   - Converts preprocessed document chunks into embeddings using OpenAI embeddings (`text-embedding-3-small`).  
   - Stores embeddings in an in-memory vector store for fast similarity search.  
   - Wraps the vector store in a retriever tool that can be invoked by the agent.  

4. **Agentic Workflow with LangGraph**  
   - Determines dynamically whether to call the retriever or respond directly to the user.  
   - Integrates multiple workflow nodes, including query generation, document retrieval, question rewriting, and answer generation.  

5. **Document Grading for Relevance**  
   - Evaluates whether retrieved documents are relevant to the user’s query using a binary grading model.  
   - Guides the workflow to either generate an answer or rewrite the query based on relevance.  

6. **Question Rewriting**  
   - Reformulates ambiguous or poorly matched questions to improve retrieval accuracy.  
   - Ensures that the agent can refine its queries and maximize retrieval relevance.  

7. **Answer Generation**  
   - Uses retrieved context to generate concise, factual answers.  
   - Limits responses to a few sentences for clarity while leveraging all relevant information.  
