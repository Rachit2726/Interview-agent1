Key Challenges

1. Real-time audio pipeline (Browser → FastAPI → Whisper → LLM → Edge-TTS)

Coordinating recording, silence detection, transcription, LLM response, and TTS playback required a pipelined architecture with asynchronous control. Managing delays, buffering, and browser audio constraints was non-trivial.


2. Silence Detection with Natural Behavior

I created a dynamic silence detection algorithm using:

Real-time audio RMS monitoring

Ambient noise calibration (0.7s sampling)

Adaptive silence thresholding

Fail-safe max-duration cutoff

This ensured the system stops recording naturally, just like a real interviewer would pause.


3. High-quality conversational flow

To ensure realistic interview behavior:

The agent follows a finite-state machine (FSM)

LLM prompts generate structured interview questions

Follow-up questions target missing details

Final feedback evaluates communication, depth, conciseness, and problem-solving

This reduced hallucinations and made the agent sound intentional and human-like.


4. Modern two-pane UI (MS Teams Style)

I built a responsive UI with:

Left pane: user camera

Right pane: interviewer avatar

Speaking animations (Snico waveform)

Automatic record & play cycles

"End interview" control

The design avoids text clutter and focuses on voice interaction.

GitHub Repo Structure

Interview-agent/
│
├── backend/
│   ├── main.py          # FastAPI server
│   ├── agent.py         # State machine logic
│   ├── tts_engine.py    # Edge-TTS synthesis
│   ├── stt_engine.py    # Whisper transcription
│   ├── llm_engine.py    # Qwen LLM inference
│   ├── config.py        
│   └── requirements.txt
│
├── frontend/
│   ├── index.html
│   ├── style.css
│   ├── script.js        # Auto-record + silence detection
│   └── assets/
│       └── interviewer.webp
│
└── README.md
