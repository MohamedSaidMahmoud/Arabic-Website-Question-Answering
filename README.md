# Arabic Retrieval-Augmented Generation (RAG) System

## 🧠 Overview

This project implements an **Arabic-language Retrieval-Augmented Generation (RAG)** system that answers Arabic user queries using real-world information extracted from Arabic news sources. It leverages modern NLP components including multilingual embeddings, vector search, and large language models (LLMs).

The goal is to provide **accurate, context-aware answers** by retrieving the most relevant passages from a vector database populated with scraped Arabic content, and using an LLM to generate responses.

---

## 🎯 Objectives

- ✅ Scrape Arabic news articles from the web
- ✅ Generate semantic embeddings from Arabic text
- ✅ Store and retrieve embeddings using a vector database
- ✅ Build a question-answering pipeline using LangChain + LLM
- ✅ Deploy a simple Gradio interface for Arabic Q&A

---

## 🏗️ System Architecture

The system consists of the following components:

1. **Data Extraction**: Arabic news scraping using [Firecrawl](https://firecrawl.dev)
2. **Text Cleaning**: Content cleaning with `BeautifulSoup`
3. **Embedding Generation**: Using `paraphrase-multilingual-MiniLM-L12-v2` from Sentence Transformers
4. **Vector Storage**: Embeddings indexed in a `ChromaDB` vector database
5. **Question Embedding**: Arabic questions converted to vector representations
6. **Document Retrieval**: Similarity search for relevant article segments
7. **Answer Generation**: Answering using Google Gemini 1.5 Flash via LangChain
8. **Web UI**: Gradio interface for Arabic question input and answer display

---

## 🛠️ Implementation Details

### 🔍 Data Scraping & Preprocessing

- Scraping performed using `Firecrawl` from Arabic news sites (e.g., Al Jazeera Sports)
- HTML content cleaned with `BeautifulSoup4`
- Cleaned text saved for embedding

### 🔢 Embedding Generation

- Model used: `paraphrase-multilingual-MiniLM-L12-v2`
- Supports multiple languages including Arabic
- Converts article chunks into dense vector embeddings

### 🧠 Vector Database

- Implemented with [`Chroma`](https://www.trychroma.com/)
- Embeddings inserted in batches for memory efficiency using `batch_upsert`
- Fast similarity search with cosine distance

### 🔁 RAG Pipeline (LangChain)

Steps:
1. Retrieve top 3 most relevant text chunks
2. Construct prompt with context and question
3. Send prompt to **Gemini 1.5 Flash**
4. Parse LLM output and return final answer

### 🌐 User Interface

- Built using [`Gradio`](https://gradio.app/)
- Arabic question input box
- Displays generated answers directly from RAG pipeline

---

## 💡 Example

### ✅ Input (Arabic):


---

## ⚙️ Technologies Used

| Component         | Tool/Library                                      |
|------------------|---------------------------------------------------|
| Web Scraping     | Firecrawl, BeautifulSoup                          |
| Embeddings        | `SentenceTransformers/paraphrase-multilingual-MiniLM-L12-v2` |
| Vector DB        | ChromaDB                                          |
| LLM              | Google Gemini 1.5 Flash (via LangChain)           |
| Interface        | Gradio                                            |
| Framework        | LangChain                                         |
| Language Support | Arabic                                            |

---

## 🧪 Performance Evaluation

- The system was tested with multiple real-world Arabic queries
- Accurately retrieved relevant context and generated appropriate answers in Arabic
- Demonstrated ability to handle morphological and orthographic variations

---

## ⚠️ Challenges & Solutions

| Challenge                        | Solution                                                                 |
|----------------------------------|--------------------------------------------------------------------------|
| Arabic Morphology & Dialects     | Used multilingual sentence embeddings with good Arabic support           |
| Context Limitations (LLMs)       | Retrieved top-3 most relevant chunks, trimmed inputs to fit context window |
| Efficient Search in Large Data   | Batch vector indexing + cosine similarity with ChromaDB                  |

---

## 📂 Folder Structure

├── data/ # Raw scraped Arabic articles

├── embeddings/ # Saved document embeddings

├── chroma_db/ # Vector database index files

├── app/ # Gradio interface and pipeline

├── rag_chain.py # LangChain-based RAG implementation

├── requirements.txt # All Python dependencies

└── README.md # Project documentation
