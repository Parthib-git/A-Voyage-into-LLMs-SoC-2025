# PDF Q&A Chatbot

An interactive chatbot that allows users to upload a PDF, process its content, and ask questions to get relevant answers based on the document. Built using Gradio, LangChain, HuggingFace Transformers, and ChromaDB.

---

## Features

- Upload and preview PDF documents
- Extract, clean, and chunk text from PDFs
- Embed chunks using HuggingFace sentence-transformers
- Store and search chunks using Chroma vector database
- Ask natural language questions based on the document
- Returns both the answer and the source chunks used for reasoning
- Styled, user-friendly Gradio interface

---

## Tech Stack

- **LangChain**: Prompting and retrieval-augmented generation
- **HuggingFace Transformers**: Pretrained language models
- **sentence-transformers**: Semantic text embeddings
- **ChromaDB**: Local vector storage and similarity search
- **Gradio**: Web-based interactive interface
- **pdfplumber**: PDF parsing and text extraction
- **NLTK**: Natural language sentence-level chunking

---

## Installation

Install all required dependencies using:

```bash
pip install -q pdfplumber langchain langchain-community langchain_huggingface \
  chromadb huggingface_hub sentence-transformers nltk torch \
  gradio transformers accelerate gradio_pdf
```

---

## Project Structure

- `read_and_clean_pdf(PDF)`  
  Extracts and cleans text from each page of the uploaded PDF using `pdfplumber`.

- `chunk_text(text, chunk_size, overlap)`  
  Uses `NLTKTextSplitter` to split the cleaned text into overlapping sentence-based chunks for semantic coherence.

- `embed_and_store_chunks(chunks)`  
  Encodes chunks using HuggingFace embeddings and stores them in a `Chroma` vector store for similarity-based retrieval.

- `retrieve_relevant_chunks(query, vector_db)`  
  Searches for the most relevant text chunks given a query using vector similarity.

- `answer_query_with_llm(query, vector_db, model, tokenizer)`  
  Constructs a prompt from the query and retrieved chunks, sends it to the language model, and returns both the answer and the chunks used.

- **Gradio UI**  
  A two-part interface that includes:
  - PDF upload and processing
  - Query input and dynamic answer display

---

## Usage Instructions

1. **Upload PDF**  
   Use the Gradio UI to upload a PDF document.

2. **Process Document**  
   Click "Process PDF" to extract and prepare the content for querying.

3. **Ask a Question**  
   Input a natural-language question related to the document.

4. **View Response**  
   The app returns:
   - A direct answer to your query
   - The actual chunks used from the PDF to generate the response

---

## Future Enhancements

- Section-aware chunking (headers and subheaders)
- Metadata tagging (e.g., page numbers in retrieved context)
- Improved speed and caching mechanisms
- Option to download answers and source references
- Multi-PDF support and indexing
- Deployment on Hugging Face Spaces or Streamlit Cloud

---

## Notes

- This project is designed for educational and research purposes.
- To use the interactive Gradio interface, run this notebook in a Colab or local Jupyter environment.
- GitHub preview may not support full rendering of interactive widgets or Gradio blocks.

