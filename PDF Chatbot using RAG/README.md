# PDF CHATBOT USING RAG

An chatbot that allows users to upload a PDF, process its content, and ask questions to get relevant answers based on the document by using Retrieval Augmented Generation. Primarily build and tested in Google Colab using T4 Tesla GPU.

---
## Features

- Upload and preview PDF documents
- Extract, clean, and chunk text from PDFs
- Embed chunks using HuggingFace sentence-transformers
- Store and search chunks using Chroma vector database
- Ask natural language questions based on the document
- Returns both the answer and the source chunks used for reasoning
- Styled, user-friendly Gradio interface


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

## Description of functions

- `read_and_clean_pdf(PDF)`  
  Extracts and cleans text from each page of the uploaded PDF using `pdfplumber`.

- `chunk_text(text, chunk_size, overlap)`  
  Uses `NLTKTextSplitter` to split the cleaned text into overlapping sentence-based chunks for semantic coherence.

- `embed_and_store_chunks(chunks)`  
  Encodes chunks using HuggingFace embeddings and stores them in a `ChromaDB` vector store for similarity-based retrieval.

- `generate_paraphrases(text, num_return_sequences=2)`
  Generated 2 paraphrases for the question for better context retrieval.

- `prompt(query, relevant_chunks)`
  Generates a prompt for the LLM using a boilerplate.

- `retrieve_relevant_chunks(query, vector_db)`  
  Searches for the most relevant text chunks given a query using similarity_search_with_score.

- `process_pdf_to_vector_database(pdf_file)`
  Streamlines the preprocessing by taking the pdf as input and giving the vector database as output.
  
- `answer_query_with_llm(query, vector_db, llm_model, llm_tokenizer)`  
  Streamlines the prompt building, relevant chunk retrieval and LLM answer generation into one function.



## Usage Instructions

1. **Download** the PDF_Chatbot_Using_RAG.ipynb file and open in Google Colab with Tesla T4 GPU connected.

1. **Install all the dependencies** from the first cell starting with  `!pip install -q...` and then run the other cells and put your own HF token in the given field for the used LLM that can be acquired from <a href = 'https://huggingface.co/meta-llama/Llama-2-7b-chat-hf'> here </a>, the model loading will take time.

1. **Upload PDF**  
   Use the Gradio UI to upload a PDF document.

2. **Process Document**  
   Click "Process PDF" to extract and prepare the content for querying.

3. **Ask a Question**  
   Input a question related to the document and press the "Ask" button.

4. **View Response**  
   The app returns:
   - A direct answer to your query
   - The actual chunks used from the PDF to generate the response

---

## Results
The following images show the question given to the LLM and it's response on the left, and the corresponding part in the PDF it should be coming from on the right side.
<table>
  <tr>
    <td style="width: 60%"><strong>Question and Response (Zoom in to read)</strong></td>
    <td style="width: 40%;"><strong>From PDF</strong></td>
  </tr>
  <tr>
    <td style="width: 60%;"><img src="QnA Results/Question 1.png" width="100%"> Pretty accurate, only added the attendance part from a part of the following section, sectionwise chunking should solve this.</td>
    <td style="width: 40%;"><img src="QnA Results/Context 1.png" width="100%"></td>
  </tr>
  <tr>
    <td style="width: 60%;"><img src="QnA Results/Question 2.png" width="100%"></td>
    <td style="width: 40%;"><img src="QnA Results/Context 2.png" width="100%"><img src="QnA Results/Context 2-2.png" width="100%"></td>
  </tr>
  <tr>
    <td style="width: 60%;"><img src="QnA Results/Question 3.png" width="100%"></td>
    <td style="width: 40%;"><img src="QnA Results/Context 3.png" width="100%"></td>
  </tr>
  <tr>
    <td style="width: 60%;"><img src="QnA Results/Question 4.png" width="100%"></td>
    <td style="width: 40%;"><img src="QnA Results/Context 4.png" width="100%"></td>
  </tr>
</table>


## UI  built on Gradio

<p>
  <img src = "Full UI Image.png">
</p>


## Future Enhancements

- Section-aware chunking (headers and subheaders)
- Metadata tagging (e.g., page numbers in retrieved context)
- Improved speed 
- Multi-PDF support
- Deployment on Hugging Face Spaces/Streamlit Cloud/Vercel/Netlify or elsewhere

---

## Notes


- GitHub preview does not support rendering of Gradio blocks.
