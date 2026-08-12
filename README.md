# 🎬 MeetMind — AI Meeting Intelligence Assistant

MeetMind is an AI-powered meeting intelligence application that converts meeting recordings and YouTube videos into structured, searchable, and actionable insights.

It combines Speech-to-Text, Large Language Models (LLMs), summarization, information extraction, vector databases, and Retrieval-Augmented Generation (RAG) to help users understand and interact with meeting content.

The application supports both **English and Hinglish meetings** through an interactive **Streamlit web interface**.

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

---

# 🏗️ System Architecture

```text
              YouTube URL / Local File
                       │
                       ▼
              ┌──────────────────┐
              │ Audio Processing │
              │ yt-dlp / PyDub   │
              └────────┬─────────┘
                       │
                       ▼
                Audio Chunking
                       │
                       ▼
           ┌───────────┴───────────┐
           │                       │
           ▼                       ▼
      ┌──────────┐            ┌───────────┐
      │ Whisper  │            │ Sarvam AI │
      │ English  │            │ Hinglish  │
      └────┬─────┘            └─────┬─────┘
           │                        │
           └──────────┬─────────────┘
                      ▼
                Full Transcript
                      │
          ┌───────────┼───────────┐
          │           │           │
          ▼           ▼           ▼
     Summarizer   Extractor   Title Generator
          │           │           │
          └───────────┼───────────┘
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
