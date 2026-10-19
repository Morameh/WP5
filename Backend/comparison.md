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
- **Who is behind it:** Daily (daily.co), with the open-source community
- **Companies using it:** NVIDIA, Anthropic, AWS, ServiceNow, Cresta, Mercor (listed on [pipecat.ai](https://www.pipecat.ai/); how each uses it is not stated)
- **Where it is used:** customer support (24/7, routing complex issues to humans), outbound calls (e.g. appointment scheduling), virtual assistants, financial services (InDebted prototype with AWS)
- **How it is used:** as the orchestration layer that connects VAD, STT, LLM and TTS. AWS's example: Silero VAD → Amazon Transcribe → Amazon Nova (Bedrock) → Amazon Polly – the same pipeline shape as our design ([AWS blog, Part 1](https://aihub.hkuspace.hku.hk/?p=3663)). NVIDIA also published a Pipecat blueprint (now deprecated).
- **Deployment:** self-hosted or via Pipecat Cloud (managed service by Daily); supports WebRTC, SIP and phone lines
- **News / challenges:** Oct 2026 – released PhoneLLM Mini, its own fast model for phone agents, on Cloudflare Workers AI ([source](https://developers.cloudflare.com/changelog/post/2026-10-15-phonellm-mini-workers-ai/))

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
- **Who is behind it:** LiveKit Inc. (founded 2021)
- **Companies using it:** OpenAI (powers ChatGPT voice mode); also xAI, Salesforce, Tesla, 911 emergency operators, mental-health providers ([TechCrunch](https://techcrunch.com/2026/01/22/voice-ai-engine-and-openai-partner-livekit-hits-1b-valuation/))
- **Where it is used:** consumer apps (ChatGPT voice mode), healthcare, emergency services (911 operators)
- **How it is used:** example – Assort Health: AI answers patients' phone calls via SIP connected to clinics' phone systems; books appointments, handles refills and payments, and routes callers to the right department. 20M+ interactions; AI handles 90% of inbound calls, 10% handed to staff ([LiveKit case study](https://livekit.com/blog/how-assort-health-uses-livekit-to-scale-patient-communication))
- **Deployment:** LiveKit Cloud (managed) or self-hosted
- **News / challenges:** Jan 2026 – raised $100M at a $1B valuation ([Bloomberg](https://www.bloomberg.com/news/articles/2026-01-22/livekit-seller-of-voice-tools-to-openai-raises-100-million))

## AVA (Asterisk AI Voice Agent)

- **Type:** Complete project (ready-made voice agent built for Asterisk)
- **Link:** https://github.com/hkjarral/AVA-AI-Voice-Agent-for-Asterisk
- **Licence:** MIT (free, commercial use OK, keep the copyright notice)
- **Language + Python:** Python (based on repository files)
- **Activity:** 1.2k stars, 280 forks, 13 open issues; regular releases (v7.6.4). Active, but smaller community
- **Documentation:** Detailed guides (local setup, WebSocket, outbound calling)
- **Asterisk connection:** Built for Asterisk (18+, ARI required). Supports AudioSocket, ExternalMedia RTP and WebSocket
- **Local / free models:** Yes: fully on-premises option with no cloud APIs; CPU-only setup possible
- **Runs on a laptop?** Needs Linux + Docker Compose; min 2 CPU / 4 GB RAM (more for local models). On Windows via WSL – needs testing
- **Main strengths:** Made for Asterisk; supports all three audio methods; fully local CPU-only option; most complete out of the box
- **Main risks:** Smaller community; harder to customise a full app than to build with a framework; some features still alpha; needs Docker
- **Call path:** Asterisk → (AudioSocket / RTP / WebSocket) → AVA engine
- **Who is behind it:** independent developer (GitHub: hkjarral) with community contributors
- **Companies using it:** none named publicly; aimed at Asterisk/FreePBX operators, especially regulated sectors (healthcare, finance, legal, government) that need audio to stay on-premises
- **Where it is used:** businesses running Asterisk/FreePBX, especially those needing audio to stay on-premises
- **How it is used:** plugs into an existing phone system without changing hardware or numbers; transfers, voicemail, call summaries. No public case studies found – not yet proven at large scale ([PBX Science](https://pbxscience.com/ava-the-open-source-ai-voice-agent-that-brings-real-intelligence-to-your-phone-system/))
- **Deployment:** self-hosted only (Docker Compose on Linux)
- **News / challenges:** regular releases (v7.x); outbound dialer still alpha; small contributor pool; local GPU first start can take 15–20 minutes

## Other options considered (not shortlisted)

- **TEN Framework:** active (11.1k stars), but multi-language (C++/Go/Python/TS), cloud-focused quick start, SIP example uses Twilio, no Asterisk guide; licence has extra conditions to check.
- **Vocode:** no public commits since Nov 2024 and the project is asking for community maintainers; hosted service reportedly no longer reachable (source: a competitor's blog, so treat with caution). Not recommended.
- **OpenVoiceOS:** home voice assistant, not designed for business telephony.
- **Other Asterisk AI agent repos:** mostly forks or variants of AVA, covered by the AVA review.

## Recommendation
(my point of view for share)
There is no perfect option. each involves a trade-off.

- **AVA** is a complete project with Asterisk support built in and ready to use, so it is the fastest way to a working phone demo. However, it has a much smaller community (1.2k stars), no public case studies, and a complete application is harder to customise.
- **Pipecat** and **LiveKit Agents** are frameworks: the Asterisk connection has to be added (Pipecat through a community package, LiveKit through extra servers).
- **Pipecat** has the widest documented choice of services, including free local models for every step (Ollama, Whisper, Piper), and the largest community (16.5k stars), daily commits and clear documentation, which suggest it is well maintained.
- **LiveKit** has the strongest real-world evidence for phone agents (e.g. Assort Health in healthcare), but its extra infrastructure and lack of Asterisk documentation make it harder to use within our constraints.

**Main option: Pipecat** – flexible, well supported, fits our free/local constraints, and lets the team build parts in parallel.

**Fallback: AVA** – if the community Asterisk package for Pipecat proves unreliable, AVA already solves the Asterisk connection and can also serve as a reference for how to integrate Asterisk.

**To validate in November:** test `pipecat-asterisk` with our Asterisk setup early.