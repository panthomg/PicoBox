<img width="16219" height="7525" alt="Untitled Document 2 (2)" src="https://github.com/user-attachments/assets/384f5fc0-6738-462b-bef4-029c18ea133e" />

# ALL THE SOFTWARE SPECIFICATIONS

<img width="6969" height="1611" alt="Untitled Document 2 (1) (1) (4)" src="https://github.com/user-attachments/assets/db4a74b1-9119-4647-abe4-44eaaebdeed1" />



> To enhance the software quality and time spent on development, AI would be used in developing the software end.

---

## 5. Software Architecture

### 5.1 Operating System

* **OS:** Debian Linux (pre-installed on UNO Q)
* **Python Version:** 3.11+
* **Package Managers:** `pip` + `apt`

### 5.2 Complete Software Stack

```
┌─────────────────────────────────────────────────────────────────┐
│                      APPLICATION LAYER                          │
├─────────────────────────────────────────────────────────────────┤
│  • FastAPI + Uvicorn (Web Framework & WebSocket)                │
├─────────────────────────────────────────────────────────────────┤
│                      CORE SERVICES                              │
├─────────────────────────────────────────────────────────────────┤
│  • Wake Word (Porcupine)   • Speaker Verification (Eagle)       │
│  • Speech-to-Text (Vosk)   • Text-to-Speech (Piper)             │
│  • VAD (Silero)           • Command Router                      │
├─────────────────────────────────────────────────────────────────┤
│                     AI INTEGRATION                              │
├─────────────────────────────────────────────────────────────────┤
│  • DeepSeek V4 API (Flash/Pro)                                  │
│  • Web Search (DuckDuckGo / Tavily)                             │
│  • Spotify API / librespot                                      │
│  • YouTube Data API + yt-dlp                                    │
│  • Google Calendar API                                          │
├─────────────────────────────────────────────────────────────────┤
│                      SYSTEM LAYER                               │
├─────────────────────────────────────────────────────────────────┤
│  • Debian Linux            • PulseAudio       • Python 3.11     │
│  • Wi-Fi/Bluetooth Stack   • GPIO Drivers                       │
└─────────────────────────────────────────────────────────────────┘

```

### 5.3 Audio Pipeline

```
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  Microphone  │───▶│   Wake Word  │───▶│  Speech-to-  │───▶│    Command   │
│  (ReSpeaker) │    │  Detection   │    │   Text (STT) │    │    Router    │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘
                                                                           │
                                                                           ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│   Speaker    │◀───│  Text-to-    │◀───│ DeepSeek API │◀───│   Command    │
│  (Output)    │    │  Speech (TTS)│    │   (Cloud)    │    │   Executor   │
└──────────────┘    └──────────────┘    └──────────────┘    └──────────────┘

```

### 5.4 Command Router Logic

```python
def route_command(transcribed_text):
    text = transcribed_text.lower()
    
    if "search and think" in text or "think and search" in text:
        # Mode: Research & Synthesis
        query = clean_query(text, ["search and think", "think and search"])
        web_results = perform_web_search(query)
        response = call_deepseek(query, context=web_results, mode="synthesis")
        
    elif "search" in text:
        # Mode: Factual Retrieval
        query = clean_query(text, ["search"])
        web_results = perform_web_search(query)
        response = call_deepseek(query, context=web_results, mode="summarize")
        
    elif "think" in text:
        # Mode: Creative/Reasoning
        query = clean_query(text, ["think"])
        response = call_deepseek(query, mode="creative")
        
    else:
        # Default: Conversational
        response = call_deepseek(text, mode="conversational")
        
    return response

```

### 5.5 DeepSeek Integration

| Model | Best For |
| --- | --- |
| **V4-Flash** | Daily Q&A, web searches, timers |
| **V4-Pro** | Complex reasoning, creative writing |

> **Note:** Peak Usage Windows apply daily during heavy processing schedules (9:00 AM–12:00 PM & 2:00 PM–6:00 PM Beijing Time).

---

## 6. Features & Capabilities

### 6.1 Core Features

| Feature | Description |
| --- | --- |
| **Wake Word** | "Hey Pico" (customizable via web app) |
| **Owner Verification** | Voiceprint-based user authentication (Picovoice Eagle) |
| **Smart Interrupt** | Barge-in capability during TTS playback (Silero VAD) |
| **Three Command Modes** | Think / Search / Think & Search |
| **Web Search** | Real-time information retrieval and extraction |
| **Media Playback** | Spotify + YouTube audio streaming support |
| **Smart Home Control** | Integration via MQTT, Matter, and WiZ lights |
| **Calendar Management** | Google Calendar automated schedule integration |
| **Multi-User** | Multiple unique voiceprints for family or team settings |
| **Privacy-First** | Zero data collection; voice processing remains local where possible |

### 6.2 Voice Interaction Flow

```
User: "Hey Pico"
   ↓
Pico: Verifies voiceprint (owner-only mode)
   ↓
Pico: "Listening..." (LED status light turns on)
   ↓
User: "Think... write a poem about AI"
   ↓
Pico: STT transcribes → Router flags the "think" modifier
   ↓
Pico: Dispatches DeepSeek API call (pure model generation)
   ↓
Pico: TTS engine parses payload and synthesizes audio stream
   ↓
Pico: Responds aloud via hardware speaker
   ↓
User: Interrupts vocal payload mid-sentence
   ↓
Pico: Immediate stream termination → Resets to listen for subsequent command

```

### 6.3 DeepSeek Command Modes

| Mode | Trigger Phrase | Action | Example |
| --- | --- | --- | --- |
| 💭 **Think** | *"Pico, think..."* | Pure LLM generation (creative layout & logic reasoning) | *"Write a poem about the ocean"* |
| 🔍 **Search** | *"Pico, search..."* | Targeted web crawl followed by semantic LLM summarization | *"What's the latest news on AI?"* |
| 🧠 **Think & Search** | *"Pico, search and think..."* | Broad web fetch followed by deep contextual synthesis | *"How will AI change education?"* |
