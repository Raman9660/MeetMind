# MeetMind — AI Meeting Intelligence Assistant

MeetMind is an AI-powered meeting intelligence application that transforms meeting recordings and YouTube videos into structured, actionable insights.

It can extract audio, transcribe conversations, generate meeting titles and summaries, identify action items, key decisions, and unresolved questions, and provide an interactive RAG-based chat interface for asking questions about the meeting.

The application supports both English and Hinglish meetings and provides a Streamlit-based web interface.

---

## ✨ Features

- 🎬 YouTube & Local File Support
  - Process meetings from YouTube URLs.
  - Process local audio/video files.

- 🎙️ Automatic Speech Transcription
  - English transcription using OpenAI Whisper.
  - Hinglish transcription and English translation using Sarvam AI.

- 📝 AI Meeting Summarization
  - Generates a concise professional summary from the complete transcript.
  - Handles long transcripts using chunking and map-reduce style summarization.

- 🏷️ Automatic Meeting Title Generation
  - Generates a short professional title based on the meeting content.

- ✅ Action Item Extraction
  - Identifies tasks discussed during the meeting.
  - Extracts the responsible person and deadline when available.

- 🔑 Key Decision Extraction
  - Identifies important decisions made during the meeting.

- ❓ Open Question Detection
  - Extracts unresolved questions and topics requiring follow-up.

- 🧠 RAG-Based Meeting Chat
  - Converts the transcript into vector embeddings.
  - Stores embeddings in a local Chroma vector database.
  - Retrieves relevant transcript sections for each question.
  - Generates answers using Mistral.
  - Answers are grounded in the meeting transcript.

- 💻 Interactive Streamlit UI
  - Meeting analysis dashboard.
  - Transcript viewer.
  - Summary and insights.
  - Interactive meeting chatbot.

---

# 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │   YouTube URL /      │
                    │   Local Audio/Video  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Audio Processing   │
                    │      yt-dlp / pydub  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Audio Chunking    │
                    └──────────┬───────────┘
                               │
                               ▼
              ┌────────────────┴────────────────┐
              │                                 │
              ▼                                 ▼
      ┌───────────────┐                 ┌────────────────┐
      │    Whisper    │                 │   Sarvam AI    │
      │    English    │                 │    Hinglish    │
      └───────┬───────┘                 └───────┬────────┘
              │                                 │
              └────────────────┬────────────────┘
                               ▼
                    ┌──────────────────────┐
                    │      Transcript      │
                    └──────────┬───────────┘
                               │
              ┌────────────────┼─────────────────┐
              │                │                 │
              ▼                ▼                 ▼
       ┌────────────┐   ┌─────────────┐   ┌─────────────┐
       │ Summarizer │   │  Extractor  │   │ Title Gen.  │
       └────────────┘   └─────────────┘   └─────────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Chroma Vector DB   │
                    │ HuggingFace Embeddings│
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      RAG Engine      │
                    │     Mistral LLM      │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Meeting Chat UI    │
                    └──────────────────────┘
