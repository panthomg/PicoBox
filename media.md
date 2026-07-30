<table>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/91856950-b66e-4197-b6a5-96c8e9e025e6" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/77c8a730-fbf3-4cd9-8379-23551eac4701" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/70581c3d-7e4d-475a-b993-8b0d721f05cb" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/93de1c08-e156-48ae-9a5f-e4a332d4e14e" width="100%"/></td>
  </tr>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/e6177890-18fb-4d30-9d57-cd728cc2bd5e" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/42935b8f-6655-42a2-a710-babdf166df94" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/6aadad71-89f0-4b3b-b29b-29d38e3b1cd8" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/2a131914-7ef6-44e3-bd6b-7f98125b17e9" width="100%"/></td>
  </tr>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/8ded8bde-bd0d-4bd4-b6f3-f9f353ed675b" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/a6c1c3cf-4feb-4ffc-b119-147e4ed91f46" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/104cc715-fa62-4ff1-ba66-58e8c3aa0efd" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/1f1d25d9-b756-4ae6-abb7-bacf85eab010" width="100%"/></td>
  </tr>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/9e1e9cc5-5577-42a9-9bee-e7a23068a259" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/ead8f0e5-5fdd-4a8e-b7aa-3d2db9a7583c" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/76ea6aac-66c6-4a39-8e20-57062b1ec092" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/b48db035-c9ef-427b-b98d-26cfdb0d0163" width="100%"/></td>
  </tr>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/a52242f9-4a20-4d95-8981-f8b48dcd49ab" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/4a93a0bb-6f84-46ba-a52c-bb2760e33f40" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/90e19e03-cfaf-425d-8168-75b419b308ac" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/3d0ddd86-cc71-43d9-bc2d-5a1280111d60" width="100%"/></td>
  </tr>
  <tr>
    <td width="25%"><img src="https://github.com/user-attachments/assets/482cab2b-57a2-4d5b-bd2f-b5ee007ee393" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/6c835900-5855-47d8-904f-8a58c409fff2" width="100%"/></td>
    <td width="25%"><img src="https://github.com/user-attachments/assets/da62b8d4-0a83-45cd-9f5b-68b2d81f417a" width="100%"/></td>
    <td width="25%"></td>
  </tr>
</table>
# ● pico

*a voice, not a gadget*

Say its name. It answers. Say nothing. It doesn't.

Pico is a hands-free voice AI object built on the Arduino UNO Q. No screen. No app. No lock-in to one company's model. A four-microphone ring, a single hidden LED, and a mind you choose yourself.

○ status: prototype / competition build. not yet open. this document is the full feasibility record.

---

## contents

01 — [what it is](#01--what-it-is)
02 — [why not a phone](#02--why-not-a-phone) ← the long answer
03 — [the object](#03--the-object)
04 — [the mind](#04--the-mind)
05 — [architecture](#05--architecture)
06 — [hardware](#06--hardware)
07 — [software](#07--software)
08 — [quick start](#08--quick-start)
09 — [the web app](#09--the-web-app)
10 — [who asks](#10--who-asks)
11 — [what it costs](#11--what-it-costs)
12 — [what it costs to run](#12--what-it-costs-to-run)
13 — [speed](#13--speed)
14 — [what's next](#14--whats-next)
15 — [the manifesto](#15--the-manifesto)
16 — [how it came to be](#16--how-it-came-to-be)
17 — [license](#17--license)

---

## 01 — what it is

**pico.**
*a stationary object that listens for its name.*

Say "hey pico" and ask anything. It searches. It thinks. It answers, out loud, in a voice that doesn't sound like a phone reading a script at you.

● no screen — the answer is spoken, not displayed
● no app — the object *is* the interface
● no single owner of the mind behind it — DeepSeek, OpenAI, Claude, Gemini, Groq, or a fully offline model, your choice, switchable anytime
● no single owner of the room — every voice in the house gets its own profile
● no performance of "smartness" — it does one thing, well, and is quiet the rest of the time

Why it exists: because every assistant before this one wanted your attention. This one only wants your question. ●

---

## 02 — why not a phone

*the long answer, because this is the question everyone asks first.*

A phone is the most over-subscribed object a person owns. It is a camera, a wallet, a ledger of every anxiety you've ever had at 2 a.m., a television, a keyboard, and — almost incidentally — a way to ask a question out loud. Every time you use it as a voice assistant, you are borrowing attention from an object whose entire design is built to capture attention. You unlock it. You find the app. You tap the mic icon. You speak *into* it, close to your face, because it can't hear you from across the room. Then you put it back in your pocket, and the sixteen notifications waiting underneath the answer pull you somewhere else entirely.

Pico does not have this problem, because Pico cannot do anything else. That is the whole point.

**the physical argument**

A phone's microphone is built for a call held to your ear, not a room. Pico's is a four-element far-field array tuned for 360°, five-meter pickup — you can be at the stove, across the room, mid-task, hands full, and it hears you the same as if you were standing next to it. This is not a workaround. It is the reason the object exists in the room at all: a phone asks you to come to it; Pico comes to you.

**the attentional argument**

Every phone interaction carries the tax of everything else the phone is. You cannot ask a phone a question without also being one glance away from your email, your group chat, your feed. Pico has no email, no group chat, no feed. It cannot distract you, because it was never built to. A single-purpose object is calmer than a multi-purpose one by construction, not by discipline.

**the ownership argument**

A phone's assistant is whichever one the manufacturer chose for you, permanently, unless you route around it with effort. Pico was built the other way: the voice pipeline — wake word, hearing, understanding — is fixed and yours, but the *mind* behind the answer is not. DeepSeek today, a local model tomorrow, Claude for the questions that need care, a cheap fast model for the ones that don't. You are not locked into a company's roadmap. You are choosing a brain the way you'd choose a book.

**the household argument**

A phone recognizes an owner, singular. Pico recognizes a household — each voiceprint its own profile, its own permissions, its own thread of context. Ask your child "what's my thing today," and it means their homework. Ask it as a parent, and it means the calendar. One phone per person is the default; one Pico can quietly serve everyone in the room, correctly, because it knows who is speaking.

**the interruption argument**

Try talking over a phone assistant mid-answer. Mostly you can't — you wait, or you tap to cancel, both of which are small defeats. Pico has smart interrupt: talk over it, and it stops and listens, the way a person would. This single behavior does more for the feeling of "this is alive" than any amount of voice-quality tuning.

**the compounding argument**

A phone is replaced every two to three years, its assistant re-taught from zero each time. Pico is a fixed point in the room. It accumulates — your voiceprint, your preferences, your history — the way a good chair accumulates the shape of the person who sits in it. Permanence is a feature phones structurally cannot offer, because permanence isn't profitable for them.

**in one line:** a phone is engineered to be everything, which means it can never fully be *this* — an object whose only ambition is to hear you and answer. Pico gives up everything else in exchange for doing the one thing properly.

| | phone assistant | pico |
|---|---|---|
| distance | must hold near face | 5 m, any direction |
| attention cost | shares you with notifications | has nothing else to offer |
| the mind | fixed by the manufacturer | your choice, switch anytime |
| the household | one owner | a voiceprint per person |
| interruption | wait or cancel | talk over it, it listens |
| lifespan | replaced, re-taught | a fixed point that accumulates you |
| screen | required | none — the answer is spoken |

| | pico | alexa | google | siri |
|---|---|---|---|---|
| far-field, hands-free | ● | ● | ● | ● |
| any AI model, switchable | ● | ○ | ○ | ○ |
| custom wake word | ● | ◐ | ◐ | ◐ |
| custom personality | ● | ○ | ○ | ○ |
| per-person voiceprint | ● | ● | ● | ◐ |
| smart interrupt | ● | ● | ● | ○ |
| open, unlocked ecosystem | ● | ○ | ○ | ○ |

● yes ◐ partial ○ no

---

## 03 — the object

**form.** a single volume, small enough for a shelf, shaped so it never quite looks like it's facing you. no visible seams where a seam isn't needed.

**hearing.** four microphones set flush into the top edge — invisible until you know to look for them. 360° pickup, five-meter range, noise suppression tuned for a room, not a call.

**speaking.** one small driver, tuned for a voice, not for music. it doesn't need to fill a room with bass. it needs to sound like someone answering you.

**light.** a single LED, hidden under the surface, glowing *through* the material rather than out of a cutout. off when idle. a soft pulse when listening. a slow ambient wash when thinking. a brief flare when it has an answer.

**sound design.** a soft chime on wake, a gentle ambient tone while it thinks, nothing sharp, nothing that sounds like a notification. the sound of *attention being paid*, not an alert.

**the hidden feature.** go quiet with it for a few days and it hums once — not a reminder, not a nudge to re-engage, just a small sound that means *still here, still curious.*

---

## 04 — the mind

Pico does not have an opinion about which AI you should use. It has a socket, and you put a mind into it.

| provider | models | roughly |
|---|---|---|
| DeepSeek | V4-Flash, V4-Pro | ₹13–83 / 1M tokens |
| OpenAI | GPT-4o, GPT-4o Mini, o1 | $0.15–60 / 1M tokens |
| Anthropic | Claude 3.5 Sonnet, Haiku | $1–75 / 1M tokens |
| Google | Gemini 2.0 Flash, 1.5 Pro | free – $10 / 1M tokens |
| Groq | Llama 3.3, Mixtral | free tier |
| Ollama | Llama 3.2, Mistral, Gemma | free — runs locally, no cloud at all |
| custom | anything API-compatible | varies |

Bring your own key. Switch providers the way you'd change a lightbulb — the object doesn't notice, it just answers differently.

**three ways to ask:**

| say | it does |
|---|---|
| "pico, think..." | pure reasoning. no web. just the mind, thinking. |
| "pico, search..." | live web search, summarized. |
| "pico, search and think..." | research, then synthesis. the deep version. |

---

## 05 — architecture

```
you: "hey pico"
        │
        ▼
┌───────────────────────────────────────┐
│ wake word (Porcupine)                 │
│ always listening, on-device, < 50 ms  │
└───────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ speaker verification (Eagle)          │
│ voiceprint match — who is speaking    │
└───────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ speech-to-text (Vosk)                 │
│ offline, ~200 ms                      │
└───────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ command router                        │
│ think / search / search & think       │
└───────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ the mind — your provider of choice    │
│ DeepSeek · OpenAI · Anthropic ·       │
│ Google · Groq · Ollama · custom       │
└───────────────────────────────────────┘
        │
        ▼
┌───────────────────────────────────────┐
│ text-to-speech (Piper)                │
│ offline, neural, not robotic          │
└───────────────────────────────────────┘
        │
        ▼
pico: "here's what I found..."
```

Two brains, one body. The Qualcomm side runs the mind — the model, the search, the speech. The STM32 side runs the body — the microphones, the button, the light, the speaker — in real time, without waiting on anything.

| processor | job |
|---|---|
| Qualcomm CPU (Linux) | the mind — AI, STT, TTS, web search |
| STM32 MCU (Arduino) | the body — mic input, button, speaker, LED, always on time |

---

## 06 — hardware

### the full build

| part | model | price (INR) | note |
|---|---|---|---|
| board | Arduino UNO Q 4GB | ₹6,399 | quad-core 2.0 GHz, 4GB RAM |
| ears | ReSpeaker XVF3800, 4-mic | ₹5,899 | 5 m, 360°, noise suppression |
| voice | USB 2.0 speaker | ₹600 | |
| power | 5V/3A USB-C | ₹580 | |
| hub | USB-C hub *(optional)* | ₹2,799 | for extra peripherals |
| **total** | | **~₹16,277 (~$195)** | |

### the lighter build

| part | model | price (INR) |
|---|---|---|
| board | Arduino UNO Q 2GB | ₹4,648 |
| ears | ReSpeaker Lite, 2-mic | ₹2,637 |
| voice | USB 2.0 speaker | ₹600 |
| power | 5V/3A USB-C | ₹580 |
| **total** | | **~₹8,465** |

### specification

| | |
|---|---|
| processor | Qualcomm QRB2210, quad-core, 2.0 GHz |
| memory | 4GB LPDDR4 + 32GB eMMC |
| hearing | 4-mic array, 360°, 5 m |
| connectivity | Wi-Fi 5 + Bluetooth 5.1 |
| mind | any provider, your choice |
| security | voiceprint verification |
| power | USB-C, 5V/3A |

### three decisions, explained

● **the microphone was never compromised on.** everything from a basic USB mic to the full far-field array was considered. the array won, because "hands-free" that only works up close isn't hands-free at all.

● **for prototyping, a Bluetooth speaker will do.** a JBL Go 3 stands in until a compact wired speaker is chosen for the final body.

● **the enclosure borrows a philosophy, not a shape** — the compactness of a cube object like the Valve Steam Machine. small enough to disappear onto a shelf. not a centerpiece. a fixture.

---

## 07 — software

| layer | technology | purpose |
|---|---|---|
| wake word | Picovoice Porcupine | "hey pico" detection |
| speaker verification | Picovoice Eagle | who is speaking |
| speech-to-text | Vosk | offline transcription |
| voice activity detection | Silero VAD | smart interrupt |
| text-to-speech | Piper TTS | offline, natural |
| the mind | universal AI client | any provider, any model |
| web search | DuckDuckGo / Tavily | live information |
| streaming | WebSockets | real-time audio/data |
| web app | React + Flask | dashboard, settings, remote |

Bring your own key for any provider. Pico does not care whose mind you plug in — only that one is plugged in.

---

## 08 — quick start

**1 — the body**
```
plug the mic array into a USB port
connect the speaker
connect power via USB-C
power on the UNO Q
```

**2 — the software**
```bash
git clone https://github.com/yourusername/pico.git
cd pico

./scripts/setup.sh
pip install -r requirements.txt
python scripts/configure.py
```

**3 — the mind**
```bash
# via the web app
https://pico.local:5000

# or via CLI
python scripts/configure.py --provider deepseek --api-key YOUR_KEY
```

**4 — wake it**
```bash
python main.py
```

**5 — ask it something**
```
"hey pico, what's the weather today?"
→ soft chime — "searching..."

"hey pico, think... write a poem about AI"
→ ambient tone — "thinking..."

"hey pico, search and think... future of education"
→ "searching and synthesizing..."
```


---

## 09 — the web app

The object stays quiet. The app is where you tune it.

| feature | what it does |
|---|---|
| dashboard | device status, usage |
| remote mode | your phone becomes the mic/speaker, over WebRTC |
| settings | wake word, voice, personality |
| chat history | the full log, always visible to you |
| token usage | live cost, per query |
| budget limits | a daily or monthly cap, set once |
| service connections | Spotify, YouTube, calendar |
| custom AI | any provider, your own key |

Onboarding is entirely voice-guided. Each device carries its own private key, paired to its owner over shared Wi-Fi during setup — a key that cannot be copied, only issued once.

---

## 10 — who asks

| age | what pico is for them |
|---|---|
| 8–17 | homework, curiosity, a patient answer to "why" |
| 18–27 | daily assistant, creative partner |
| 28–43 | productivity, home control, saved time |
| 44–59 | information, reminders, news |
| 60+ | news, weather, a voice in the room |

**the people it was built for:** the student up late trying to understand something. the professional who needs an answer without a screen between them and their hands. the elder for whom a phone interface is a wall, not a door. the child who asks "why" a hundred times and deserves a hundred patient answers. the creator who thinks out loud. the citizen who wants to know what's happening.

**what it isn't:** a locked commercial gadget with an agenda. it is a companion for the curious mind, nothing more, nothing less.

---

## 11 — what it costs

full build: **~₹16,277 (~$195)**, once.
lighter build: **~₹8,465**, once.

That's it for the object. What follows is what it costs to *think*.

---

## 12 — what it costs to run

*assuming ~50 questions a day*

| mind | monthly (INR) |
|---|---|
| DeepSeek V4-Flash | ₹60 – ₹120 |
| DeepSeek V4-Pro | ₹180 – ₹360 |
| OpenAI GPT-4o Mini | ₹150 – ₹300 |
| Ollama, local | ₹0 |

Add Spotify if you want it, ~₹119/month. Total monthly cost: **₹60–₹480**, well under the cost of stacking subscriptions on a phone that's already doing seventeen other jobs.

---

## 13 — speed

| step | time |
|---|---|
| wake word | < 50 ms |
| mic processing | 10–50 ms |
| speech-to-text | 200–300 ms |
| first token from the mind | ~1.4 s |
| text-to-speech, 75 words | 1–3 s |
| **end-to-end, simple question** | **~2.5–4.5 s** |
| **end-to-end, complex question** | **~4–8 s** |

Fast enough to feel like a conversation, not a query.

---

## 14 — what's next

| phase | what arrives | when |
|---|---|---|
| 1.0 | core voice pipeline, first mind, web app | Q3 2026 |
| 1.1 | multi-user, Spotify, YouTube | Q4 2026 |
| 1.2 | local models, smart home control | Q1 2027 |
| 2.0 | vision, pico-to-pico, mobile app | Q2 2027 |
| 2.1 | more languages, enterprise | Q3 2027 |

Longer-term ideas explored: a proactive mode that offers a morning briefing unprompted; long-term memory across weeks, not just a session; and — the furthest idea — pico-to-pico, two objects, two owners, quietly connected.

---

## 15 — the manifesto

> in a world of screens, pico is your voice.
> in a world of noise, pico is your answer.
>
> for the student staying up late, trying to understand.
> for the professional who needs an answer, hands-free.
> for the elder who finds screens a wall, not a door.
> for the child who asks "why" a hundred times.
> for the creator with a mind full of ideas.
> for the citizen who wants to stay informed.
>
> pico is for everyone who has ever wondered.
> for everyone who has ever asked.
> for those who question. for those who ask.
>
> **just ask. pico will answer.** ●

---

## 16 — how it came to be

Pico started as a solo build — one creator, one Arduino UNO Q, and a question: what does a $150–200 board become if you strip away everything except the ability to hear and answer. It grew from a basic "hello world" voice loop into a full pipeline: wake word, voiceprint, routed reasoning, a companion app.

It was also shaped as an entry for an Arduino design competition, filed under **Smart Home & Consumer AI** — the category it fits with the least friction:

> *"a hands-free, privacy-conscious voice assistant, built on Arduino UNO Q. a far-field 4-mic array hears the room. speech becomes text, text meets a mind of your choosing, the answer comes back spoken, natural. ask a question, search the web, control a light, play a song — all with 'hey pico.'"*

Launch markets considered, in order: **India, the United States, the United Kingdom, Canada** — India first, on the strength of its fast-growing, voice-first market.

---

## 17 — license

Pico is a personal prototype and competition object. Not open, not yet. This document is the design record — the *why*, not a contribution guide.

When it does open, the first doors will be: new mind-adapters, new voices, new languages, a better app.

---

*for those who ask. for those who question.* ●
