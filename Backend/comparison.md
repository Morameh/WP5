# WP5 – Framework comparison

| Criterion | Pipecat | LiveKit Agents | AVA |
|---|---|---|---|
| Type | Framework | Framework | |
| Link | github.com/pipecat-ai/pipecat | github.com/livekit/agents | |
| Licence | BSD 2-Clause (free, commercial use OK, keep the copyright notice) | Apache 2.0 (free, commercial use OK); turn-detector model has a separate LiveKit Model License | |
| Language + Python | Python, min 3.11, recommended 3.12+ | Python (also Node.js), 3.10+ | |
| Activity | 16.5k stars, commits within the last day, very active | 14.8k stars, daily commits, very active | |
| Documentation | Clear, with many examples (docs.pipecat.ai) | Good, but examples mostly assume LiveKit Cloud | |
| Asterisk connection | Not built in; community package `pipecat-asterisk` (Asterisk WebSocket channel, tested with Python 3.12+) | Not documented. Uses SIP, so possible in principle, but needs LiveKit server + LiveKit SIP service in between. Docs only cover paid providers (Twilio, Telnyx, Plivo) | |
| Local / free models | Yes: Whisper, Moonshine (STT); Ollama (LLM); Piper, Kokoro, XTTS (TTS); Silero VAD | Not clearly documented; examples use cloud services | |
| Runs on a laptop? | Framework: yes. Local models need more memory; small models recommended | Agent: yes. Real calls also need a LiveKit server + SIP service (self-hosted or LiveKit Cloud) | |
| Main strengths | Very active, large choice of services, can run fully local, works with FastAPI | Very active, strong company behind it, good turn detection, can be fully self-hosted | |
| Main risks | Asterisk support is community-made, not official; needs Python 3.12 for it | More infrastructure; no Asterisk guide; cloud-focused examples; local models not clear | |

## How a call reaches the agent

```
Pipecat: Asterisk → (WebSocket) → Pipecat agent
LiveKit: Asterisk → (SIP) → LiveKit SIP service → LiveKit server → LiveKit agent
```