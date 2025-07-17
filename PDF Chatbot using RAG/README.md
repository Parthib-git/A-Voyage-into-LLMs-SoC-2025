# PDF CHATBOT USING RAG

An interactive chatbot that allows users to upload a PDF, process its content, and ask questions to get relevant answers based on the document. Built using Gradio, LangChain, HuggingFace Transformers, and ChromaDB. Primarily build and tested in Google Colab using T4 Tesla GPU.

---

## Project Stucture

- Upload and preview PDF documents using **gradio_pdf**.
- Extract, clean, and chunk text from PDFs using **pdfplumber**,**regex** and **NLTKTextSplitter** (For better semantic retention).
- Embed chunks using **HuggingFace sentence-transformers//multi-qa-MiniLM-L6-cos-v1**.
- Store and search chunks using **ChromaDB**.
- Ask natural language questions based on the document
- Makes 2 more questions by paraphrasing the user-given question using paraphrasing model **humarin/chatgpt_paraphraser_on_T5_base**.
- Searches the database for best matching chunks by ranking them using **similarity_search_with_score** from ChromaDB Database.
- Makes a prompt using a boilerplate code for prompt making with concise instructions to the LLM.
- Uses the model **meta-llama/Llama-2-7b-chat** from **HuggingFace**.
- Returns both the answer and the source chunks used for reasoning for transparency
- Styled **Gradio** interface for better user-friendliness.

---


## Installation

Install all required dependencies using:

```
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

