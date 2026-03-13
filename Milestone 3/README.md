# PolicyNav – AI Powered Policy Navigation System (Milestone 3)
Project Title

PolicyNav: AI-Powered Policy Understanding and Navigation System

Description

PolicyNav is an AI-powered platform designed to help users easily search, understand, and analyze government policies and documents.

The system processes policy documents (PDFs), builds a semantic vector database, and allows users to ask natural language questions. The platform retrieves relevant policy information and generates intelligent responses using a Large Language Model (LLM).

In Milestone 3, the system integrates advanced features including:

- User Authentication with OTP verification

- AI-powered Question Answering

- Semantic Search using FAISS

- Knowledge Graph Visualization

- Policy Readability Analysis

- Secure Dashboard Interface

- The application is built using Streamlit, Python, and Machine Learning/NLP technologies.


## Features Implemented in Milestone 3

### 1. User Authentication System

The platform includes a secure authentication system:

- User Signup

- Login with password verification

- Forgot Password functionality

- OTP verification through Email

- Secure JWT-based authentication

- Password hashing using bcrypt

### 2. AI-Based Policy Question Answering

Users can ask questions about policy documents such as:

"What are the schemes for farmers?"

The system:

- Converts documents into embeddings

- Stores them in a FAISS vector database

- Retrieves the most relevant sections

- Generates answers using an LLM model

### 3. Semantic Document Search (RAG)

The system implements Retrieval-Augmented Generation (RAG):

- Documents are converted into embeddings using Sentence Transformers

- Stored in a FAISS vector index

When a question is asked:

- Relevant document chunks are retrieved

- The LLM generates a contextual response

- This enables accurate responses directly from policy documents.

### 4. Knowledge Graph Visualization

PolicyNav extracts entities and relationships from policy documents and visualizes them as a Knowledge Graph.

This helps users:

- Understand connections between policies

- Identify related schemes

- Explore structured policy information

### 5. Policy Readability Analysis

The system includes a Readability Analyzer that evaluates how easy or difficult a policy document is to read.

Metrics used include:

- Flesch Reading Ease

- Sentence length

- Word complexity

- Readability scores

- This helps policymakers improve document clarity.

### 6. Document Processing

The system automatically processes:

PDF policy documents

HTML web content

Using:

PyPDF2

BeautifulSoup

The extracted text is cleaned and stored for AI-based search.

### Technologies Used

Programming Language

Python

Frontend

Streamlit

Machine Learning / AI

Transformers

Sentence Transformers

FAISS Vector Database

NLP Tools

HuggingFace Transformers

TextStat

BeautifulSoup

Backend

SQLite Database

JWT Authentication

Bcrypt Password Hashing

Visualization

Plotly

Knowledge Graph

Deployment Tools

Google Colab

Ngrok


### Steps to Run the Application

Step 1: Install Required Libraries

Step 2: Mount Google Drive (If using Colab)

Step 3: Upload Policy Documents

Step 4: Build the Vector Index

Step 5: Launch the Streamlit Application

Step 6: Create Public Link using Ngrok



