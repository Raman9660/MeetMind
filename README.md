🎬 MeetMind — AI Meeting Intelligence Assistant

MeetMind is an AI-powered meeting intelligence application that converts meeting recordings and YouTube videos into structured, searchable, and actionable insights.

It combines speech-to-text, Large Language Models (LLMs), text summarization, information extraction, vector databases, and Retrieval-Augmented Generation (RAG) to help users understand and interact with meeting content.

The application supports both English and Hinglish meetings and provides an interactive Streamlit web interface.

✨ Key Features

🎥 Process YouTube meeting videos

🎵 Process local audio/video files

🎙️ Automatic speech-to-text transcription

🇬🇧 English transcription using OpenAI Whisper

🇮🇳 Hinglish transcription and English translation using Sarvam AI

📝 AI-generated meeting summaries

🏷️ Automatic meeting title generation

✅ Action item extraction

🔑 Key decision extraction

❓ Open question and follow-up extraction

🧠 Retrieval-Augmented Generation (RAG)

💬 Ask questions about the meeting using an AI chatbot

🔎 Semantic search over meeting transcripts

🗃️ Local Chroma vector database

🤗 HuggingFace embeddings

🖥️ Interactive Streamlit dashboard

💻 Command-line pipeline support

🏗️ How MeetMind Works

                YouTube URL / Local File
                         │
                         ▼
                ┌───────────────────┐
                │  Audio Processing │
                │   yt-dlp / pydub  │
                └─────────┬─────────┘
                          │
                          ▼
                   Audio Chunking
                          │
                          ▼
             ┌────────────┴────────────┐
             │                         │
             ▼                         ▼
       ┌─────────────┐          ┌──────────────┐
       │   Whisper   │          │   Sarvam AI  │
       │   English   │          │   Hinglish   │
       └──────┬──────┘          └───────┬──────┘
              │                         │
              └───────────┬─────────────┘
                          ▼
                    Full Transcript
                          │
             ┌────────────┼────────────┐
             │            │            │
             ▼            ▼            ▼
        Summarizer    Extractor    Title Generator
             │            │            │
             └────────────┼────────────┘
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
                   Meeting Chatbot

🛠️ Complete Tech Stack

Programming Language

Python

Python is used as the primary programming language for the complete application.

Recommended version:

Python 3.10+

Frontend / User Interface

Streamlit

MeetMind uses Streamlit to build the interactive web application.

The interface provides:

YouTube URL / local file input

Language selection

Meeting analysis controls

Pipeline status

Transcript viewer

Summary display

Action items

Key decisions

Open questions

AI meeting chatbot

Run the UI using:

streamlit run app.py

Speech-to-Text

OpenAI Whisper

Whisper is used for local English speech transcription.

Meeting Audio
     ↓
Audio Chunks
     ↓
Whisper
     ↓
English Transcript

The default model is:

small

Configuration:

WHISPER_MODEL=small

Hinglish Transcription

Sarvam AI

Sarvam AI is used for Hinglish speech processing and English translation.

Hinglish Audio
      ↓
Audio Pieces
      ↓
Sarvam AI
      ↓
English Transcript

Configuration:

SARVAM_API_KEY=your_api_key
SARVAM_STT_MODEL=saaras:v2.5

Audio / Video Processing

yt-dlp

Used to download audio from YouTube URLs.

YouTube URL
     ↓
yt-dlp
     ↓
Downloaded Audio

PyDub

Used for:

Audio conversion

Audio manipulation

Audio chunking

Preparing audio for transcription

FFmpeg

Required for audio/video conversion.

Check installation:

ffmpeg -version

FFmpeg must be installed separately and available in the system PATH.

🤖 Large Language Model

Mistral AI

Mistral is the primary LLM used by MeetMind.

It is responsible for:

Meeting summarization

Meeting title generation

Action item extraction

Key decision extraction

Open question extraction

RAG-based question answering

Configuration:

MISTRAL_API_KEY=your_mistral_api_key

🔗 LangChain

LangChain is used to build the LLM and RAG pipelines.

The project uses LangChain components for:

Prompt templates

LLM chains

Output parsing

Runnable pipelines

Retrieval

RAG orchestration

🧠 Retrieval-Augmented Generation (RAG)

MeetMind uses RAG to make the meeting chatbot grounded in the transcript.

Instead of sending the entire transcript to the LLM for every question:

Transcript
    ↓
Split into chunks
    ↓
Generate embeddings
    ↓
Store vectors
    ↓
Search relevant chunks
    ↓
Send relevant context to Mistral
    ↓
Generate answer

This allows the chatbot to answer questions using relevant parts of the actual meeting transcript.

🗃️ Vector Database

ChromaDB

ChromaDB is used as the local vector database.

Transcript
    ↓
Text Chunks
    ↓
Embeddings
    ↓
ChromaDB

The generated vector database is stored locally in:

vector_db/

This directory should normally be excluded from GitHub.

🤗 Embeddings

HuggingFace Sentence Transformers

MeetMind uses HuggingFace embeddings to convert transcript chunks into numerical vectors.

Model:

all-MiniLM-L6-v2

Pipeline:

Transcript Chunk
       ↓
all-MiniLM-L6-v2
       ↓
Vector Embedding
       ↓
ChromaDB

Relevant packages include:

sentence-transformers

langchain-huggingface

huggingface-hub

✂️ Text Splitting

MeetMind uses LangChain's RecursiveCharacterTextSplitter to divide long transcripts into smaller chunks.

This helps with:

LLM context limits

Better semantic retrieval

More precise RAG results

Large Transcript
       ↓
RecursiveCharacterTextSplitter
       ↓
Multiple Smaller Chunks

📝 Meeting Summarization

For long transcripts, MeetMind uses a chunk-based summarization approach.

Full Transcript
      ↓
Transcript Chunks
      ↓
Individual Summaries
      ↓
Combined Information
      ↓
Final Summary

This allows longer meetings to be processed more effectively.

📋 Meeting Information Extraction

The extractor module uses Mistral to identify important meeting information.

Action Items

Extracts:

Task

Responsible person

Deadline when available

Key Decisions

Identifies important decisions made during the meeting.

Open Questions

Identifies unresolved questions and topics requiring follow-up.

🔐 Environment & Configuration

MeetMind uses python-dotenv for environment variables.

Create a .env file in the project root:

MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key

WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5

Never commit .env to GitHub.

Recommended .gitignore:

.env
.env.*
.venv/
__pycache__/
*.pyc
vector_db/
downloades/
*.log

📁 Project Structure

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

📌 Core Modules

app.py

Main Streamlit application.

Responsible for:

User interface

Meeting input

Language selection

Pipeline execution

Pipeline status

Result display

Meeting chatbot

main.py

Command-line version of the MeetMind pipeline.

core/transcriber.py

Responsible for speech-to-text.

English  → Whisper
Hinglish → Sarvam AI

core/summarizer.py

Responsible for:

Transcript splitting

Summary generation

Title generation

core/extractor.py

Responsible for extracting:

Action items

Key decisions

Open questions

core/vector_store.py

Responsible for:

Creating embeddings

Creating ChromaDB

Storing transcript chunks

Loading the vector database

Creating the retriever

core/rag_engine.py

Responsible for:

Loading the vector store

Retrieving relevant transcript chunks

Creating the RAG chain

Asking questions using Mistral

utils/audio_processor.py

Responsible for:

YouTube audio downloading

Local audio/video processing

WAV conversion

Audio chunking

🚀 How to Run MeetMind

Step 1 — Install Python

Install Python 3.10 or newer.

Check:

python --version

Step 2 — Install FFmpeg

Check:

ffmpeg -version

If the command is not recognized, install FFmpeg and add it to your system PATH.

Step 3 — Clone the Repository

git clone https://github.com/Raman9660/MeetMind.git
cd MeetMind

Step 4 — Create a Virtual Environment

Windows

python -m venv .venv

Activate:

.venv\Scripts\Activate.ps1

If PowerShell blocks activation:

Set-ExecutionPolicy -Scope Process -ExecutionPolicy RemoteSigned

Then:

.venv\Scripts\Activate.ps1

macOS / Linux

python3 -m venv .venv
source .venv/bin/activate

Step 5 — Install Dependencies

Run:

pip install -r Requirements.txt

The requirements include the project's AI, RAG, audio-processing, and UI dependencies.

If required by the source imports, ensure these packages are also present:

pip install langchain-chroma langchain-text-splitters

Step 6 — Configure API Keys

Create:

.env

in the project root.

Add:

MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key

WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5

Replace the placeholders with your actual API keys.

Step 7 — Run the Web Application

Start Streamlit:

streamlit run app.py

Open:

http://localhost:8501

in your browser.

🎬 How to Use the Application

1. Provide Meeting Source

You can provide:

YouTube URL

Local audio/video file

Example:

https://www.youtube.com/watch?v=XXXXXXXX

2. Select Language

Choose:

English

or:

Hinglish

English uses Whisper.

Hinglish uses Sarvam AI.

3. Analyse the Meeting

MeetMind runs:

Audio / Video
     ↓
Audio Extraction
     ↓
Audio Chunking
     ↓
Speech Recognition
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
Vector Database
     ↓
RAG Chatbot

📊 Generated Results

The application provides:

🏷️ Meeting Title

AI-generated title.

📝 Summary

AI-generated meeting summary.

✅ Action Items

Tasks and responsibilities identified from the meeting.

🔑 Key Decisions

Important decisions made during the meeting.

❓ Open Questions

Unresolved questions and follow-up topics.

📄 Full Transcript

Complete meeting transcript.

💬 Chat With the Meeting

Example questions:

What were the main decisions?

Who was assigned the marketing task?

What deadlines were discussed?

What problems were identified?

What topics require follow-up?

The RAG pipeline retrieves relevant transcript sections and sends them to Mistral to generate the answer.

💻 Running the CLI Version

Run:

python main.py

The program asks for:

Enter YouTube URL or local file path:

Then:

Language (english/hinglish):

It processes the meeting and generates:

Meeting title

Summary

Action items

Key decisions

Open questions

RAG-based answers

🧪 Testing

The project includes:

test.py

Run:

python test.py

This can be used to test the main meeting-processing workflow.

⚠️ Troubleshooting

FFmpeg Error

Check:

ffmpeg -version

Install FFmpeg and add it to PATH if necessary.

API Key Error

Check .env:

MISTRAL_API_KEY=your_key
SARVAM_API_KEY=your_key

Restart the application after changing environment variables.

Whisper Is Slow

Whisper runs locally. Performance depends on:

CPU

GPU

RAM

Audio duration

Whisper model size

ChromaDB Issues

Delete:

vector_db/

and process the meeting again to rebuild the vector store.

📦 Main Technologies

Category

Technology

Language

Python

UI

Streamlit

Speech-to-Text

OpenAI Whisper

Hinglish STT

Sarvam AI

LLM

Mistral AI

LLM Framework

LangChain

RAG

LangChain RAG

Vector Database

ChromaDB

Embeddings

HuggingFace

Embedding Model

all-MiniLM-L6-v2

Text Splitting

RecursiveCharacterTextSplitter

YouTube Processing

yt-dlp

Audio Processing

PyDub

Multimedia Backend

FFmpeg

Environment Management

python-dotenv

ML Runtime

PyTorch

🎯 Use Cases

MeetMind can be used for:

Corporate meetings

Team meetings

Client calls

Interviews

Online lectures

Project discussions

Research meetings

Student discussions

Conference recordings

Meeting documentation

🚀 Future Improvements

👥 Speaker diarization

🗣️ Speaker identification

📅 Calendar integration

📧 Automatic follow-up email generation

📄 PDF meeting reports

📊 Meeting analytics

💾 Meeting history

🔎 Search across multiple meetings

👤 User authentication

☁️ Cloud deployment

⚡ GPU-accelerated transcription

🌐 Additional Indian language support

📱 Mobile-friendly UI

💡 Technical Highlights

MeetMind demonstrates practical implementation of:

Large Language Models

Retrieval-Augmented Generation

Vector Databases

Speech-to-Text

Audio Processing

Long-Document Summarization

Prompt Engineering

LangChain

Mistral AI

OpenAI Whisper

Sarvam AI

ChromaDB

HuggingFace Embeddings

Streamlit

API Integration

Environment-based Secret Management

👨‍💻 Author

Harsh Vardhan Raj

GitHub: Raman9660

⚡ Quick Start

git clone https://github.com/Raman9660/MeetMind.git
cd MeetMind

python -m venv .venv

Windows

.venv\Scripts\Activate.ps1

Install Dependencies

pip install -r Requirements.txt

Configure .env

MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
WHISPER_MODEL=small
SARVAM_STT_MODEL=saaras:v2.5

Run

streamlit run app.py

Open:

http://localhost:8501

⭐ MeetMind

Transcribe → Summarise → Extract Insights → Search → Chat
