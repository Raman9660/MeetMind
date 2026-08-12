# 🎬 MeetMind — AI Meeting Intelligence Assistant

MeetMind is an AI-powered meeting intelligence application that converts meeting recordings and YouTube videos into structured, searchable, and actionable insights.

It combines Speech-to-Text, Large Language Models (LLMs), AI summarization, information extraction, vector databases, embeddings, and Retrieval-Augmented Generation (RAG) to help users understand and interact with meeting content.

MeetMind supports both **English and Hinglish meetings** through an interactive **Streamlit web interface**.

---

## ✨ Features

- 🎥 YouTube meeting video processing
- 🎵 Local audio/video file processing
- 🎙️ Automatic speech-to-text transcription
- 🇬🇧 English transcription using OpenAI Whisper
- 🇮🇳 Hinglish transcription using Sarvam AI
- 📝 AI-generated meeting summaries
- 🏷️ Automatic meeting title generation
- ✅ Action item extraction
- 🔑 Key decision extraction
- ❓ Open question extraction
- 🧠 Retrieval-Augmented Generation (RAG)
- 💬 AI chatbot for asking questions about meetings
- 🔎 Semantic search over meeting transcripts
- 🗃️ ChromaDB vector database
- 🤗 HuggingFace embeddings
- 🖥️ Streamlit web interface
- 💻 Command-line pipeline
- 🔐 Secure API-key management using `.env`

---

# 🛠️ Technology Stack

## Programming Language

- Python 3.10+

## Frontend / User Interface

- Streamlit

## Speech-to-Text

- OpenAI Whisper
- Sarvam AI

## Large Language Model

- Mistral AI
- `mistral-small-latest`

## LLM Framework

- LangChain
- LangChain Core
- LangChain Community
- LangChain Mistral
- LangChain Chroma
- LangChain HuggingFace
- LangChain Text Splitters

## Retrieval-Augmented Generation

- LangChain RAG
- ChromaDB
- HuggingFace Embeddings
- Sentence Transformers

## Embedding Model

```text
all-MiniLM-L6-v2
```

## Text Processing

- RecursiveCharacterTextSplitter

## Audio / Video Processing

- yt-dlp
- PyDub
- FFmpeg

## Machine Learning

- PyTorch
- HuggingFace Sentence Transformers

## Environment Management

- python-dotenv

## Other Libraries

- Requests
- NumPy
- tqdm

---

# 📦 Complete Tech Stack

| Category | Technology |
|---|---|
| Language | Python |
| UI | Streamlit |
| English STT | OpenAI Whisper |
| Hinglish STT | Sarvam AI |
| LLM | Mistral AI |
| LLM Model | mistral-small-latest |
| LLM Framework | LangChain |
| RAG | Retrieval-Augmented Generation |
| Vector Database | ChromaDB |
| Embeddings | HuggingFace |
| Embedding Model | all-MiniLM-L6-v2 |
| Text Splitting | RecursiveCharacterTextSplitter |
| YouTube | yt-dlp |
| Audio Processing | PyDub |
| Multimedia | FFmpeg |
| ML Runtime | PyTorch |
| Environment Variables | python-dotenv |
| UI Framework | Streamlit |

---

# 🏗️ System Architecture

```text
                 USER
                  │
                  ▼
        ┌────────────────────┐
        │    Streamlit UI    │
        └─────────┬──────────┘
                  │
                  ▼
           Meeting Input
           /           \
          /             \
         ▼               ▼
  YouTube URL       Local File
       │                 │
       ▼                 ▼
    yt-dlp        Audio / Video
       │                 │
       └────────┬────────┘
                ▼
        Audio Processing
                │
                ▼
          Audio Chunking
                │
        ┌───────┴────────┐
        │                │
        ▼                ▼
     English          Hinglish
        │                │
        ▼                ▼
     Whisper          Sarvam AI
        │                │
        └───────┬────────┘
                ▼
           Transcript
                │
       ┌────────┼────────┐
       │        │        │
       ▼        ▼        ▼
    Summary  Extractor  Title
       │        │        │
       └────────┼────────┘
                ▼
        Meeting Insights
                │
                ▼
          Text Chunking
                │
                ▼
      HuggingFace Embeddings
                │
                ▼
             ChromaDB
                │
                ▼
          RAG Retriever
                │
                ▼
           Mistral LLM
                │
                ▼
           AI Chatbot
```

---

# 📁 Project Structure

```text
MeetMind/
│
├── app.py
├── main.py
├── test.py
├── Requirements.txt
├── README.md
├── .gitignore
│
├── core/
│   ├── transcriber.py
│   ├── summarizer.py
│   ├── extractor.py
│   ├── vector_store.py
│   └── rag_engine.py
│
└── utils/
    └── audio_processor.py
```

### Generated locally during execution

```text
.venv/
.env
vector_db/
__pycache__/
downloades/
*.pyc
```

These files/directories should not be uploaded to GitHub.

---

# 📌 Core Modules

## `app.py`

Main Streamlit application.

Responsible for:

- User interface
- Meeting input
- File upload
- YouTube URL input
- Language selection
- Meeting processing
- Transcript display
- Summary display
- Action items
- Key decisions
- Open questions
- AI meeting chatbot

---

## `main.py`

Command-line version of the MeetMind pipeline.

Pipeline:

```text
Input
 ↓
Audio Processing
 ↓
Transcription
 ↓
Title Generation
 ↓
Summarization
 ↓
Action Items
 ↓
Key Decisions
 ↓
Open Questions
 ↓
Vector Database
 ↓
RAG
```

---

## `core/transcriber.py`

Responsible for speech-to-text.

```text
English  → OpenAI Whisper
Hinglish → Sarvam AI
```

---

## `core/summarizer.py`

Responsible for:

- Transcript chunking
- Meeting summarization
- Meeting title generation

---

## `core/extractor.py`

Responsible for extracting:

- Action items
- Key decisions
- Open questions

---

## `core/vector_store.py`

Responsible for:

- Generating embeddings
- Creating ChromaDB
- Storing transcript chunks
- Loading the vector database
- Creating the retriever

---

## `core/rag_engine.py`

Responsible for:

- Loading the vector store
- Retrieving relevant transcript chunks
- Building the RAG pipeline
- Sending context to Mistral
- Generating answers

---

## `utils/audio_processor.py`

Responsible for:

- YouTube audio downloading
- Local media processing
- Audio conversion
- Audio chunking

---

# 🧠 RAG Architecture

MeetMind uses Retrieval-Augmented Generation to answer questions based on the actual meeting transcript.

Instead of sending the entire transcript to the LLM for every question, the system retrieves only the most relevant transcript sections.

```text
User Question
      │
      ▼
Question Embedding
      │
      ▼
ChromaDB Vector Search
      │
      ▼
Relevant Transcript Chunks
      │
      ▼
Prompt + Retrieved Context
      │
      ▼
Mistral LLM
      │
      ▼
Grounded Answer
```

---

# 🔎 RAG Pipeline

## Step 1 — Transcript Chunking

Long transcripts are divided into smaller chunks using:

```text
RecursiveCharacterTextSplitter
```

```text
Full Transcript
      ↓
Text Chunks
```

---

## Step 2 — Generate Embeddings

Each transcript chunk is converted into a vector using:

```text
all-MiniLM-L6-v2
```

```text
Text Chunk
    ↓
HuggingFace Embedding Model
    ↓
Vector
```

---

## Step 3 — Store in ChromaDB

The generated embeddings are stored in:

```text
vector_db/
```

---

## Step 4 — Retrieve Relevant Context

When the user asks a question, ChromaDB searches for the most relevant transcript chunks.

---

## Step 5 — Generate Answer

The retrieved context is passed to Mistral.

```text
Question
   +
Retrieved Context
   ↓
Mistral
   ↓
Answer
```

---

# 🎙️ Speech-to-Text Pipeline

## English

```text
Audio
  ↓
Audio Chunks
  ↓
OpenAI Whisper
  ↓
English Transcript
```

## Hinglish

```text
Hinglish Audio
      ↓
Audio Chunks
      ↓
Sarvam AI
      ↓
English Transcript
```

---

# 📝 Meeting Summarization

Long transcripts are processed in chunks.

```text
Full Transcript
      ↓
Split into Chunks
      ↓
Individual Summaries
      ↓
Combine Summaries
      ↓
Final Meeting Summary
```

---

# 📋 Meeting Insights

MeetMind automatically generates:

### 🏷️ Meeting Title

A short AI-generated title describing the meeting.

### 📝 Summary

A concise summary containing the important discussion points.

### ✅ Action Items

Identifies tasks, responsible people, and deadlines when available.

### 🔑 Key Decisions

Identifies important decisions made during the meeting.

### ❓ Open Questions

Identifies unresolved questions and follow-up topics.

---

# 🚀 Installation & Setup

Follow these steps to run MeetMind from a fresh computer.

---

# 1. Prerequisites

Install the following:

| Requirement | Purpose |
|---|---|
| Python 3.10+ | Run the application |
| Git | Clone the repository |
| FFmpeg | Audio/video processing |
| Mistral API Key | LLM and RAG |
| Sarvam AI API Key | Hinglish transcription |

Check Python:

```bash
python --version
```

Check Git:

```bash
git --version
```

Check FFmpeg:

```bash
ffmpeg -version
```

---

# 2. Clone the Repository

Open a terminal and run:

```bash
git clone https://github.com/Raman9660/MeetMind.git
```

Go inside the project:

```bash
cd MeetMind
```

---

# 3. Create Virtual Environment

A virtual environment keeps the project's dependencies isolated from the rest of the system.

## Windows

```powershell
python -m venv .venv
```

Activate it:

```powershell
.venv\Scripts\Activate.ps1
```

After activation, the terminal should show:

```text
(.venv) PS C:\...\MeetMind>
```

### If PowerShell blocks activation

Run:

```powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned
```

Then:

```powershell
.venv\Scripts\Activate.ps1
```

---

## macOS / Linux

Create:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

---

# 4. Install Python Dependencies

Make sure `.venv` is activated.

Run:

```bash
pip install -r Requirements.txt
```

If any required LangChain packages are missing:

```bash
pip install langchain-chroma langchain-text-splitters
```

Verify installed packages:

```bash
pip list
```

---

# 5. Install FFmpeg

FFmpeg is required for processing audio and video.

Check:

```bash
ffmpeg -version
```

If you see:

```text
'ffmpeg' is not recognized...
```

install FFmpeg and add it to your system PATH.

After installation, restart VS Code and run:

```bash
ffmpeg -version
```

again.

---

# 6. Create the `.env` File

Create a file named:

```text
.env
```

in the root of the project.

Your structure should look like:

```text
MeetMind/
│
├── .env
├── app.py
├── main.py
├── test.py
├── Requirements.txt
├── README.md
├── .gitignore
│
├── core/
└── utils/
```

---

# 7. Configure `.env`

Open `.env` and add:

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key

WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5
```

Replace:

```text
your_mistral_api_key
```

with your actual Mistral API key.

Replace:

```text
your_sarvam_api_key
```

with your actual Sarvam AI API key.

---

# 8. API Keys

## Mistral AI

Mistral AI is used for:

- Meeting summarization
- Meeting title generation
- Action item extraction
- Key decision extraction
- Open question extraction
- RAG question answering

Add:

```env
MISTRAL_API_KEY=your_mistral_api_key
```

---

## Sarvam AI

Sarvam AI is used for:

- Hinglish speech recognition
- English translation

Add:

```env
SARVAM_API_KEY=your_sarvam_api_key
```

---

## OpenAI Whisper

Whisper runs locally.

No Whisper API key is required.

Configure:

```env
WHISPER_MODEL=small
```

---

# 9. Environment File Structure

After creating `.env`, the project should look like:

```text
MeetMind/
│
├── .env
├── app.py
├── main.py
├── test.py
├── Requirements.txt
├── README.md
├── .gitignore
│
├── core/
│   ├── transcriber.py
│   ├── summarizer.py
│   ├── extractor.py
│   ├── vector_store.py
│   └── rag_engine.py
│
└── utils/
    └── audio_processor.py
```

---

# 🔒 10. Protect API Keys

**Never upload `.env` to GitHub.**

Your `.gitignore` should contain:

```gitignore
# Environment
.env
.env.*

# Virtual environment
.venv/

# Python cache
__pycache__/
*.pyc

# Generated vector database
vector_db/

# Downloaded media
downloades/

# Logs
*.log
```

Before pushing to GitHub, run:

```bash
git status
```

Make sure `.env` is not included in the files being committed.

---

# ▶️ 11. Run the Streamlit Application

Make sure the virtual environment is active:

```text
(.venv)
```

Run:

```bash
streamlit run app.py
```

If `streamlit` is not recognized, use:

```bash
python -m streamlit run app.py
```

You should see:

```text
Local URL: http://localhost:8501
```

Open:

```text
http://localhost:8501
```

in your browser.

---

# 🎬 12. How to Use MeetMind

## Step 1 — Provide Meeting Source

You can provide:

### YouTube URL

Example:

```text
https://www.youtube.com/watch?v=XXXXXXXX
```

### Local Audio/Video

Example:

```text
C:\Users\YourName\Videos\meeting.mp4
```

---

## Step 2 — Select Language

Choose:

```text
English
```

or:

```text
Hinglish
```

### English

Uses:

```text
OpenAI Whisper
```

### Hinglish

Uses:

```text
Sarvam AI
```

---

## Step 3 — Start Analysis

Start the meeting analysis.

MeetMind processes:

```text
Input
  ↓
Audio Extraction
  ↓
Audio Chunking
  ↓
Speech-to-Text
  ↓
Full Transcript
  ↓
Meeting Title
  ↓
Summary
  ↓
Action Items
  ↓
Key Decisions
  ↓
Open Questions
  ↓
Text Chunking
  ↓
Embeddings
  ↓
ChromaDB
  ↓
RAG Retriever
  ↓
Mistral
  ↓
AI Meeting Chat
```

---

# 📊 13. Generated Results

After processing, MeetMind provides:

### 📝 Meeting Summary

A concise summary of the meeting.

### 🏷️ Meeting Title

AI-generated title.

### ✅ Action Items

Tasks and responsibilities identified from the meeting.

### 🔑 Key Decisions

Important decisions made during the meeting.

### ❓ Open Questions

Unresolved questions and follow-up topics.

### 📄 Transcript

Complete meeting transcript.

### 💬 AI Meeting Chat

Ask questions about the processed meeting.

Example questions:

```text
What were the main decisions?
```

```text
Who was assigned the project task?
```

```text
What deadlines were discussed?
```

```text
What problems were identified?
```

```text
What topics require follow-up?
```

---

# 💻 14. Run Using Command Line

MeetMind also provides a CLI pipeline.

Run:

```bash
python main.py
```

The application will ask:

```text
Enter YouTube URL or local file path:
```

Then:

```text
Language (english/hinglish):
```

The CLI pipeline processes the meeting and generates:

- Meeting title
- Summary
- Action items
- Key decisions
- Open questions
- RAG-based answers

---

# 🧪 15. Run Tests

The project contains:

```text
test.py
```

Run:

```bash
python test.py
```

---

# 🗃️ 16. Vector Database

When MeetMind processes a meeting, it automatically creates:

```text
vector_db/
```

You do **not** need to manually create this folder.

Pipeline:

```text
Transcript
     ↓
Text Chunking
     ↓
HuggingFace Embeddings
     ↓
ChromaDB
     ↓
Vector Search
     ↓
RAG
```

---

# 🧹 17. Reset Vector Database

If ChromaDB causes an error or you want to rebuild the database:

Delete:

```text
vector_db/
```

Then run:

```bash
streamlit run app.py
```

The vector database will be created again automatically.

---

# 🔄 18. Complete Fresh Setup

For a new computer, follow these steps:

### Clone

```bash
git clone https://github.com/Raman9660/MeetMind.git
cd MeetMind
```

### Create virtual environment

```bash
python -m venv .venv
```

### Windows activation

```powershell
.venv\Scripts\Activate.ps1
```

### Install dependencies

```bash
pip install -r Requirements.txt
```

### Install additional packages if required

```bash
pip install langchain-chroma langchain-text-splitters
```

### Create `.env`

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5
```

### Check FFmpeg

```bash
ffmpeg -version
```

### Run application

```bash
streamlit run app.py
```

### Open browser

```text
http://localhost:8501
```

---

# ⚠️ Troubleshooting

## `ModuleNotFoundError`

Activate the virtual environment:

```powershell
.venv\Scripts\Activate.ps1
```

Then install dependencies:

```bash
pip install -r Requirements.txt
```

---

## `streamlit is not recognized`

Run:

```bash
python -m streamlit run app.py
```

---

## `ffmpeg is not recognized`

Install FFmpeg and add it to the system PATH.

Restart VS Code.

Then verify:

```bash
ffmpeg -version
```

---

## API Key Error

Check that:

```text
MeetMind/.env
```

exists.

It should contain:

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
```

Restart Streamlit after changing `.env`.

---

## Whisper Processing Is Slow

Whisper runs locally.

Processing speed depends on:

- CPU
- GPU
- RAM
- Audio duration
- Whisper model size

---

## ChromaDB Error

Delete:

```text
vector_db/
```

Then restart:

```bash
streamlit run app.py
```

---

# 📌 Important Files

| File / Folder | Purpose |
|---|---|
| `app.py` | Streamlit web application |
| `main.py` | Command-line application |
| `test.py` | Testing |
| `Requirements.txt` | Python dependencies |
| `.env` | API keys and configuration |
| `.gitignore` | Git ignored files |
| `core/transcriber.py` | Speech-to-text |
| `core/summarizer.py` | Summarization and title generation |
| `core/extractor.py` | Action items, decisions and questions |
| `core/vector_store.py` | Embeddings and ChromaDB |
| `core/rag_engine.py` | RAG question answering |
| `utils/audio_processor.py` | Audio/video processing |
| `vector_db/` | Generated vector database |
| `.venv/` | Local Python virtual environment |

---

# 🚫 Files NOT to Upload to GitHub

Do not upload:

```text
.env
.venv/
__pycache__/
*.pyc
vector_db/
downloades/
*.log
```

These are either sensitive, generated, or unnecessary files.

---

# 📤 GitHub Upload / Update Commands

After making changes to the project:

Check status:

```bash
git status
```

Add files:

```bash
git add .
```

Commit:

```bash
git commit -m "Update MeetMind project"
```

Push:

```bash
git push
```

---

# ⚡ Quick Start

If Python, Git and FFmpeg are already installed:

```bash
git clone https://github.com/Raman9660/MeetMind.git
cd MeetMind
python -m venv .venv
```

### Windows

```powershell
.venv\Scripts\Activate.ps1
```

### Install dependencies

```bash
pip install -r Requirements.txt
```

### Create `.env`

```env
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5
```

### Run

```bash
streamlit run app.py
```

### Open

```text
http://localhost:8501
```

---

# 🎯 Use Cases

MeetMind can be used for:

- Corporate meetings
- Team meetings
- Client calls
- Interviews
- Online lectures
- Project discussions
- Research meetings
- Student discussions
- Conference recordings
- Meeting documentation

---

# 🚀 Future Improvements

- 👥 Speaker diarization
- 🗣️ Speaker identification
- 📅 Calendar integration
- 📧 Automatic follow-up email generation
- 📄 PDF meeting reports
- 📊 Meeting analytics
- 💾 Persistent meeting history
- 🔎 Search across multiple meetings
- 👤 User authentication
- ☁️ Cloud deployment
- ⚡ GPU-accelerated transcription
- 🌐 Additional Indian language support
- 📱 Mobile-friendly interface

---

# 💡 Technical Highlights

This project demonstrates practical implementation of:

- Python
- Artificial Intelligence
- Large Language Models
- Speech Recognition
- OpenAI Whisper
- Sarvam AI
- Mistral AI
- LangChain
- Retrieval-Augmented Generation
- Vector Databases
- ChromaDB
- HuggingFace Embeddings
- Sentence Transformers
- Audio Processing
- YouTube Processing
- Prompt Engineering
- Long-document Summarization
- Semantic Search
- Streamlit
- API Integration
- Environment-based Secret Management

---

# 👨‍💻 Author

**Harsh Vardhan Raj**

GitHub:

https://github.com/Raman9660/MeetMind

---

# ⭐ MeetMind

### Transcribe → Summarise → Extract Insights → Search → Chat
