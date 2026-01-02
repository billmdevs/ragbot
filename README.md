# Simple RAG-based bot

Simple Retrieval Augmented Generation (RAG) based bot in Python. It allows users to ask questions about multiple PDF documents. It extracts text from PDFs, creates embeddings, builds a vector store, and uses a conversational retrieval chain to answer user queries based on the document content.


# **Scalability Improvements for Large Document Sets**
My approach from here will change drastically if my knowledge base was 1k documents or 1M documents.

Here are some considerations and details on how I will approach them.

**Distributed Processing:** I would implement a distributed system using technologies like Apache Spark or Dask for parallel processing of documents and use cloud services like AWS Lambda or Google Cloud Functions for serverless, scalable document processing.


**Database for Document Storage:** I would the in-memory storage with a distributed database like Cassandra or MongoDB for document metadata and content.


**Chunking and Embedding:** I would process documents in batches, possibly using a message queue system like RabbitMQ or Apache Kafka to manage the workload and use asynchronous processing to handle embedding generation in parallel.

**Caching:** I would implement a caching layer (e.g., Redis) to store frequent queries and their results, reducing the load on the vector database.


**Indexing Strategy:** I would implement incremental indexing to handle updates and additions to the document set without reprocessing everything and use hierarchical indexing techniques for ultra-large datasets.


**Query Optimization:** I would implement query planning and optimization techniques to handle complex queries efficiently and use approximate nearest neighbor (ANN) search algorithms for faster retrieval in very large datasets.


**Monitoring and Scaling:** I would implement comprehensive monitoring and auto-scaling solutions to handle varying loads and use orchestration tools like Kubernetes for orchestrating and scaling the various components of the system.

<br /><br />

# **Latency Optimizations: Embedding Models and Vector Databases I would choose for speed and accuracy balance.**

**Embedding Models:** OpenAI's text-embedding-ada-002, BERT-based models (e.g., DistilBERT, MiniLM), Sentence-BERT models, FastText.
**Vector Databases:** Pinecone, Weaviate.

<br /><br />

# **Cost Estimation for 10k and 1M Requests**

## **Cost Breakdown**

**Embedding Generation**

    - OpenAI API: $0.0001 per 1K tokens
    - Cost per document: $0.0001 * (1000/1000) = $0.0001
    - Cost per query: $0.0001 * (100/1000) = $0.00001


**Chat Model (GPT-3.5-turbo)**

    - $0.002 per 1K tokens
    - Assuming 500 tokens per response: $0.001 per query


**Vector Database (Pinecone S1 Plan)**

    - $0.12 per hour (assumed for this calculation)



## **Cost Estimation**

**For 10k requests**
    - Embedding cost: 10,000 * $0.00001 = $0.1 
    - Chat model cost: 10,000 * $0.001 = $10
    - Pinecone cost (assuming queries spread over a month): $0.12 * 24 * 30 = $86.4

#### Total estimated cost for 10k requests: $96.5

**For 1M requests**: 
    - Embedding cost: 1,000,000 * $0.00001 = $10
    - Chat model cost: 1,000,000 * $0.001 = $1,000
    - Pinecone cost (assuming higher tier needed): ~$700 per month

#### Total estimated cost for 1M requests: $1,710
Note: These are rough estimates. As engineers we know that sometimes stuff that we didn't predict happens but these are my best estimates.
