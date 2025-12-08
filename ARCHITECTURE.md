# Piper TTS Personalization — Architecture

This diagram shows the system components, the two-phase integration pipeline (Training & Inference), runtime flow, and key performance / technical specs.

```mermaid
flowchart LR
  %% Phase 1: Training
  subgraph Phase1["Phase 1: Training (2.8s total)"]
    direction TB
    AU[User Audio<br/>WAV / MP3]
    AP[Audio Preprocessor<br/>22 kHz PCM<br/>librosa]
    FE[Feature Extractor<br/>12 metrics<br/>librosa.feature]
    PL[Pattern Learner<br/>Statistics<br/>numpy]
    PM[Profile Manager<br/>personalized_voice_profile.json<br/>~2.5 KB<br/>python json]
    AU --> AP --> FE --> PL --> PM
  end

  %% Phase 2: Inference
  subgraph Phase2["Phase 2: Inference (0.7s)"]
    direction TB
    TXT[Text + Emotion]
    LOAD[Load Profile<br/>personalized_voice_profile.json]
    SY[ Synthesis Adapter<br/>Piper TTS v1.2.0<br/>en_US-amy-medium.onnx (15MB) ]
    OUT[Generated WAV<br/>Mono, 22,050 Hz]
    TXT --> LOAD --> SY --> OUT
  end

  %% Link between phases
  PM -->|profile.json| LOAD

  %% Runtime flow / user steps
  subgraph Runtime["Runtime Flow (user)"]
    direction LR
    UPL[Upload 1–5 min voice recording]
    EX[Engine extracts: WPM=132, pauses=52, pitch=1487Hz, emotion=neutral]
    CRE[Creates personalized_voice_profile.json]
    UPL --> EX --> CRE
    CRE --> PM
  end

  %% Performance & environment note (visualized as a side note)
  perf[(Performance / Environment
  • Audio Input: 124.3 s
  • Processing Time: 2.84 s
  • Features Extracted: 12 metrics
  • Synthesis Latency: 710 ms
  • Memory Peak: 150 MB
  • Voice Model: en_US-amy-medium.onnx (15 MB)
  • Sample Rate: 22,050 Hz
  • Format: WAV mono
  • Environment: Google Colab CPU
  • Dependencies: librosa, numpy
  )]

  Phase1 --- perf
  Phase2 --- perf
  Runtime --- perf
```
