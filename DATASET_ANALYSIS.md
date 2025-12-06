# Task 1: Dataset Analysis

## Datasets I analyzed:
- LJSpeech: 24hr single female, clean English
- VCTK: 109 speakers, UK accents  
- LibriTTS: 585hr audiobooks
- Hi-Fi: 292hr studio quality
- Common Voice: Multilingual crowdsourced

Clean data = clear voice. Noisy data = muffled voice.

Datasets
LJSpeech:
Single female (US English), 24 hours clean studio audio — best for clear single-speaker TTS.

VCTK:
109 UK English speakers, 44 hours — good for accent and multi-speaker TTS.

LibriTTS:
2,456 speakers, 585 hours — large-scale, mixed quality, ideal for robust models.

Hi-Fi Multi-Speaker:
10 pro speakers, 292 hours — premium quality with emotional variation.

HUI German Corpus:
German voices with perfect alignment — for German TTS training.

Common Voice:
9,000+ hours, 60+ languages — useful for multilingual and low-resource TTS.

Voice Quality Factors
Clarity:
High SNR (>20dB) and 22kHz audio = clear speech.

Naturalness:
Prosody (rhythm, pauses) affects how human-like speech sounds.

Accent:
Train with region-matched datasets (US/UK English, etc.).

Pitch & Timbre:
Voice tone and quality come from speaker’s F0 range (male: 100–180Hz, female: 180–250Hz).

Emotion:
Expressive datasets improve emotional tone variety.

Dataset Selection Tips
Match language, accent, and speaker style to your TTS goal.

Use expressive data for emotional voices, neutral for assistants.

Prefer studio-quality audio (>20dB SNR, 22kHz+).

Use single-speaker for clarity or multi-speaker for diversity.

Collect 10–25+ hours for good results, 100+ hours for strong multi-speaker systems.

Data Preparation Steps
Remove noisy/corrupt files.

Resample (16–22kHz), normalize loudness (-20dBFS).

Trim silence, clean text, and convert numbers/dates.

Align text–audio using Montreal Forced Aligner.

Segment into 5–15 sec clips.

Extract mel-spectrograms (80 mel bins).

Split: 90% train, 5% validation, 5% test.

Key Takeaways
Dataset = Voice Quality. Good data → natural TTS.

LJSpeech: high-quality single voice.

VCTK: diverse accent modeling.

LibriTTS: robust, large training base.

Preprocessing ensures consistent and clean results.


