# 🧭 PolicyNav

### **AI-Powered Public Policy Navigation, Search & Intelligence Platform**

> *Navigating complex policies — made simple, accessible, and multilingual.*

---

## 🔗 Quick Links

| **Category** | **Details** |
|---|---|
| 📽️ Demo | Google Colab + ngrok (live tunnel) |
| 🧩 Source Code | This Repository |
| ☁️ Platform | Google Colab + Google Drive |
| 🧠 AI Models | Qwen2.5-1.5B-Instruct · NLLB-200 · spaCy · sentence-transformers · FAISS |
| 🔐 Auth | JWT · bcrypt · OTP Email · Security Questions |

---

## 📌 Table of Contents

1. [About the Project](#-about-the-project)
2. [Problem Statement & Motivation](#-problem-statement--motivation)
3. [Key Features](#-key-features)
4. [Architecture Overview](#-architecture-overview)
5. [Tech Stack](#️-tech-stack)
6. [AI Models Used](#-ai-models-used)
7. [Project Structure](#-project-structure)
8. [Installation & Setup](#️-installation--setup)
9. [Usage Guide](#-usage-guide)
10. [Admin Dashboard](#️-admin-dashboard)
11. [Multilingual Support](#-multilingual-support)
12. [Screenshots](#-screenshots)
13. [Roadmap](#️-roadmap)
14. [Team](#-team)
15. [License](#-license)

---

## 📖 About the Project

**PolicyNav** is a full-stack, AI-powered platform that makes public policy documents accessible to everyone — regardless of language, background, or expertise.

Built as part of the **Infosys Springboard Internship — PolicyNav Specialization Module**, this platform combines RAG-based question answering, multilingual translation, document summarization, entity extraction via knowledge graphs, and readability analytics into a single, production-grade Streamlit application.

📌 **Target Users:** Citizens, policy analysts, governance professionals, legal researchers, journalists, and students.

---

## 🎯 Problem Statement & Motivation

Public policy documents are long, jargon-heavy, and often available only in English. Millions of citizens across India and the world are unable to understand the policies that directly affect their lives.

**PolicyNav solves this by:**

- 🔍 Enabling natural-language search directly over policy PDFs using FAISS vector search
- 🌐 Translating questions and answers across 7+ Indian languages via NLLB-200
- 📝 Summarizing large documents into 3 concise bullet points instantly
- 🕸️ Mapping entities and relationships via an interactive knowledge graph
- 📊 Scoring readability with 5 industry-standard metrics and visual gauges
- 🔐 Securing access with JWT auth, OTP email verification, and account lockout

---

## 🚀 Key Features

### 👤 User Features

| **Feature** | **Description** |
|---|---|
| 🔐 JWT Authentication | Secure login, registration, OTP-based password recovery, account lockout after 3 failed attempts |
| 🔍 RAG Search Engine | FAISS vector search over ingested policy PDFs with bi-directional multilingual support |
| 📝 Document Summarizer | Upload PDF or paste text; generates 3-point summary with follow-up Q&A mode |
| 🕸️ Knowledge Graph | Interactive pyvis entity graph with NER — ORG, LAW, GPE, PERSON nodes |
| 📊 Readability Analyzer | Flesch, Flesch-Kincaid, SMOG, Gunning Fog, Coleman-Liau + Plotly gauges |
| 🌐 Multilingual Output | NLLB-200 translates AI responses into 7 Indian languages |
| 👤 User Profile Dashboard | Avatar upload, email change (OTP-verified), password history, personalised settings |
| ⭐ Feedback System | Per-section 5-star ratings + comments logged to SQLite |
| 🕘 Activity History | Full timeline of all user interactions with section, input, and AI output |
| ⚙️ Personalised Settings | Language preference, notifications, timestamps, results-per-page — all saved to DB |

### 🛠️ Admin-Only Features

- **User Management** — unlock, lock, promote to admin, demote, delete accounts
- **Real-Time Activity Tracking** — full system-wide audit log with timeline UI
- **Data Visualization** — feature popularity pie chart, language distribution bar chart, model utilization graphs
- **Feedback Analysis** — star rating cards + WordCloud of user comments
- **Data Export** — one-click CSV download of users, activity logs, and feedback
- **Root Admin Protection** — root admin account cannot be locked, demoted, or deleted

---

## 🧩 Architecture Overview

> **Deployment Model:** Monolithic Streamlit Application hosted on Google Colab, tunnelled via ngrok

**Data Flow:**
```
User → Streamlit UI → JWT Auth → NLP Engine → FAISS Vector Store → Qwen2.5 LLM → NLLB Translator → Response
```

| **Component** | **Role** |
|---|---|
| `config.py` | JWT settings, email credentials, admin config, security constants |
| `db.py` | SQLite schema, CRUD for users, activity_log, feedback, user_settings |
| `auth.py` | bcrypt hashing, JWT encode/decode, OTP generation, email dispatch |
| `vector_store.py` | PDF/HTML/TXT ingestion, FAISS indexing, semantic search with deduplication |
| `nlp_engine.py` | Qwen2.5 LLM inference, NLLB-200 translation, RAG pipeline, summarization |
| `knowledge_graph.py` | spaCy NER, NetworkX graph construction, pyvis interactive HTML export |
| `readability.py` | textstat wrapper — 5 readability metrics + derived stats |
| `profile_page.py` | User dashboard — avatar, email change (OTP), password, settings tabs |
| `app.py` | Streamlit router, all page tabs, sidebar, admin dashboard, session state |

---

## 🛠️ Tech Stack

| **Layer** | **Technology** |
|---|---|
| Frontend | Streamlit + streamlit-option-menu |
| Backend / Logic | Python 3.10+ |
| AI / NLP | Hugging Face Transformers, sentence-transformers, spaCy |
| Vector Search | FAISS (faiss-cpu) |
| Database | SQLite (via Python sqlite3) |
| Security | JWT (PyJWT), bcrypt, OTP over Gmail SMTP |
| Visualization | Plotly, pyvis, matplotlib, WordCloud |
| Deployment | Google Colab + Google Drive + ngrok |
| PDF Parsing | PyPDF2, BeautifulSoup4 |
| Readability | textstat |

---

## 🤖 AI Models Used

| **Model** | **Purpose** | **Framework** |
|---|---|---|
| Qwen2.5-1.5B-Instruct | Primary LLM for RAG Q&A, summarization, document Q&A | 🤗 Transformers |
| NLLB-200 Distilled 600M | Multilingual translation — 7 Indian languages + English | 🤗 Transformers |
| paraphrase-multilingual-MiniLM-L12-v2 | Sentence embeddings for FAISS semantic search | sentence-transformers |
| en_core_web_sm | Named Entity Recognition — ORG, LAW, GPE, PERSON | spaCy |
| textstat metrics | Readability scoring — 5 industry-standard formulas | textstat |

> 💡 **Note:** Qwen2.5 runs in `float16` mode (no quantization required for 1.5B). NLLB-200 uses 2-beam search for speed. All models are loaded once and cached globally via Streamlit's `@st.cache_resource`.

---

## 📂 Project Structure

```
PolicyNav/
├── milestone_4.ipynb         # Main Colab notebook (all cells)
│
├── app.py                    # Streamlit app router & all page tabs
├── config.py                 # JWT, email, admin constants
├── db.py                     # SQLite schema & all DB operations
├── auth.py                   # Auth helpers: hash, JWT, OTP, email
├── readability.py            # Readability metrics wrapper
├── vector_store.py           # FAISS ingestion & semantic search
├── nlp_engine.py             # Qwen LLM + NLLB translator pipeline
├── knowledge_graph.py        # spaCy NER + NetworkX + pyvis graph
├── profile_page.py           # User Profile Dashboard (Milestone 4)
│
└── [Google Drive: /PolicyNav/]
    ├── documents/            # Upload policy PDFs here
    ├── graphs/               # Generated knowledge graph HTML
    ├── faiss_index.bin       # FAISS vector index
    ├── faiss_meta.pkl        # Document chunk metadata
    └── policynav_users.db    # SQLite database
```

---

## ⚙️ Installation & Setup

### Prerequisites

- Google account with Google Colab and Google Drive access
- ngrok account — free tier is sufficient (grab your `NGROK_AUTHTOKEN`)
- Gmail account with **App Password** enabled (for OTP emails)

### Step 1 — Add Colab Secrets

In Google Colab, open the **Secrets panel** (🔑 icon on the left sidebar) and add:

| **Secret Key** | **Value** |
|---|---|
| `JWT_SECRET_KEY` | Any strong random string |
| `EMAIL_ID` | Your Gmail address |
| `EMAIL_APP_PASSWORD` | Gmail App Password (not your login password) |
| `ADMIN_EMAIL_ID` | Email address for the root admin account |
| `ADMIN_PASSWORD` | Password for the root admin account |
| `NGROK_AUTHTOKEN` | From your ngrok dashboard |

### Step 2 — Run Cells in Order

| **Cell** | **Action** |
|---|---|
| Cell 1 | Install all dependencies (pip + spaCy model download) |
| Cell 2 | Mount Google Drive and create APP_DIR folders |
| Cell 3–5 | Write `config.py`, `db.py`, `auth.py` |
| Cell 6–9 | Write `readability.py`, `vector_store.py`, `knowledge_graph.py`, `nlp_engine.py` |
| Cell 10 | Write `profile_page.py` (Milestone 4 User Dashboard) |
| Cell 11 | Write `app.py` (main Streamlit application) |
| Cell 12 | Load secrets into environment variables |
| Cell 13 | *(Optional)* Ingest policy PDFs into FAISS |
| Cell 14 | 🚀 Launch app via ngrok — copy the public URL |

### Step 3 — Upload Policy Documents

Place your policy PDFs, HTML files, or TXT files into:

```
/PolicyNav/documents/   (on your Google Drive)
```

Then run **Cell 13** to ingest them into the FAISS vector store. New files are detected automatically — already-ingested files are skipped.

---

## 📝 Usage Guide

1️⃣ **Register / Login** — Create an account with email, username, and a strong password (min. 8 chars, uppercase + number required)

2️⃣ **Select a Feature** from the sidebar — RAG Search, Summarization, Knowledge Graph, Readability Analyzer, or History

3️⃣ **RAG Search** — Type your policy question in any supported language. Choose output language and optionally enable **Simplify Jargon** mode. The AI searches the vector DB and translates the answer back.

4️⃣ **Summarizer** — Upload a policy PDF or paste text, select output language, and get a 3-bullet summary. Use the Q&A box to ask follow-up questions from the same document.

5️⃣ **Knowledge Graph** — Click **Render Interactive Topology** to generate a live force-directed entity graph from all ingested documents. Hover nodes for details.

6️⃣ **Readability Analyzer** — Enter text or upload a PDF/TXT. View 5 readability gauges, grade level classification (Beginner / Intermediate / Advanced / Expert), and detailed text statistics.

7️⃣ **Profile** — Manage your avatar, change email (OTP-verified), update password (with history check), and configure app settings.

8️⃣ **Feedback** — Submit a 5-star rating and optional comment after using any feature.

---

## 🛡️ Admin Dashboard

Login with admin credentials to access:

- 👥 **User Control** — view all users, lock/unlock accounts, promote/demote admins, delete users
- 📜 **Activity Tracking** — real-time system-wide audit log
- 📈 **Data Visualization** — feature popularity, language usage, and model utilization charts
- 💬 **Feedback Analysis** — ratings, comments, and WordCloud visualization
- 📥 **Data Export** — download Users, Activity Logs, and Feedback as CSV files

---

## 🌐 Multilingual Support

PolicyNav uses Facebook's **NLLB-200** (No Language Left Behind) model for high-quality, bi-directional translation. Your question is first translated to English for FAISS search, then the AI answer is translated back to your chosen language.

| **Language** | **NLLB-200 Code** |
|---|---|
| English | `eng_Latn` |
| Hindi | `hin_Deva` |
| Tamil | `tam_Taml` |
| Telugu | `tel_Telu` |
| Kannada | `kan_Knda` |
| Marathi | `mar_Deva` |
| Bengali | `ben_Beng` |

---

## 📸 Screenshots

> *(To be updated with real UI images)*

- Login & Registration Page
- User Dashboard with Activity Stats
- RAG Search Chat Interface (multilingual)
- Document Summarizer with Q&A Mode
- Interactive Knowledge Graph Explorer
- Readability Analyzer with Plotly Gauges
- User Profile — Avatar, Email, Password, Settings Tabs
- Admin Dashboard — User Control & Analytics

---

## 🗺️ Roadmap

### ✅ Completed (Milestone 4)

- [x] Full Streamlit application with JWT auth and admin dashboard
- [x] FAISS-based RAG pipeline with Qwen2.5-1.5B-Instruct
- [x] NLLB-200 multilingual translation (7 languages)
- [x] Interactive Knowledge Graph with pyvis
- [x] User Profile Dashboard — avatar, email change, settings
- [x] Activity history, feedback system, CSV data export

### 🔜 Planned

- [ ] Fine-tuned policy-domain LLM on Indian governance datasets
- [ ] Speech-to-text input for accessibility
- [ ] WhatsApp / Telegram bot interface for rural citizen access
- [ ] Docker containerization for local deployment
- [ ] Expanded language support (Gujarati, Punjabi, Odia, Urdu)
- [ ] Policy comparison mode — side-by-side diff across documents

---

## 👥 Team

| **Name** | **Role** | **Responsibilities** |
|---|---|---|
| Add Name | ML / NLP Engineer | Qwen LLM integration, NLLB translation, RAG pipeline, FAISS |
| Add Name | Backend Developer | JWT auth, SQLite DB, admin dashboard, activity logging |
| Add Name | Frontend Developer | Streamlit UI, Plotly charts, knowledge graph, readability tab |
| Add Name | Full Stack / Profile | Profile dashboard, settings, avatar, email OTP, Milestone 4 |
| Add Name | Documentation | README, project report, presentation, deployment guide |

---

## 📜 License

🆓 **MIT License** — Free to use, modify, and distribute with attribution. See the [LICENSE](LICENSE) file for full terms.

---

<div align="center">

Built with ❤️ as part of the **Infosys Springboard — PolicyNav Specialization**

*Applying AI to governance, public affairs, and policy intelligence.*

</div>
