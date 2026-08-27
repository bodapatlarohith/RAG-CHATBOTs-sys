⚖️ LQ-RAG — Legal Question Answering & Summarization System

An AI-powered Retrieval-Augmented Generation (RAG) system that answers questions about the Indian Constitution by retrieving relevant legal information from documents and generating context-aware responses using an LLM.

📄 Project Overview
Objective

The objective of LQ-RAG is to build an intelligent legal question-answering system that allows users to ask questions related to the Indian Constitution in natural language.

The system uses Retrieval-Augmented Generation (RAG) to retrieve relevant information from constitutional documents before generating an answer. This helps the LLM provide responses that are grounded in the retrieved legal content instead of relying only on its pretrained knowledge.

✨ Key Features
🤖 Retrieval-Augmented Generation (RAG) for legal question answering
⚖️ Indian Constitution-based question answering
📚 Document-based legal knowledge retrieval
✂️ Intelligent text chunking using LangChain
🔢 Semantic text embeddings using Sentence Transformers
🔍 Fast similarity search using FAISS
🧠 LLM-based context-aware answer generation
📝 Legal document summarization
🗄️ MongoDB for storing constitutional documents/data
🚀 Semantic search instead of traditional keyword-only search
🛠️ Technologies Used
Layer	Technology
Programming Language	Python
RAG Framework	LangChain
LLM	Large Language Model
Embeddings	Sentence Transformers
Embedding Model	sentence-transformers/all-MiniLM-L6-v2
Vector Database	FAISS
Database	MongoDB
Text Processing	NLTK
Document Processing	LangChain
Development	Jupyter Notebook / VS Code
🏛️ Architecture
                 User Question
                       │
                       ▼
              ┌─────────────────┐
              │ Query Processing│
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Query Embedding │
              │ Sentence        │
              │ Transformer     │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │  FAISS Vector   │
              │     Search      │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │ Relevant Text   │
              │     Chunks      │
              └────────┬────────┘
                       │
                       ▼
              ┌─────────────────┐
              │      LLM        │
              │ Question +      │
              │ Retrieved Context│
              └────────┬────────┘
                       │
                       ▼
                 Final Answer
🔄 Document Processing Pipeline
Indian Constitution Documents
            │
            ▼
      Text Extraction
            │
            ▼
      Text Preprocessing
            │
            ▼
         Chunking
            │
            ▼
        Embeddings
            │
            ▼
      FAISS Vector Index
💡 How It Works
1. 📚 Document Collection

The system uses documents containing information from the Indian Constitution as the knowledge source.

2. 🧹 Text Preprocessing

The documents are cleaned and processed using Python and NLTK to prepare the content for retrieval.

3. ✂️ Text Chunking

Large documents are divided into smaller chunks using LangChain's RecursiveCharacterTextSplitter.

The project uses:

chunk_size = 512
chunk_overlap = 128

The overlap helps preserve contextual information between neighboring chunks.

4. 🔢 Generate Embeddings

Each document chunk is converted into a numerical vector using:

sentence-transformers/all-MiniLM-L6-v2

These embeddings represent the semantic meaning of the text.

5. 🔍 FAISS Vector Search

The generated embeddings are stored in a FAISS vector index.

FAISS performs similarity search to identify the document chunks that are most relevant to the user's question.

6. ❓ User Query

The user enters a question in natural language.

Example:

What is Article 21 of the Indian Constitution?

The question is converted into an embedding using the same embedding model.

7. 🔎 Retrieve Relevant Information

FAISS compares the query embedding with the stored document embeddings and retrieves the most relevant chunks.

User Question
      ↓
Query Embedding
      ↓
FAISS Similarity Search
      ↓
Relevant Constitutional Content
8. 🧠 Generate Answer

The retrieved content is provided to the LLM along with the original question.

Question
   +
Retrieved Context
   ↓
  LLM
   ↓
Final Answer

The LLM generates a response based on the retrieved information.

🔄 Complete RAG Pipeline
              OFFLINE / INDEXING

Indian Constitution Documents
            │
            ▼
      Text Preprocessing
            │
            ▼
          Chunking
    512 Size / 128 Overlap
            │
            ▼
        Embeddings
   all-MiniLM-L6-v2
            │
            ▼
      FAISS Vector Store
            │
            │
            ▼
              ONLINE / QUERY

        User Question
            │
            ▼
      Query Embedding
            │
            ▼
    FAISS Similarity Search
            │
            ▼
     Relevant Text Chunks
            │
            ▼
    Context + User Question
            │
            ▼
            LLM
            │
            ▼
       Final Answer
