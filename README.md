# ⚖️ LQ-RAG — Legal Question Answering & Summarization System

An AI-powered **Retrieval-Augmented Generation (RAG)** system that answers questions about the **Indian Constitution** by retrieving relevant legal information from documents and generating context-aware responses using an LLM.

---

## 📄 Project Overview

### Objective

The objective of **LQ-RAG** is to build an intelligent legal question-answering system that allows users to ask questions related to the Indian Constitution in natural language.

The system uses Retrieval-Augmented Generation (RAG) to retrieve relevant information from constitutional documents before generating an answer. This helps the LLM provide responses that are **grounded in the retrieved legal content** instead of relying only on its pretrained knowledge.

---

## ✨ Key Features

- 🤖 Retrieval-Augmented Generation (RAG) for legal question answering
- ⚖️ Indian Constitution-based question answering
- 📚 Document-based legal knowledge retrieval
- ✂️ Intelligent text chunking using LangChain
- 🔢 Semantic text embeddings using Sentence Transformers
- 🔍 Fast similarity search using FAISS
- 🧠 LLM-based context-aware answer generation
- 📝 Legal document summarization
- 🗄️ MongoDB for storing constitutional documents/data
- 🚀 Semantic search instead of traditional keyword-only search

---

## 🛠️ Technologies Used

| Layer | Technology |
|---|---|
| Programming Language | Python |
| RAG Framework | LangChain |
| LLM | Large Language Model |
| Embeddings | Sentence Transformers |
| Embedding Model | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector Database | FAISS |
| Database | MongoDB |
| Text Processing | NLTK |
| Document Processing | LangChain |
| Development | Jupyter Notebook / VS Code |

---

## 🏛️ Architecture

```
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
```

---

## 🔄 Document Processing Pipeline

```
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
```

---

## 💡 How It Works

### 1. 📚 Document Collection
The system uses documents containing information from the Indian Constitution as the knowledge source.

### 2. 🧹 Text Preprocessing
The documents are cleaned and processed using Python and NLTK to prepare the content for retrieval.

### 3. ✂️ Text Chunking
Large documents are divided into smaller chunks using LangChain's `RecursiveCharacterTextSplitter`.

The project uses:

```python
chunk_size = 512
chunk_overlap = 128
```

The overlap helps preserve contextual information between neighboring chunks.

### 4. 🔢 Generate Embeddings
Each document chunk is converted into a numerical vector using:

```
sentence-transformers/all-MiniLM-L6-v2
```

These embeddings represent the semantic meaning of the text.

### 5. 🔍 FAISS Vector Search
The generated embeddings are stored in a FAISS vector index. FAISS performs similarity search to identify the document chunks that are most relevant to the user's question.

### 6. ❓ User Query
The user enters a question in natural language.

**Example:**
```
What is Article 21 of the Indian Constitution?
```

The question is converted into an embedding using the same embedding model.

### 7. 🔎 Retrieve Relevant Information
FAISS compares the query embedding with the stored document embeddings and retrieves the most relevant chunks.

```
User Question
      ↓
Query Embedding
      ↓
FAISS Similarity Search
      ↓
Relevant Constitutional Content
```

### 8. 🧠 Generate Answer
The retrieved content is provided to the LLM along with the original question.

```
Question
   +
Retrieved Context
   ↓
  LLM
   ↓
Final Answer
```

The LLM generates a response based on the retrieved information.

---

## 🔄 Complete RAG Pipeline

```
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
```

---

## 📂 Project Structure

```
LQ-RAG/
├── data/                   # Indian Constitution source documents
├── notebooks/               # Jupyter notebooks for experimentation
├── src/
│   ├── preprocessing.py     # Text cleaning & preprocessing (NLTK)
│   ├── chunking.py          # LangChain text splitting
│   ├── embeddings.py        # Sentence Transformer embedding generation
│   ├── vector_store.py      # FAISS index creation & search
│   ├── retriever.py         # Query embedding & retrieval logic
│   ├── llm.py                # LLM prompt construction & answer generation
│   └── db.py                  # MongoDB connection & data storage
├── app.py                   # Entry point / API or UI
├── requirements.txt
└── README.md
```

> Adjust this structure to match your actual repository layout.

---

## ⚙️ Installation

```bash
# Clone the repository
git clone https://github.com/<your-username>/LQ-RAG.git
cd LQ-RAG

# Create a virtual environment
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Requirements

- Python 3.9+
- MongoDB (local or Atlas connection string)
- API key/access for your chosen LLM provider

---

## 🚀 Usage

1. **Prepare the documents**
   Place Indian Constitution source files in the `data/` directory.

2. **Build the FAISS index**
   ```bash
   python src/vector_store.py
   ```

3. **Ask a question**
   ```bash
   python app.py --query "What is Article 21 of the Indian Constitution?"
   ```

4. **Sample output**
   ```
   Q: What is Article 21 of the Indian Constitution?
   A: Article 21 guarantees the right to life and personal liberty...
      (Answer generated using retrieved constitutional context)
   ```

---

## 🗺️ Roadmap

- [ ] Add support for multiple legal documents beyond the Constitution
- [ ] Web-based chat interface
- [ ] Multi-lingual query support
- [ ] Citation of specific Articles/Sections in generated answers
- [ ] Evaluation metrics for retrieval and answer quality

---

## 🤝 Contributing

Contributions are welcome! Please open an issue or submit a pull request for improvements, bug fixes, or new features.

---

## 📜 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙏 Disclaimer

This system is intended for **educational and informational purposes only** and does not constitute legal advice. For official legal matters, please consult a qualified legal professional.
