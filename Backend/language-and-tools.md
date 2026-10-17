## Language and tools

- **Language: Python** – Pipecat, LiveKit Agents and AVA are all Python, and most AI/speech libraries are Python-first, and probably matches the team's skills.
- **Voice pipeline: Pipecat** – manages the conversation flow (speech-to-text → LLM → text-to-speech), interruptions and streaming.
- **Backend server: FastAPI** – receives call audio from Asterisk over WebSocket (Pipecat's `pipecat-asterisk` serializer is designed for its FastAPI WebSocket transport) and provides endpoints for the call screen (WP6), e.g.
 `/health`(is the backend still running?), `/calls`(the list of active calls), `/calls/{call_id}`(the converstation for one call).
- **Why FastAPI rather than something else**
*it’s Python, the same as Pipecat*<br>
*it’s built for async work, meaning many things at once, like several calls together*<br>
*it supports WebSockets, which are needed for live audio
it’s very popular and well documented*<br>
*Pipecat already supports it directly*
- **Telephony: Asterisk** – connected through the Asterisk WebSocket channel (`pipecat-asterisk`); AudioSocket / ExternalMedia remain options if WP4 prefers them.
- **Python version: 3.12** – required by `pipecat-asterisk`.