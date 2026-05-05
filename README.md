
# 🔐 DataVault – Secure File Storage and Management

> A secure, AI-powered cloud file storage and management platform built with Python & Streamlit — featuring dual-layer AES-256 encryption, intelligent document analysis, RAG-based chatbot, and controlled file sharing.

📹 **Demo Video:** [Watch on YouTube](https://youtu.be/ZTv9pz90Kd0)

---

## 📌 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Team](#team)

---

## Overview

DataVault is a Streamlit-powered secure cloud file storage and management platform that prioritizes **data privacy**, **user control**, and **intelligent document handling** — unlike conventional third-party platforms such as Google Drive or Dropbox.

It employs **dual-layer AES-256 encryption** combined with format-native password protection, ensuring no plaintext file or credential is ever persisted. Shared file access enforces a **three-factor verification scheme** (password + decryption key + time-limited email OTP), and every sharing operation produces a **per-recipient independently re-encrypted file copy**, ensuring full credential isolation.

An AI module powered by **Google Gemini** automatically categorizes documents and extracts future-dated calendar events, while a **RAG-based chatbot** enables natural language querying of document content with web search fallback.

---

## Features

### 🔒 Security
- **Dual-layer encryption** — AES-256 encryption on top of format-native password protection (PDF, DOCX, XLSX)
- **Zero plaintext storage** — no file or credential is ever stored unencrypted
- **Three-factor file sharing** — password + decryption key + time-limited email OTP
- **Per-recipient re-encryption** — each shared copy uses unique credentials for full isolation
- **bcrypt authentication** — secure password hashing for user accounts
- **JWT-based session management** — secure and stateless session control

### 🤖 AI & Intelligence
- **Automatic document classification** — Google Gemini categorizes uploaded files (Finance, Medical, Legal, Job, Education, etc.)
- **Calendar event extraction** — AI extracts future-dated events from documents automatically
- **RAG-based chatbot** — ask natural language questions about your uploaded documents using LangChain + ChromaDB + HuggingFace embeddings
- **Web search fallback** — Tavily API provides live web context when document alone is insufficient

### 📊 Analytics & Trust
- **Dynamic trust score system** — tracks file integrity across sharing chains with real-time owner notifications
- **Analytics dashboard** — visualizes file activity, sharing statistics, and network graphs
- **Automated email notifications** — alerts owners when trust scores are updated

### 👤 User Experience
- Intuitive Streamlit web interface
- Secure file upload and download
- Active share management with expiry controls
- File detail view with sharing history

---

## Tech Stack

| Layer | Technology |
|---|---|
| **Frontend / UI** | Streamlit |
| **Backend** | Python |
| **Database** | MongoDB Atlas |
| **File Storage** | Google Drive (via Colab mount) |
| **Encryption** | AES-256 (pyAesCrypt), PDF/DOCX/XLSX native (PyPDF2, msoffcrypto) |
| **AI / LLM** | Google Gemini API |
| **RAG Pipeline** | LangChain, ChromaDB, HuggingFace (all-MiniLM-L6-v2) |
| **Document Parsing** | Docling |
| **Web Search** | Tavily API |
| **Authentication** | bcrypt, JWT |
| **Email** | SendMail (SMTP) |
| **Tunneling** | Ngrok (pyngrok) |
| **Visualization** | Plotly, NetworkX |

---

## System Architecture

```
User Upload
    │
    ▼
Content Extraction (Docling)
    │
    ▼
AI Analysis (Google Gemini)
 ├── Document Classification
 └── Event Extraction
    │
    ▼
Dual-Layer Encryption
 ├── Layer 1: Format-native password protection
 └── Layer 2: AES-256 encryption
    │
    ▼
Secure Storage (MongoDB + Google Drive)
    │
    ▼
RAG Indexing (ChromaDB + HuggingFace Embeddings)
    │
    ▼
User Access / Sharing
 ├── 3-Factor Verification (password + key + OTP)
 └── Per-recipient re-encrypted copy
```

---

## Installation

### Prerequisites
- Python 3.10+
- MongoDB Atlas account
- Google Gemini API key
- Tavily API key
- Ngrok account

### 1. Clone the Repository

```bash
git clone https://github.com/JahnavikaGopalbvrith/DataVault.git
cd DataVault
```

### 2. Install Dependencies

```bash
pip install streamlit pyngrok pymongo bcrypt send-mail mammoth weasyprint \
            langchain-core==0.3.76 langchain-chroma==0.2.6 \
            langchain-google-genai==2.1.10 langgraph==0.6.6 \
            langchain_experimental langchain-huggingface==0.3.1 \
            docling PyPDF2 pyAesCrypt msoffcrypto-tool \
            tavily-python networkx plotly cryptography
```

### 3. Set Up Environment Variables

Create a `.env` file in the root directory (see [Environment Variables](#environment-variables) section).

### 4. Run the App

```bash
streamlit run app.py
```

> **Note:** If running on Google Colab, the notebook uses Ngrok to tunnel the Streamlit app. Run all cells in order and access the app via the generated Ngrok URL.

---

## Environment Variables

Create a `.env` file with the following:

```env
MONGODB_URI=your_mongodb_connection_string
GOOGLE_API_KEY=your_google_gemini_api_key
TAVILY_API_KEY=your_tavily_api_key
Ngrok_API_KEY=your_ngrok_authtoken
EMAIL_ADDRESS=your_sender_email@gmail.com
EMAIL_PASSWORD=your_email_app_password
SECRET_KEY=your_fernet_secret_key
```

> To generate a Fernet `SECRET_KEY`:
> ```python
> from cryptography.fernet import Fernet
> print(Fernet.generate_key().decode())
> ```

---

## Usage

1. **Sign Up / Login** — Create an account with secure bcrypt-hashed credentials.
2. **Upload Files** — Upload PDF, DOCX, or XLSX files. The system automatically encrypts and classifies them.
3. **View AI Analysis** — See automatic document category and any extracted calendar events.
4. **Chat with Your Document** — Use the RAG chatbot to ask questions about any uploaded file.
5. **Share Securely** — Share files with recipients using 3-factor verification and expiry controls.
6. **Monitor Trust Scores** — Track file integrity across sharing chains from your dashboard.
7. **Analytics** — Visualize sharing networks and file activity stats.

---

## Project Structure

```
DataVault/
├── app.py              # Main Streamlit application
├── helper.py           # Core utilities: encryption, DB, AI, RAG
├── send_mail.py        # Email notification module
├── .env                # Environment variables (not committed)
├── logs_dir/           # Daily activity logs
└── README.md
```


---

## 📄 License

This project was developed as an academic major project. All rights reserved by the authors.
