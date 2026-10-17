# WP5 – Requirements

## 1. What the system must do (must-have)
- Answer inbound phone calls automatically
- Understand what the caller is asking in natural speech
- Answer common questions using only Mobex's real information
- Transfer the caller to the right person or department
- Only transfer to approved phone numbers
- Say clearly when it does not have the information
- Stop talking when the caller interrupts
- Offer another option if a transfer fails (e.g. busy or no answer)
- Keep each call separate (no mixing between callers)(giving ID to each call)
- Show the call on a screen: caller's words, answers and transfers
- Reply fast enough to feel like a normal conversation

## 2. Nice to have (optional)
- Outbound calls (reminders, confirmations) – a possible later phase in the proposal

## 3. Constraints
- Cost: free tools and free tiers only (the plan mentions "free limits" and "free host"). No paid services assumed.
- Hardware: must run on team members' laptops or a free cloud host. No dedicated GPU server assumed.
- Time: Research in October, build from November, demo in January.
- Privacy: callers' voices and words are personal data. Prefer tools that can run locally or keep data inside the UK/EU, and avoid storing recordings unless needed.
## 4. Unknowns / assumptions
- Unknown: how call audio leaves Asterisk (WP4) – ExternalMedia, AudioSocket or WebSocket channel.
  Assumption for now: the backend should support at least one of these; the final choice is agreed with WP4.
- Unknown: LLM is local or API (WP2).
  Assumption for now: the backend calls the LLM through one standard interface, so either option can be plugged in.
- Unknown: whether speech-to-text and text-to-speech support streaming (WP3).
  Assumption for now: streaming is supported; without it, reply delay will be noticeably longer.
- Unknown: where the system runs (WP1) – laptop, free cloud host or Docker.
  Assumption for now: everything runs on one laptop for the prototype.
- Unknown: when Mobex provides real information (FAQs, departments, phone numbers).
  Assumption for now: the team uses sample data until the real data arrives.
## Call flow (architecture)
Caller speaks → speech-to-text → understand intent → find facts / decide routing → write reply (text) → text-to-speech → caller hears
