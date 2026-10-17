# WP5 – Framework comparison

## Pipecat

- **Type:** Framework
- **Link:** https://github.com/pipecat-ai/pipecat
- **Licence:** BSD 2-Clause (free, commercial use OK, keep the copyright notice)
- **Language + Python:** Python, min 3.11, recommended 3.12+
- **Activity:** 16.5k stars, commits within the last day, very active
- **Documentation:** Clear, with many examples (docs.pipecat.ai)
- **Asterisk connection:** Not built in; community package `pipecat-asterisk` (Asterisk WebSocket channel, tested with Python 3.12+)
- **Local / free models:** Yes: Whisper, Moonshine (STT); Ollama (LLM); Piper, Kokoro, XTTS (TTS); Silero VAD
- **Runs on a laptop?** Framework: yes. Local models need more memory; small models recommended
- **Main strengths:** Very active, large choice of services, can run fully local, works with FastAPI
- **Main risks:** Asterisk support is community-made, not official; needs Python 3.12 for it
- **Call path:** Asterisk → (WebSocket) → Pipecat agent

## LiveKit Agents

- **Type:** Framework
- **Link:** https://github.com/livekit/agents
- **Licence:** Apache 2.0 (free, commercial use OK); turn-detector model has a separate LiveKit Model License
- **Language + Python:** Python (also Node.js), 3.10+
- **Activity:** 14.8k stars, daily commits, very active
- **Documentation:** Good, but examples mostly assume LiveKit Cloud
- **Asterisk connection:** Not documented. Uses SIP, so possible in principle, but needs LiveKit server + LiveKit SIP service in between. Docs only cover paid providers (Twilio, Telnyx, Plivo)
- **Local / free models:** Not clearly documented; examples use cloud services
- **Runs on a laptop?** Agent: yes. Real calls also need a LiveKit server + SIP service (self-hosted or LiveKit Cloud)
- **Main strengths:** Very active, strong company behind it, good turn detection, can be fully self-hosted
- **Main risks:** More infrastructure; no Asterisk guide; cloud-focused examples; local models not clear
- **Call path:** Asterisk → (SIP) → LiveKit SIP service → LiveKit server → LiveKit agent

## AVA (Asterisk AI Voice Agent)

- **Type:**
- **Link:** https://github.com/hkjarral/AVA-AI-Voice-Agent-for-Asterisk
- **Licence:**
- **Language + Python:**
- **Activity:**
- **Documentation:**
- **Asterisk connection:**
- **Local / free models:**
- **Runs on a laptop?**
- **Main strengths:**
- **Main risks:**
- **Call path:**