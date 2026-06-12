# AI-Video-Assistant
Transcribe any YouTube video or audio file, extract action items, decisions, open questions, and chat with the content using RAG. Supports English, Hindi, and Hinglish.

No more paying for Otter.ai or Fireflies. This does everything they do — transcription, summarisation, action items, and chat with your meeting — completely free.

---

## What This Does

You give it a YouTube URL or an audio/video file. It handles the rest.

| Feature | Description |
|---|---|
| Transcription (English) | Local OpenAI Whisper — runs on your machine, no API cost |
| Transcription (Hindi/Hinglish) | Sarvam AI for mixed-language Indian meetings |
| Summarisation | Bullet-point summary of the full meeting |
| Action Items | Extracted with owner and deadline |
| Key Decisions | What was agreed upon |
| Open Questions | Follow-ups that need answers |
| Chat with Meeting | Ask anything — powered by RAG + ChromaDB |
| Export | Full report as PDF or TXT |

---

## Tech Stack

```
Python
├── OpenAI Whisper       → Local speech-to-text (English), free
├── Sarvam AI            → Hindi / Hinglish transcription
├── LangChain LCEL       → Modern pipeline orchestration
├── Mistral AI           → LLM for summarisation & extraction (free API)
├── ChromaDB             → Vector store for RAG
├── HuggingFace          → Local embeddings, free
└── Streamlit            → UI
```

---

## Project Structure

```
AI-Meeting-Assistant/
├── utils/
│   └── audio_processor.py   # Extract & optimise audio from video/YouTube
├── transcriber.py            # Whisper + Sarvam transcription logic
├── translator.py             # Hindi/Hinglish → clean English
├── summarise.py              # Meeting summarisation via LangChain + Mistral
├── extractor.py              # Action items, decisions, open questions
├── vector_store.py           # Embeddings + ChromaDB storage
├── rag_engine.py             # RAG pipeline for chat
├── main.py                   # Orchestrator — ties all modules together
├── app.py                    # Streamlit UI
├── requirements.txt
└── .env
```

---

## Setup

**1. Clone the repo**
```bash
git clone https://github.com/YOUR_USERNAME/AI-Meeting-Assistant
cd AI-Meeting-Assistant
```

**2. Create a virtual environment**
```bash
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Add your `.env` file**
```env
MISTRAL_API_KEY=your_mistral_key
SARVAM_API_KEY=your_sarvam_key
```

Get your free keys:
- Mistral AI → https://console.mistral.ai
- Sarvam AI → https://dashboard.sarvam.ai

**5. Run the app**
```bash
streamlit run app.py
```

---

## How It Works

```
Input (YouTube URL / audio / video)
        |
Audio Extraction & Optimisation
        |
Transcription  -->  English?  --> Whisper (local)
               \--> Hindi?    --> Sarvam AI --> Translate to English
        |
LangChain + Mistral
  ├── Summarise
  ├── Extract Action Items
  ├── Extract Decisions
  └── Extract Open Questions
        |
ChromaDB Vector Store (HuggingFace Embeddings)
        |
RAG Chat Interface  +  PDF / TXT Export
```

---

## What I Learned

The trickiest part was handling Hindi/Hinglish audio — Whisper alone doesn't do a great job with code-switched speech, so Sarvam AI fills that gap cleanly. Chaining the translation step into the LangChain pipeline before summarisation made the whole flow consistent regardless of the meeting language.

Structuring the RAG retrieval for meeting-specific Q&A also needed careful chunking — meetings have a lot of filler context, so tuning chunk size and retrieval parameters made a noticeable difference in answer quality.

---

## Related Projects

- [Multi-Agent AI Research System](https://github.com/Himanshu25589/Multi-Agent-Research-System) — 4-agent pipeline that searches the web, reads sources, writes a report, and critiques it automatically.

---

**Himanshu Saini — DTU '28**  
[LinkedIn](https://linkedin.com/in/your-profile) · [GitHub](https://github.com/Himanshu25589)
