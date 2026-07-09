<img width="6951" height="3225" alt="Untitled Document 2 (1)" src="https://github.com/user-attachments/assets/fc2be432-f714-4b43-b5ba-200988178e2c" />

# PICO — Hands-Free Voice AI Assiant Speaker 
> Note: Everything written below is written/typed by a human please don't mind mistakes. A human can make mistake.


> **"For those who ask. For those who question."**
Introducing Pico, a smart LLM based assitant speaker built for your you, for your home. Pico is more than just assitant, it is someone who will satisfy your thirst of questions, generative and brainstorm expert will help you think and brainstorm new ideas or projects you working on, research companion, your mentor, your helper in day to day life, Pico can help you with any thing from cooking to philosphy to complex science questions, to fact checking, to checking news and match stores, weather broadcast, your music streaming dj/speaker with support of Spotify.
Freedom to ask anything. Pico is for students, for professionals, for the elderly, for anyone who asks. Knowledge should be accessible to everyone with Pico. 
Pico talks to you in your natural language. You don't type you speak what you want to. Pico is there to understand you and help you regarding nearly infinite topics and things.


# Just say "Hey Pico"
> **4-5 meter range, across the room**
> **Have it remember your voice and memories with you**
> **Always ready to answer anything you ask 24/7 at your service**
> **Use any LLM Model you want, your choice. Add custom commands, personality, actions, etc.**
> **Unlike other electronics with support LLM like your phone and pcs, Pico stands distraction free dedicated for you reach your motive.** 


Unlike conventional smart speakers, Pico offers an open, modular ecosystem. It gives users complete agency over their hardware and software: choose any AI model (from cloud APIs to local offline models), configure custom voice triggers, set hard token budgets, and manage the device through a responsive React companion web app.


# Why Pico exist? Why is it the best in its field/Niche?

- Pico is extremly customizable from LLM model selection, to your voice pick up, to Pico's custom voice and personality.
- Each family member can recieve a unique personality and memories realted to them with voice identification
- Pico works with LLM API KEYS, your own api keys stored locally encrypted. Select any model you like.
- Pico can search internet *(depends on LLM model)*, Pico has ability to think before answering *(depends on LLM model)*
- Unlike a phone, you don't have to touch or type anything just call "Hey Pico" and ask. This makes it way easier for younger children to seek for knowledge or senior citizens access such powerful LLMs without them having to deal with complex user interfaces on phone they can use their voice and recieve answer in voice significantly redcuing the time spent on getting you work done. Your phone is designed for the young and tech-savvy. Pico is designed for everyone.
- 🙌 Truly Hands-Free : When you're cooking, writing, or working—you can't use your phone. Pico is always available.
- Stationary, always in the room plugged, No notifications, Built for the space


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
