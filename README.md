# RAG System Documentation

## Project Setup Instructions

### 1. Create a Virtual Environment

Create a virtual environment using Python 3.12:

```
python3.12 -m venv venv
```

### 2. Activate the Virtual Environment

Activate the virtual environment:

**On Windows:**
```
venv\Scripts\activate
```

**On macOS/Linux:**
```
source venv/bin/activate
```

### 3. Install Required Packages

Install all required dependencies:

```
pip install -r requirements.txt
```

Your `requirements.txt` should include:
```
langchain
langchain_anthropic
pinecone-client
anthropic
voyageai
langchain-voyageai
python-dotenv
pypdf
langchain-community
datasets
langchain_openai
```

### 4. Set Up the .env File

Ensure your `.env` file contains the following API keys:
* **PINECONE_API_KEY** (for vector database)
* **ANTHROPIC_API_KEY** (for Claude models)
* **VOYAGE_API_KEY** (for Voyage embeddings)

Example `.env` file:
```
PINECONE_API_KEY=your_pinecone_api_key_here
ANTHROPIC_API_KEY=your_anthropic_api_key_here
VOYAGE_API_KEY=your_voyage_api_key_here
```

### 5. Run the RAG System

After setting up the virtual environment and installing the dependencies, execute the main script:

```
python rag_system.py
```

## Project Overview

This project implements a Retrieval-Augmented Generation (RAG) system that can:
1. Load documents (PDF, DOCX)
2. Split them into manageable chunks
3. Generate embeddings for each chunk
4. Store those embeddings in Pinecone vector database
5. Retrieve relevant information based on queries
6. Generate responses using various LLM options (Claude, Gemini, or Hugging Face models)

## Implementation Details

### Document Processing

The system loads documents from a specified folder:
- Supports PDF and DOCX formats
- Splits documents into chunks using RecursiveCharacterTextSplitter
- Creates embeddings using SentenceTransformer

### Vector Database Setup

The system uses Pinecone as a vector database:
- Creates a serverless index if one doesn't exist
- Stores document embeddings with their content
- Default dimension size is 384 (based on the all-MiniLM-L6-v2 model)

### Retrieval and Generation Options

The system provides multiple LLM options:
1. **Gemini API Integration**:
   - Custom implementation for Gemini 2.0 Flash model
   - Handles API requests and responses

2. **Hugging Face Models**:
   - Uses models like google/flan-t5-large
   - Implements using HuggingFacePipeline

### Query Processing

The final RAG pipeline:
- Takes a user query
- Retrieves relevant document chunks from Pinecone
- Passes the context to the selected LLM
- Returns a contextually-informed answer

## Usage Example

```python
query = "What is the main topic of the documents?"
response = rag_system.invoke({"query": query})
print("Answer:", response["result"])
```
