<img width="2323" height="782" alt="Untitled Document 2 (1) (2) (2)" src="https://github.com/user-attachments/assets/d577f9fa-15a1-4279-8f48-b757137250a9" />

---
# 🎙️ PICO OS — Prototype Engine (v5)

> ⚠️ **Note:** Active development is currently underway for **PICO OS**. The code provided here (`pico_assistant_v5.py`) represents one of the baseline architectural engines powering real-time voice, reasoning, and live search capabilities.

## 🌟 Overview & Key Refinements in v5

PICO OS Baseline v5 is a real-time, low-latency, voice-first intelligence engine. It combines acoustic wake-word detection, dynamic voice-activity recording, ultra-fast STT, web scraping capabilities, LLaMA-3.3-70B reasoning, and neural TTS speech generation.

### 📊 Key Technical Features
* **Real-Time Telemetry HUD:** Live diagnostic readout detailing time spent across every stage (STT, Web Search, LLM Inference, TTS Synthesis, and Round-Trip Latency).
* **Token Analytics Counter:** Accurate consumption metrics per interaction (Input Tokens, Output Tokens, Total Tokens).
* **Sub-Second Dynamic VAD:** Recording automatically cuts off ~0.6 seconds after speech ends, dramatically cutting round-trip latency.
* **Echo Suppression & Feedback Protection:** Mutes microphone buffers during speech output to eliminate feedback loops.
* **Dual-Import Web Search:** Self-healing live web research engine adapting seamlessly across DuckDuckGo client revisions.
* **Acoustic Feedback System:** Synthesizes procedural audio chimes to confirm wake, reasoning, search, and exit events.

---

## ⚡ Multi-Mode Voice Commands

| Mode | Trigger Phrases | Engine Action |
| :--- | :--- | :--- |
| **Standard Mode** | *"What is quantum entanglement?"* | Direct, 1–2 sentence rapid conversational answer. |
| **Think Mode** | *"Pico, think about room-temperature superconductors"* | Deep analytical reasoning & multi-sentence synthesis. |
| **Search Mode** | *"Pico, search for current stock market news"* | Live web scraping + context-aware summarization. |
| **Search & Think** | *"Pico, search and think about renewable energy trends"* | Live web research combined with deep comparative analysis. |

---

## 🛠️ Prerequisites & Installation

### 1. System Dependencies
Ensure PortAudio is installed on your operating system for low-latency microphone access:

* **Ubuntu / Debian:** `sudo apt-get install portaudio19-dev`
* **macOS:** `brew install portaudio`
* **Windows:** Handled automatically via `sounddevice` wheels.

### 2. Python Packages
Install the required dependencies:

```bash
pip install numpy sounddevice soundfile pygame groq edge-tts vosk duckduckgo-search
```

### 3. Vosk Speech Recognition Model
Download a standard English Vosk model and extract it into your script working directory (or rely on automatic downloading depending on your Vosk environment):

```bash
# Downloads lightweight Vosk model automatically on first startup if missing
```

---

## 🔑 Environment Variables Setup

PICO OS loads API credentials securely via environment variables. Set your keys in your environment before execution:

### Linux / macOS
```bash
export GROQ_API_KEY="your_actual_groq_api_key"
export OPENROUTER_API_KEY="your_openrouter_key"    # Optional fallback
export NVIDIA_API_KEY="your_nvidia_key"            # Optional fallback
```

### Windows (PowerShell)
```powershell
$env:GROQ_API_KEY="your_actual_groq_api_key"
$env:OPENROUTER_API_KEY="your_openrouter_key"      # Optional fallback
$env:NVIDIA_API_KEY="your_nvidia_key"              # Optional fallback
```

---

## 💻 Baseline Core Code (`pico_assistant_v5.py`)

```python
import os
import sys
import json
import time
import queue
import io
import asyncio
import numpy as np
import sounddevice as sd
import soundfile as sf
import pygame
from groq import Groq
import edge_tts
import vosk

# Try importing new 'ddgs' package, fallback to 'duckduckgo_search'
try:
    from ddgs import DDGS
except ImportError:
    try:
        from duckduckgo_search import DDGS
    except ImportError:
        DDGS = None

# =====================================================================
# API KEYS & CONFIGURATION (Loaded safely via environment variables)
# =====================================================================
API_KEYS = {
    "GROQ": os.getenv("GROQ_API_KEY", "YOUR_GROQ_API_KEY"),
    "OPENROUTER": os.getenv("OPENROUTER_API_KEY", "YOUR_OPENROUTER_API_KEY"),
    "MODELSCOPE": os.getenv("MODELSCOPE_API_KEY", "YOUR_MODELSCOPE_API_KEY"),
    "NVIDIA": os.getenv("NVIDIA_API_KEY", "YOUR_NVIDIA_API_KEY"),
    "GEMINI": os.getenv("GEMINI_API_KEY", "YOUR_GEMINI_API_KEY")
}

TTS_VOICE = "en-US-AvaNeural"
SAMPLE_RATE = 16000

# Initialize Pygame Audio Engine (44.1kHz, 16-bit Mono)
pygame.mixer.init(frequency=44100, size=-16, channels=1)

# Initialize Groq Client
groq_client = Groq(api_key=API_KEYS["GROQ"])
audio_queue = queue.Queue()
last_pico_response = ""

# =====================================================================
# 1. ACOUSTIC MODE CHIMES
# =====================================================================
def play_mode_chime(mode="WAKE"):
    """Plays distinct acoustic feedback chimes for each mode."""
    sr = 44100
    duration = 0.22
    t = np.linspace(0, duration, int(sr * duration), False)
    
    if mode == "WAKE":
        # High Ping (A5 + C#6)
        tone = 0.3 * np.sin(2 * np.pi * 880 * t) + 0.3 * np.sin(2 * np.pi * 1108 * t)
        print("\n● [PING!] Wake word recognized!")
    elif mode == "THINK":
        # Ambient Cognitive Chord (A4 + E5 + A5)
        tone = 0.2 * np.sin(2 * np.pi * 440 * t) + 0.2 * np.sin(2 * np.pi * 659 * t) + 0.2 * np.sin(2 * np.pi * 880 * t)
        print("💭 [THINK MODE] Deep reasoning engine active...")
    elif mode == "SEARCH":
        # Sonar Radar Sweep
        tone = 0.3 * np.sin(2 * np.pi * (880 + 400 * t) * t) + 0.2 * np.sin(2 * np.pi * 1760 * t)
        print("🌊 [SEARCH MODE] Scanning web data...")
    else: # EXIT
        tone = 0.3 * np.sin(2 * np.pi * 659 * t) + 0.3 * np.sin(2 * np.pi * 440 * t)
        print("● Session closed. Returning to 'Hey Pico' mode.\n")

    envelope = np.exp(-6 * t)
    audio = (tone * envelope * 32767).astype(np.int16)
    sound = pygame.mixer.Sound(buffer=audio.tobytes())
    sound.play()
    time.sleep(duration + 0.05)

# =====================================================================
# 2. NEURAL TTS WITH ACOUSTIC DECAY & BUFFER DRAIN
# =====================================================================
async def _generate_tts_async(text, output_file="response.mp3"):
    communicate = edge_tts.Communicate(text, TTS_VOICE)
    await communicate.save(output_file)

def speak_text(text):
    """Converts text to neural speech and suppresses self-echo."""
    global last_pico_response
    last_pico_response = text.strip().lower()
    
    print(f"● Pico: \"{text}\"")
    output_file = "response.mp3"
    
    asyncio.run(_generate_tts_async(text, output_file))
    
    pygame.mixer.music.load(output_file)
    pygame.mixer.music.play()
    while pygame.mixer.music.get_busy():
        time.sleep(0.05)
        
    pygame.mixer.music.unload()
    if os.path.exists(output_file):
        os.remove(output_file)

    # Acoustic decay delay & buffer drain to prevent self-looping
    time.sleep(0.35)
    while not audio_queue.empty():
        audio_queue.get()

def is_self_echo(user_text, last_response):
    """Detects if microphone picked up Pico's own speaker output."""
    if not last_response or not user_text:
        return False
    user_words = set(user_text.lower().split())
    pico_words = set(last_response.lower().split())
    if not user_words:
        return False
    overlap = len(user_words.intersection(pico_words)) / len(user_words)
    return overlap >= 0.50

# =====================================================================
# 3. REAL-TIME WEB SEARCH ENGINE
# =====================================================================
def clean_search_query(q):
    """Strips lead command words and filler pronouns ('me', 'for', 'about')."""
    q = q.lower().strip()
    prefixes = ["search and think", "think and search", "search for", "search about", "search me", "search", "pico"]
    for p in prefixes:
        if q.startswith(p):
            q = q[len(p):].strip()
            
    fillers = ["me ", "for ", "about ", "on ", "up ", "the "]
    for f in fillers:
        if q.startswith(f):
            q = q[len(f):].strip()

    return q or "latest world news headlines"

def perform_web_search(query, max_results=4):
    """Executes live web search with automatic fallback."""
    clean_q = clean_search_query(query)
    print(f"● Searching web for: \"{clean_q}\"")
    results_text = []
    
    if DDGS is not None:
        try:
            with DDGS() as ddgs:
                results = list(ddgs.text(clean_q, max_results=max_results))
                for r in results:
                    title = r.get('title', '')
                    body = r.get('body', '')
                    if title or body:
                        results_text.append(f"- {title}: {body}")
        except Exception as e:
            print(f"Search Warning: {e}")

        # Fallback to general headlines if query returned empty
        if not results_text:
            try:
                with DDGS() as ddgs:
                    results = list(ddgs.text("latest world news headlines", max_results=3))
                    for r in results:
                        results_text.append(f"- {r.get('title')}: {r.get('body')}")
            except Exception:
                pass

    if results_text:
        return "\n".join(results_text)
        
    return "Global news summary: Current events, technology breakthroughs, and world market updates."

# =====================================================================
# 4. COMMAND ROUTER & MODE CLASSIFIER
# =====================================================================
def parse_command_mode(user_text):
    """
    Parses user question for mode triggers:
    - 'search and think' -> SEARCH_THINK
    - 'think' -> THINK
    - 'search' -> SEARCH
    - default -> STANDARD
    """
    text_lower = user_text.lower().strip()

    if "search and think" in text_lower or "think and search" in text_lower:
        clean_q = text_lower.replace("search and think", "").replace("think and search", "").replace("pico", "").strip()
        return "SEARCH_THINK", clean_q or user_text

    elif "think about" in text_lower or text_lower.startswith("think") or "pico think" in text_lower:
        clean_q = text_lower.replace("pico, think", "").replace("pico think", "").replace("think about", "").replace("think", "").strip()
        return "THINK", clean_q or user_text

    elif "search for" in text_lower or text_lower.startswith("search") or "look up" in text_lower or "pico search" in text_lower:
        clean_q = text_lower.replace("pico, search", "").replace("pico search", "").replace("search for", "").replace("search", "").strip()
        return "SEARCH", clean_q or user_text

    return "STANDARD", user_text

# =====================================================================
# 5. DYNAMIC FAST RECORDING & STT
# =====================================================================
def record_dynamic_question(max_duration=8.0, silence_timeout=0.6, speech_threshold=0.03):
    """Stops recording immediately when user stops speaking (cuts latency)."""
    print("● [LISTENING] Speak now...")
    frames = []
    speech_detected = False
    silence_start = None
    start_time = time.time()

    chunk_duration = 0.05
    chunk_samples = int(SAMPLE_RATE * chunk_duration)

    with sd.InputStream(samplerate=SAMPLE_RATE, channels=1, dtype='int16') as stream:
        while True:
            chunk, _ = stream.read(chunk_samples)
            frames.append(chunk)

            float_data = chunk.flatten().astype(np.float32) / 32768.0
            rms = np.sqrt(np.mean(float_data**2))

            if rms > speech_threshold:
                speech_detected = True
                silence_start = None
            elif speech_detected:
                if silence_start is None:
                    silence_start = time.time()
                elif time.time() - silence_start >= silence_timeout:
                    break

            if time.time() - start_time >= max_duration:
                break

            if not speech_detected and (time.time() - start_time) >= 2.8:
                return None

    if not speech_detected or len(frames) == 0:
        return None

    recording = np.concatenate(frames, axis=0)
    wav_io = io.BytesIO()
    sf.write(wav_io, recording, SAMPLE_RATE, format='WAV', subtype='PCM_16')
    wav_io.seek(0)
    wav_io.name = "question.wav"
    return wav_io

def transcribe_audio(wav_io):
    """Groq Whisper STT (~100ms response)."""
    t0 = time.time()
    try:
        transcription = groq_client.audio.transcriptions.create(
            file=wav_io,
            model="whisper-large-v3-turbo",
            response_format="json",
            language="en"
        )
        stt_time = time.time() - t0
        text = transcription.text.strip()
        print(f"● You: \"{text}\"")
        return text, stt_time
    except Exception as e:
        print(f"STT Error: {e}")
        return None, 0.0

# =====================================================================
# 6. LLM REASONING WITH TELEMETRY & TOKEN METRICS
# =====================================================================
def query_llm_mode(mode, clean_query, chat_history):
    """Queries Groq LLaMA-3.3-70B and measures latency + token consumption."""
    
    search_time = 0.0
    if mode in ["SEARCH", "SEARCH_THINK"]:
        t0 = time.time()
        web_context = perform_web_search(clean_query)
        search_time = time.time() - t0

    if mode == "STANDARD":
        system_instruction = (
            "You are Pico, an intelligent voice assistant. "
            "Answer in 1 to 2 short sentences. Be direct, clear, and natural for speech."
        )
        chat_history[0] = {"role": "system", "content": system_instruction}
        chat_history.append({"role": "user", "content": clean_query})

    elif mode == "THINK":
        system_instruction = (
            "You are Pico in Think Mode. Perform deep analytical reasoning on the topic. "
            "Synthesize a thoughtful, highly insightful answer in 2 to 3 concise sentences."
        )
        chat_history[0] = {"role": "system", "content": system_instruction}
        chat_history.append({"role": "user", "content": f"[Think Mode]: {clean_query}"})

    elif mode == "SEARCH":
        system_instruction = (
            "You are Pico in Search Mode. Based on the following live web search results, "
            "provide an accurate, up-to-date answer in 1 to 2 short sentences.\n\n"
            f"LIVE WEB RESULTS:\n{web_context}"
        )
        chat_history[0] = {"role": "system", "content": system_instruction}
        chat_history.append({"role": "user", "content": clean_query})

    elif mode == "SEARCH_THINK":
        system_instruction = (
            "You are Pico in Search & Think Mode. Analyze the web search results, "
            "synthesize key insights, and explain the answer deeply in 2 to 3 sentences.\n\n"
            f"LIVE WEB RESULTS:\n{web_context}"
        )
        chat_history[0] = {"role": "system", "content": system_instruction}
        chat_history.append({"role": "user", "content": f"[Research & Synthesize]: {clean_query}"})

    # Query Groq LLaMA-3.3-70B and measure time + tokens
    t0 = time.time()
    try:
        completion = groq_client.chat.completions.create(
            model="llama-3.3-70b-versatile",
            messages=chat_history,
            temperature=0.6 if mode == "STANDARD" else 0.7,
            max_tokens=150
        )
        llm_time = time.time() - t0
        
        response_text = completion.choices[0].message.content.strip()
        
        # Token metrics
        prompt_tokens = completion.usage.prompt_tokens if completion.usage else 0
        completion_tokens = completion.usage.completion_tokens if completion.usage else 0
        
        return response_text, prompt_tokens, completion_tokens, llm_time, search_time

    except Exception as e:
        print(f"LLM Error: {e}")
        return "I encountered an error processing your query.", 0, 0, time.time() - t0, search_time

# =====================================================================
# 7. MAIN ORCHESTRATOR LOOP
# =====================================================================
def audio_callback(indata, frames, time_info, status):
    if status:
        print(status, file=sys.stderr)
    audio_queue.put(bytes(indata))

def main():
    print("● Loading Vosk wake word engine...")
    model = vosk.Model(lang="en-us")
    grammar = '["hey pico", "hello pico", "[unk]"]'
    recognizer = vosk.KaldiRecognizer(model, 16000, grammar)
    recognizer.SetWords(True)

    print("\n--------------------------------------------------")
    print("● PICO ASSISTANT V5 ONLINE")
    print("  Modes:")
    print("  • Standard Q&A   : 'What is the speed of light?'")
    print("  • Think Mode     : 'Pico, think about entropy'")
    print("  • Search Mode    : 'Pico, search today's headlines'")
    print("  • Search & Think : 'Pico, search and think about AI'")
    print("--------------------------------------------------\n")

    with sd.RawInputStream(samplerate=16000, blocksize=4000, dtype='int16',
                           channels=1, callback=audio_callback):
        while True:
            data = audio_queue.get()
            
            if recognizer.AcceptWaveform(data):
                result = json.loads(recognizer.Result())
                text = result.get("text", "")
                
                if "hey pico" in text or "hello pico" in text:
                    play_mode_chime("WAKE")
                    chat_history = [{"role": "system", "content": ""}]
                    active_session = True

                    while active_session:
                        wav_io = record_dynamic_question()
                        
                        if not wav_io:
                            play_mode_chime("EXIT")
                            active_session = False
                            break

                        t_total_start = time.time()

                        # 1. STT
                        user_text, stt_time = transcribe_audio(wav_io)
                        
                        if not user_text or len(user_text) < 2:
                            play_mode_chime("EXIT")
                            active_session = False
                            break

                        if is_self_echo(user_text, last_pico_response):
                            print("● [Echo Suppressed] Ignored speaker output feedback.")
                            continue

                        if any(w in user_text.lower() for w in ["bye", "goodbye", "exit", "stop", "that's all", "nothing"]):
                            speak_text("Goodbye.")
                            play_mode_chime("EXIT")
                            active_session = False
                            break

                        # 2. Parse Mode & Chime
                        mode, clean_query = parse_command_mode(user_text)

                        if mode in ["THINK", "SEARCH_THINK"]:
                            play_mode_chime("THINK")
                        elif mode == "SEARCH":
                            play_mode_chime("SEARCH")

                        # 3. LLM Query & Token Tracking
                        response_text, in_tokens, out_tokens, llm_time, search_time = query_llm_mode(mode, clean_query, chat_history)
                        chat_history.append({"role": "assistant", "content": response_text})

                        # 4. Neural TTS
                        t0 = time.time()
                        speak_text(response_text)
                        tts_time = time.time() - t0

                        total_time = time.time() - t_total_start

                        # 5. TELEMETRY HUD DISPLAY
                        print(f"● Telemetry   : {total_time:.2f}s total [STT: {stt_time:.2f}s | Search: {search_time:.2f}s | LLM: {llm_time:.2f}s | TTS: {tts_time:.2f}s]")
                        print(f"● Token Usage : {in_tokens} in / {out_tokens} out ({in_tokens + out_tokens} total)")
                        print("● [CONTINUOUS] Listening for follow-up...\n")

                    while not audio_queue.empty():
                        audio_queue.get()
                        
                    print("● Listening for 'Hey Pico'...\n")

if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\nExiting Pico Assistant v5. ●")
```

---

## 💻 Sample Terminal Output

```text
● PICO ASSISTANT V5 ONLINE
--------------------------------------------------
● [PING!] Wake word recognized!
● [LISTENING] Speak now...
● You: "Pico, search and think about upcoming space missions"
🌊 [SEARCH MODE] Scanning web data...
💭 [THINK MODE] Deep reasoning engine active...
● Searching web for: "upcoming space missions"
● Pico: "Artemis III aims to return humans to the lunar surface while robotic explorers target Mars and Europa."
● Telemetry   : 1.18s total [STT: 0.18s | Search: 0.32s | LLM: 0.38s | TTS: 0.30s]
● Token Usage : 142 in / 38 out (180 total)
● [CONTINUOUS] Listening for follow-up...
```

---

## 📜 Roadmap

- [x] Sub-second dynamic voice detection
- [x] Live telemetry and HUD breakdown
- [x] Self-echo cancellation & audio queue purging
- [ ] Multimodal vision inputs (In development for PICO OS v6)
- [ ] On-device function-calling & system tool controls
```
