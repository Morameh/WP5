## Call control and separate calls

### Action control – "the LLM suggests, the backend decides"
Actions (transfer, hang-up) are requested by the LLM through tool calling (e.g. `transfer_call("billing")`), but executed only after the backend validates them:

- **Allowed list:** only approved departments (e.g. sales, billing, support, reception) can be transfer targets.
- **No numbers in the LLM:** the LLM only names a department; the backend maps it to the real extension from a config file. This prevents invented numbers and prompt-injection attacks.
- **Confirmation:** the agent confirms with the caller before transferring.
- **Limits:** a maximum number of transfers per call to prevent loops.
- **Failed transfers:** if the line is busy or unanswered, the agent returns and offers an alternative (e.g. take a message).
- **Safe default:** when unsure, transfer to reception (a human).
- **Hang-up:** only after a goodbye or a long silence.
- **Logging:** every action is logged with call ID, time and result, and shown on the call screen (WP6).

### Separate calls – "one call, one session"
- Each call has a unique **call ID** (from the Asterisk channel).
- Each call has its own **session** (conversation history, state, transfer count) and its own **Pipecat pipeline**.
- Calls share only **read-only** resources (e.g. the Mobex knowledge base); no caller data is shared.
- When a call ends, its session is **deleted** and connections closed.
- Errors in one call do not affect others.
- A **maximum number of concurrent calls** is set based on hardware; extra calls go to a human or queue.
- All logs and events are tagged with the call ID.

### Feasibility (checked against documentation)

| Feature | Feasible? | Notes |
|---|---|---|
| Session and pipeline per call | Yes – easy | Standard in Pipecat/FastAPI |
| Allowed list and logging | Yes – easy | Our own backend code |
| Tool calling for transfers | Yes – medium | Pipecat supports function calling and the handler runs in our own code, so we can validate requests; Pipecat does not validate arguments itself ([Pipecat docs](https://docs.pipecat.ai/guides/learn/function-calling)). Small local LLMs may be less reliable at tool calling – to be tested with WP2 |
| Transfer via ARI | Yes – medium/hard | The ARI application performs transfers itself (Asterisk does not handle them automatically) ([Asterisk docs](https://docs.asterisk.org/Configuration/Interfaces/Asterisk-REST-Interface-ARI/Introduction-to-ARI-Transfer-Handling/)). Must be built with WP4 alongside the audio connection |
| Return to agent after failed transfer | Possible – hardest | Prototype: offer to take a message instead |
| Concurrent calls on a laptop | Limited | Expect 1–3 calls with local models; set a maximum |