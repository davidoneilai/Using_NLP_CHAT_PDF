# README.md

```markdown
# Langchain Document Loader

This project demonstrates how to load a PDF document, split the text into chunks, generate embeddings for each chunk, and store the embeddings in a vector store for retrieval using the Langchain library.

## Installation

Before running the code, you need to install the required libraries. You can do this by running the following commands in your terminal:

```bash
pip install langchain
pip install faiss-cpu
pip install huggingface_hub
pip install sentence-transformers
pip install chromadb
pip install langchainhub
```

## Usage

### Set Hugging Face API Token

First, you need to set your Hugging Face API token. This token is used to access the Hugging Face model hub. Replace

 `

YOUR_HUGGINGFACE_API_TOKEN` with your actual Hugging Face API token.

```python
import os
os.environ["HUGGINGFACEHUB_API_TOKEN"] = "YOUR_HUGGINGFACE_API_TOKEN"
```

### Load a PDF Document

Next, you can load a PDF document. Replace `YOUR_PDF_FILE` with the path to your PDF file.

```python
from langchain.document_loaders import PyPDFLoader
loader = PyPDFLoader("YOUR_PDF_FILE")
pages = loader.load()
```

### Split Text into Chunks

Then, you can split the text into chunks using the `CharacterTextSplitter`. The `chunk_size` parameter determines the size of each chunk, and the `chunk_overlap` parameter determines the overlap between chunks.

```python
from langchain.text_splitter import CharacterTextSplitter
text_splitter = CharacterTextSplitter(chunk_size=500, chunk_overlap=0)
docs = text_splitter.split_documents(pages)
```

### Generate Embeddings

After splitting the text, you can generate embeddings for each chunk using the `HuggingFaceEmbeddings` class. The `model_name` parameter should be the name of a BERT model. In this example, we're using the `neuralmind/bert-base-portuguese-cased` model.

```python
from langchain.embeddings import HuggingFaceEmbeddings
embedding = HuggingFaceEmbeddings(model_name="neuralmind/bert-base-portuguese-cased")
```

### Store Embeddings for Retrieval

Finally, you can store the embeddings in a vector store for retrieval. The `Chroma` class is used to create the vector store, and the `as_retriever` method is used to create a retriever. The `search_type` parameter determines the type of search to perform, and the `search_kwargs` parameter is used to pass additional arguments to the search method.

```python
from langchain_community.vectorstores import Chroma
vectorstore = Chroma.from_documents(documents=docs, embedding=embedding)
retriever = vectorstore.as_retriever(search_type="similarity", search_kwargs={"k": 6})
```

Now, you can use the `retriever` to retrieve similar chunks of text based on their embeddings.
```
