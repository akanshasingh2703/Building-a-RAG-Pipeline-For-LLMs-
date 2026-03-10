## 🤖 Retrieval-Augmented Generation (RAG) Pipeline for LLMs

### 🎯 Project Goal
The goal of this project was to build a **Retrieval-Augmented Generation (RAG) pipeline** that enhances Large Language Models (LLMs) by allowing them to retrieve relevant external knowledge before generating answers.  

Traditional LLMs rely only on the data they were trained on, which can lead to **hallucinations or outdated information**. This project addresses that limitation by combining **retrieval systems with transformer-based models**, enabling the system to generate responses grounded in real-world data.

The objective was to create an end-to-end pipeline capable of:

- Retrieving external knowledge from Wikipedia
- Splitting large documents into smaller semantic chunks
- Converting text into embeddings for similarity search
- Retrieving the most relevant information for a user query
- Generating accurate answers using a question-answering model

---

### ⚙️ Approach

The system was implemented using **Python, Hugging Face Transformers, Sentence Transformers, and FAISS**.

#### 1. Knowledge Retrieval
- Used the **Wikipedia API** to retrieve full article content based on a user-provided topic.
- This served as the **external knowledge base** for the RAG system.

#### 2. Document Chunking
- Tokenized the retrieved document using the **`all-mpnet-base-v2` tokenizer**.
- Split the document into **256-token chunks with 20-token overlap** to preserve contextual continuity.
- This process transformed long articles into **dozens of manageable chunks for semantic search**.

#### 3. Embedding Generation
- Converted each chunk into dense vector representations using the **Sentence Transformer model (`all-mpnet-base-v2`)**.
- These embeddings capture the **semantic meaning of the text**, enabling similarity-based retrieval.

#### 4. Vector Storage and Retrieval
- Stored all embeddings in a **FAISS vector index** using the L2 distance metric.
- When a user asks a question, the system:
  - Converts the query into an embedding
  - Searches the FAISS index
  - Retrieves the **top 3 most relevant document chunks**

#### 5. Answer Generation
- Combined the retrieved chunks into a single context.
- Used the **`deepset/roberta-base-squad2` question-answering model** to extract the most relevant answer from the retrieved context.

---

### 📊 Results

The RAG pipeline successfully transformed unstructured knowledge into an interactive question-answering system:

- Retrieved **complete Wikipedia articles dynamically**
- Split documents into **~256-token chunks with contextual overlap**
- Generated **vector embeddings for each chunk**
- Stored embeddings in a **FAISS vector database for efficient semantic search**
- Retrieved the **top 3 most relevant passages for each query**
- Used a transformer-based QA model to produce **context-aware answers**

This architecture significantly improves response quality by ensuring that answers are **grounded in retrieved knowledge instead of relying solely on the LLM’s internal training data**.

---

### 💡 Key Outcome

This project demonstrates how **Retrieval-Augmented Generation can enhance LLM capabilities** by integrating external knowledge sources with transformer models.  

By combining **semantic search (FAISS), embeddings (Sentence Transformers), and transformer-based QA models**, the system creates a scalable pipeline capable of answering questions using real-time retrieved information.

Such architectures are widely used in **modern AI applications including document assistants, enterprise search systems, research tools, and intelligent chatbots.**
