## Language and tools

- **Language: Python** – Pipecat, LiveKit Agents and AVA are all Python, and most AI/speech libraries are Python-first, and probably matches the team's skills.
- **Voice pipeline: Pipecat** – manages the conversation flow (speech-to-text → LLM → text-to-speech), interruptions and streaming.
- **Backend server: FastAPI** – receives call audio from Asterisk over WebSocket (Pipecat's `pipecat-asterisk` serializer is designed for its FastAPI WebSocket transport) and provides endpoints for the call screen (WP6).<br>
**What is FastAPI :** 
FastAPI is an open-source Python framework for building web servers and APIs. An API is the "entry point" of a program: it receives requests from other programs and sends back responses. FastAPI is fast, supports async code (handling many tasks at the same time) and WebSockets (two-way live connections), which are needed for real-time audio.
**Role in this project:** FastAPI is the entry point of the backend. It (1) accepts the live call audio from Asterisk over a WebSocket and passes it to the Pipecat pipeline, and (2) provides endpoints for the call screen (WP6), such as `/health` (is the backend running?), `/calls` (list of active calls) and `/calls/{call_id}` (the conversation of one call).
- **Why FastAPI rather than something else**<br>
*it’s Python, the same as Pipecat*<br>
*it’s built for async work, meaning many things at once, like several calls together*<br>
*it supports WebSockets, which are needed for live audio
it’s very popular and well documented*<br>
*Pipecat already supports it directly*
- **Telephony: Asterisk** – connected through the Asterisk WebSocket channel (`pipecat-asterisk`); AudioSocket / ExternalMedia remain options if WP4 prefers them.
- **Python version: 3.12** – required by `pipecat-asterisk`.