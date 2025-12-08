# PiperTTS Personalization Engine Architecture

flowchart TD
A[User Input
Text + Voice Preference] --> B[API Gateway
FastAPI/Flask]
B --> C[Text Preprocessing
Normalization, SSML]
C --> D[Voice Selector
Model Picker
User Profile]
D --> E[Piper TTS Core
ONNX Runtime
Voice Models]
E --> F[Audio Post-Processing
WAV/MP3 Conversion
Normalization]
F --> G[Output Delivery
File Storage
Streaming API]

style A fill:#e1f5fe
style G fill:#c8e6c9

## Architecture Components

**User Input Layer**
- Receives text input and voice preferences via REST API or CLI [web:20]
- Handles authentication and rate limiting

**API Gateway**
- FastAPI endpoints for `/synthesize`, `/voices`, `/profile` [web:4]
- Request validation and JSON parsing

**Text Preprocessing**
- Normalizes text (punctuation, casing, phonemes) [web:1]
- Supports SSML-like tags for prosody control

**Voice Selector**
- Loads user-specific voice models from config/profile [web:7]
- Selects language, speaker, and quality settings

**Piper TTS Core**
- Executes Piper ONNX models for neural TTS synthesis [web:20]
- Manages inference sessions for low-latency generation

**Audio Post-Processing**
- Converts raw audio to WAV/MP3 formats [web:2]
- Applies volume normalization and silence trimming

**Output Delivery**
- Streams audio bytes or saves to local/cloud storage [web:10]
- Returns download URLs or base64 audio data
