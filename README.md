# MeetingMind 🧠
> AI-powered meeting assistant that turns any transcript into structured 
> action items, summaries, calendar events, and automated emails — in seconds.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Flask](https://img.shields.io/badge/Flask-3.0-black?style=flat-square&logo=flask)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.3%2070B-orange?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

## 🌐 Live Demo

🚀 **Try it live:** https://meetingmind-jxb3.onrender.com

> Note: First load may take 30-50 seconds as the 
> free server wakes up. Please be patient!

---

## 🚀 What is MeetingMind?

MeetingMind is an AI-powered meeting assistant that eliminates the most 
painful part of every meeting — manually tracking who needs to do what, 
by when, and following up with everyone.

Paste any meeting transcript (or upload audio, or record live in your browser) 
and MeetingMind instantly:
- Extracts every action item
- Assigns it to the right person
- Detects deadlines and priority levels
- Emails all assignees automatically
- Exports to Google Calendar, PDF, and Excel

---

## ✨ Features

| Feature | Description |
|---|---|
| 🤖 AI Action Item Extraction | Extracts who does what by when using LLaMA 3.3 70B |
| 📊 Meeting Summary | Auto-generates a concise 2-3 sentence summary |
| 🎙️ Audio Transcription | Upload audio/video files up to 1GB — ffmpeg compresses to mono MP3 at 16kHz, then Groq Whisper transcribes in seconds |
| 🎙️ Live Meeting Recording | Record directly in the browser using your microphone — real-time transcription with pause/resume, multi-language support, and live waveform. Powered by Web Speech API. Works best on Chrome and Edge. |
| 📧 Email Assignees | Send action items to assignees via Brevo REST API with Google Calendar links |
| 📅 Calendar Export | Download .ics file for Google Calendar, Outlook, Apple Calendar |
| 📄 PDF Export | Professional branded PDF report with summary and action items |
| 📊 Excel Export | Color-coded Excel file with priority highlighting |
| 💬 Chat with Meeting | Ask follow-up questions about the transcript |
| ✏️ Editable Items | Fix AI mistakes inline before exporting |
| 🌗 Dark / Light Mode | Full theme support |

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Backend | Flask (Python) |
| AI Extraction & Chat | Groq API — LLaMA 3.3 70B |
| Audio Transcription | Groq Whisper API (whisper-large-v3) with ffmpeg compression |
| Audio Processing | ffmpeg (extract audio, convert to mono MP3 at 16kHz) |
| Email Delivery | Brevo REST API (api.brevo.com) |
| PDF Generation | ReportLab |
| Excel Generation | OpenPyXL |
| Live Recording | Web Speech API (built-in browser API — no install needed) |
| Frontend | HTML + CSS + Vanilla JavaScript |

---

## ⚙️ Setup & Installation

### Prerequisites
- Python 3.10+
- **ffmpeg** installed and available in PATH (required for audio/video transcription)
  - Windows: `choco install ffmpeg` or download from [ffmpeg.org](https://ffmpeg.org/download.html)
  - Mac: `brew install ffmpeg`
  - Linux: `sudo apt install ffmpeg`
- A Groq API key (free at https://console.groq.com)
- A Brevo API key (free at https://www.brevo.com — sign up and get API key from SMTP & API section)

### 1. Clone the repository
```bash
git clone https://github.com/yourusername/MeetingMind.git
cd MeetingMind
```

### 2. Create and activate virtual environment

**Windows (PowerShell):**
```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Mac/Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Create .env file
Create a `.env` file in the project root:
```
GROQ_API_KEY=your_groq_api_key_here
SENDER_EMAIL=your_sender_email@example.com
BREVO_API_KEY=your_brevo_api_key_here
```

### 5. Run the application
```bash
python app.py
```

Then open `http://127.0.0.1:5000/` in your browser.

---

## 📖 How to Use

1. **Input your meeting**
   - Paste a transcript directly
   - Upload an audio/video file up to 1GB (ffmpeg automatically compresses to mono MP3 at 16kHz for faster transcription)
   - Record live in the browser using your microphone (Chrome/Edge recommended)

2. **Extract insights**
   - Click **Submit** to generate action items and meeting summary
   - AI automatically detects: person responsible, deadline, and priority

3. **Review and edit**
   - Double-click any action item to edit inline
   - Add or change assignee emails in the Email tab

4. **Share and export**
   - **Send Emails** — Automatically notifies all assignees
   - **Export PDF** — Professional report for stakeholders
   - **Export Excel** — Color-coded action items spreadsheet
   - **Export Calendar** — .ics file for Google/Outlook/Apple Calendar

5. **Chat for clarity**
   - Ask follow-up questions about the meeting in the Chat tab

---

## 📸 Screenshots

### Home Page
![MeetingMind Home](screenshots/hero.png)

### Action Items Extracted
![Action Items](screenshots/action_items.png)

### PDF Export
![PDF Report](screenshots/pdf_export.png)

### Email Sent
![Email](screenshots/email.png)

---

## 🔒 Environment Variables

| Variable | Required | Description |
|---|---|---|
| `GROQ_API_KEY` | Yes | API key for LLaMA 3.3 70B and Whisper transcription (get at [console.groq.com](https://console.groq.com)) |
| `SENDER_EMAIL` | Yes | Gmail address used to send emails |
| `BREVO_API_KEY` | Yes | API key from Brevo (get at [brevo.com](https://www.brevo.com) → SMTP & API → API Keys) |

---

## 🐛 Bug Fixes / Changelog

### v1.4 (Latest)
- **Switched email delivery from Gmail SMTP to Brevo REST API** —
  More reliable transactional email delivery via Brevo (formerly Sendinblue).
  Requires BREVO_API_KEY instead of SENDER_APP_PASSWORD.

### v1.3
- **Replaced YouTube URL input with Live Meeting Recording** — 
  Users can now record directly in the browser using the Web Speech API.
  Supports pause/resume, live waveform, timestamps, and multi-language 
  transcription. No API key or extension required.
- **Removed youtube-transcript-api dependency** — No longer needed.

### v1.2
- **Added ffmpeg audio compression** — Before sending to Groq Whisper, files are compressed to mono MP3 at 16kHz (reduces 72MB video to under 5MB)
- **Increased file size limit to 1GB** — Backend now accepts files up to 1GB (compressed before transcription)
- **Removed AssemblyAI** — Switched back to Groq Whisper with ffmpeg preprocessing for better reliability
- **Added ffmpeg-python to requirements** — For audio processing capabilities

### v1.1
- **Fixed calendar events appearing on wrong dates** — AI now receives today's date in the prompt and returns all deadlines as ISO format (YYYY-MM-DD) instead of vague text like "Wednesday" or "next Friday"
- **Switched to Gmail SMTP for email delivery** — More reliable delivery and better spam folder avoidance
- **Fixed iCal zero-duration events** — DTEND is now correctly set to deadline date + 1 day (per iCal spec for all-day events)
- **Fixed ambiguous date format parsing** — Removed dd/mm vs mm/dd conflict by standardizing on ISO format

---

## �️ License

MIT License — feel free to use for personal or commercial projects.

---

## 🙏 Acknowledgments

- [Groq](https://groq.com) for blazing-fast LLaMA inference
- [Groq Whisper API](https://console.groq.com) — Ultra-fast cloud audio transcription
- [ffmpeg](https://ffmpeg.org/) for audio/video processing
- [ReportLab](https://www.reportlab.com/) for PDF generation

---

<p align="center">Built with ❤️ for teams who hate busywork</p>
