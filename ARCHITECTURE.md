# Piper TTS Personalization Engine Architecture

## System Overview
The system extends Piper TTS with user-specific voice learning capabilities through a 5-stage pipeline.

## High-Level Architecture

┌─────────────────────────────────────────────────────────────┐
│ PERSONALIZATION ENGINE │
├─────────────────┬─────────────────┬─────────────────────────┤
│ 1. Preprocessor │ 2. Extractor │ 3. Learner │
│ WAV → 22kHz │ Pauses/WPM │ Statistics │
│ librosa │ librosa.feature │ numpy │
└─────────────────┼─────────────────┼─────────────────────────┤
│ │ │
▼ ▼ ▼
┌─────────────────┴─────────────────┴─────────────────────────┐
│ VOICE PROFILE (JSON) │
│ duration: 124s, wpm: 132, pitch: 1487Hz, emotion: neutral │
└─────────────────────────────────────────────────────────────┘
│
▼
┌─────────────────────────────────────────────────────────────┐
│ SYNTHESIS ADAPTER │
│ Piper TTS + Profile Parameters → Personalized WAV │
└─────────────────────────────────────────────────────────────┘
## Component Specifications

### 1. Audio Preprocessor
**Input:** User audio (WAV/MP3, 1-5min)  
**Output:** 22kHz mono PCM  
**Parameters:**  
- Sample rate: 22050 Hz  
- Normalization: RMS -20dBFS  
- Silence threshold: -40dB  

### 2. Feature Extractor
**Features Extracted:**
| Feature | Method | Purpose |
|---------|--------|---------|
| Speaking Rate | Silence ratio | WPM estimation |
| Pause Duration | Energy frames | Rhythm modeling |
| Spectral Centroid | librosa.feature | Pitch proxy |
| RMS Energy | librosa.feature.rms | Emotion indicator |

### 3. Pattern Learner
**Statistical Modeling:**
- Mean/Std/Percentiles for all features
- Distribution analysis (pauses, pitch)
- Emotion classification (3 classes)

## Integration with Piper TTS

Piper TTS Pipeline:
Text ──► Acoustic Model (.onnx) ──► Waveform (22kHz)

Extended Pipeline:
Text ──► [Profile Loader] ──► Acoustic Model ──► [Adapter] ──► Waveform
JSON Speed/Pause adjust
## Performance Characteristics

| Metric | Value | Notes |
|--------|-------|-------|
| Processing Time | 2.8s | CPU (Colab) |
| Memory Usage | 150MB | Peak during feature extraction |
| Profile Size | 2.5KB | JSON |
| Inference Latency | 700ms | Real-time capable |
| Audio Requirement | ≥60s | Statistical reliability |

## Runtime Environment
- Runtime: Google Colab (CPU)
- Dependencies: librosa, numpy, Piper v1.2.0
- Voice Model: en_US-amy-medium.onnx (15MB)
- Output Format: WAV 22kHz mono
