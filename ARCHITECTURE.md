# Piper TTS Personalization Architecture

## System Components (5 Modules)

| Module | Input | Output | Tech Stack |
|--------|-------|--------|------------|
| **1. Audio Preprocessor** | WAV/MP3 | 22kHz PCM | librosa |
| **2. Feature Extractor** | Audio | 12 metrics | librosa.feature |
| **3. Pattern Learner** | Features | Statistics | numpy |
| **4. Profile Manager** | Stats | JSON | Python json |
| **5. Synthesis Adapter** | Text+Profile | WAV | Piper TTS |

## Integration Pipeline
Phase 1: Training (2.8s total)
User Audio ──► Preprocess ──► Extract ──► Learn ──► JSON Profile

Phase 2: Inference (0.7s)
Text + Emotion ──► Load Profile ──► Piper TTS ──► Personalized WAV


## Performance Data (From task2_logs.txt)
Audio Input: 124.3 seconds

Processing Time: 2.84 seconds

Features Extracted: 12 metrics

Profile Size: 2.5KB JSON

Synthesis Latency: 710ms

Memory Peak: 150MB


## Runtime Flow
User uploads 1-5min voice recording

Engine extracts: WPM=132, pauses=52, pitch=1487Hz, emotion=neutral

Creates personalized_voice_profile.json

Runtime: Load JSON → Adjust Piper params → Generate speech


## Technical Specifications
Voice Model: en_US-amy-medium.onnx (15MB)
Sample Rate: 22,050 Hz
Format: WAV mono
Piper Version: v1.2.0
Environment: Google Colab CPU
Dependencies: librosa, numpy


**See DIAGRAMS.md for visual architecture.**
