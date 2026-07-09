<img width="6951" height="3225" alt="Untitled Document 2 (1)" src="https://github.com/user-attachments/assets/fc2be432-f714-4b43-b5ba-200988178e2c" />
<img width="16219" height="7525" alt="Untitled Document 2 (2)" src="https://github.com/user-attachments/assets/621c2ef2-973c-41c4-b945-e500d4c8432b" />
<img width="11585" height="5375" alt="Untitled Document 2" src="https://github.com/user-attachments/assets/a34b2cce-6f3c-4e3b-97ca-45fe082d3a3d" />
# PICO — The Universal, Hands-Free Voice AI Assistant

> **"For those who ask. For those who question."**

Pico is a physical, hands-free voice-activated AI companion built on the **Arduino UNO Q 4GB** single-board computer and the **ReSpeaker XVF3800 4-Mic Array**. 

Unlike conventional smart speakers, Pico offers an open, modular ecosystem. It gives users complete agency over their hardware and software: choose any AI model (from cloud APIs to local offline models), configure custom voice triggers, set hard token budgets, and manage the device through a responsive React companion web app.

---

## 🚀 Key Features

*   **Universal AI Integration:** Swap backend LLM engines seamlessly. Supports DeepSeek (V4-Flash & V4-Pro), OpenAI, Anthropic, Google Gemini, Groq, or local offline models using Ollama.
*   **True Hands-Free Interaction:** Uses a professional-grade 4-microphone array with XMOS XVF3800 hardware processing for 360° far-field voice tracking (up to 5 meters) and Acoustic Echo Cancellation (AEC).
*   **Smart Interrupt (Barge-In):** Features real-time Voice Activity Detection (VAD) via Silero. Interrupt Pico mid-sentence simply by speaking, without needing physical buttons or wake-word repeating.
*   **Three Interaction Modes:**
    *   `Think Mode`: Pure on-device/LLM generation for reasoning, creative tasks, and coding help.
    *   `Search Mode`: Direct web-search queries with concise summaries.
    *   `Think & Search Mode`: Multi-turn, deep-synthesis queries that research online databases and compile detailed analytical responses.
*   **Sleek Companion Web App:** Control settings, customize responses, view real-time chat logs, monitor token consumption, and manage connected services through a cross-platform dashboard.
*   **Hardware and Smart Home Hub:** Modular connectivity for Spotify streaming, YouTube audio extraction (`yt-dlp`), and direct IoT control (MQTT, Matter, and WiZ smart bulbs).

---

## 🛠️ System Architecture

Pico leverages the hybrid dual-processor design of the Arduino UNO Q to segregate real-time audio handling from heavy AI logic, preventing playback jitter.
