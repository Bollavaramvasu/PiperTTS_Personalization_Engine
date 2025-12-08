# Task 1: Dataset Analysis

## Datasets I analyzed:
- LJSpeech: 24hr single female, clean English
- VCTK: 109 speakers, UK accents  
- LibriTTS: 585hr audiobooks
- Hi-Fi: 292hr studio quality
- Common Voice: Multilingual crowdsourced

Clean data = clear voice. Noisy data = muffled voice.

#  TTS Dataset Analysis 

##  Dataset Overview

| Dataset Name | Description | Use Case |
|---------------|--------------|-----------|
| **LJSpeech** | Single female (US English), 24h clean studio audio | Clear single-speaker TTS |
| **VCTK** | 109 UK English speakers, 44h total | Accent & multi-speaker TTS |
| **LibriTTS** | 2,456 speakers, 585h diverse audio | Robust large-scale models |
| **Hi-Fi Multi-Speaker** | 10 pro speakers, 292h | Premium quality, emotional TTS |
| **HUI German Corpus** | Multi-speaker German dataset with aligned text | German TTS training |
| **Common Voice** | 9,000+ hours across 60+ languages | Multilingual / low-resource TTS |

---

##  Voice Quality Factors

- **Clarity:**  
  High SNR (>20 dB) and sample rate (22 kHz+) → crisp, clear audio.

- **Naturalness:**  
  Prosody (rhythm, pauses, intonation) = human-like speech.

- **Accent:**  
  Output accent depends on dataset source (US, UK, etc.).

- **Pitch & Timbre:**  
  - Female range: 180–250 Hz  
  - Male range: 100–180 Hz  
  Voice tone comes from speakers’ frequency and vocal traits.

- **Emotion:**  
  Expressive datasets = emotional, realistic voices.

---

##  Dataset Selection Tips

- Match **language**, **accent**, & **speaker style** to your target voice.  
- Use **expressive** data for emotional TTS; **neutral** for assistants.  
- Prefer **high-quality studio recordings** (>20 dB SNR).  
- **Single-speaker** → consistent quality.  
- **Multi-speaker** → diversity and accent coverage.  
- Collect **10–25 h+** for good results; **100 h+** for multi-speaker strength.

---

##  Data Preparation Pipeline

1. Clean dataset — remove noise & misalignments.  
2. Resample audio to 16 kHz / 22.05 kHz.  
3. Normalize loudness to -20 dBFS & trim silence below -40 dB.  
4. Text normalization (expand numbers, abbreviations, etc.).  
5. Forced alignment with **Montreal Forced Aligner**.  
6. Segment audio into 5–15 sec clips.  
7. Extract **Mel-spectrograms** (80 mel bins, 25 ms window, 10 ms hop).  
8. Split:
   - 90% → Train  
   - 5% → Validation  
   - 5% → Test  

---

##  Key Takeaways

- Good **data = good TTS quality**.  
- **LJSpeech** → natural single voice.  
- **VCTK** → diverse accent modeling.  
- **LibriTTS** → large, strong baseline dataset.  
- **Clean preprocessing** ensures consistent speech synthesis.

---

## Mermaid Diagram (rectangular / large layout)

Below is a redesigned Mermaid diagram that lays out the content in a large rectangular shape (top = datasets, right = pipeline steps stacked, bottom = model & use cases, left = voice quality factors). This creates a square/rectangle flow that is visually larger and avoids a long single line. Paste this into GitHub (file view) or a Mermaid previewer (VSCode/mermaid.live).

```mermaid
flowchart LR
  %% Top row: datasets (left-to-right)
  subgraph TOP [Datasets]
    direction LR
    LJS["LJSpeech\n(24h, single speaker)"]
    VCTK["VCTK\n(109 speakers)"]
    Libri["LibriTTS\n(585h, diverse)"]
    HiFi["Hi‑Fi Multi‑Speaker\n(292h, studio)"]
    CV["Common Voice\n(Multilingual, crowd)"]
  end

  %% Right column: preparation pipeline (top-to-bottom)
  subgraph RIGHT [Data Preparation Pipeline]
    direction TB
    P1["1. Clean\n(remove noise & misalignments)"]
    P2["2. Resample\n(16kHz / 22.05kHz)"]
    P3["3. Loudness normalize\n(-20 dBFS) & trim silence"]
    P4["4. Text normalization\n(expand numbers/abbr)"]
    P5["5. Forced alignment\n(Montreal Forced Aligner)"]
    P6["6. Segment\n(5–15s clips)"]
    P7["7. Extract Mel-spectrograms\n(80 bins, 25ms/10ms)"]
    P8["8. Split\n(Train 90% / Val 5% / Test 5%)"]
  end

  %% Bottom row: models and use cases (left-to-right)
  subgraph BOTTOM [Model Training & Use Cases]
    direction LR
    MTrain["Train Models\n(TTS, encoders, VAE)"]
    MEval["Evaluate\n(metrics & QA)"]
    USingle["Single-speaker TTS\n(voice cloning)"]
    UMulti["Multi-speaker\n& Accent Transfer"]
    UExpress["Expressive / Emotional\nTTS"]
  end

  %% Left column: voice quality factors (top-to-bottom)
  subgraph LEFT [Voice Quality Factors]
    direction TB
    F1["Clarity\n(high SNR, sr>=22kHz)"]
    F2["Naturalness\n(prosody, intonation)"]
    F3["Accent\n(dataset source)"]
    F4["Pitch & Timbre\n(male/female ranges)"]
    F5["Emotion\n(expressive recordings)"]
  end

  %% Rectangle connections (flow around a rectangle)
  TOP -->|feeds into| P1
  P8 -->|processed data ->| MTrain
  MTrain --> MEval
  MEval --> USingle
  MEval --> UMulti
  MEval --> UExpress
  USingle -->|informs| TOP
  UMulti -->|informs| TOP
  UExpress -->|informs| TOP

  %% Close rectangle by linking left factors into top datasets and into pipeline
  LEFT -->|influence| TOP
  LEFT -->|guide prep| P2

  %% Make visual loop to emphasize rectangular layout
  TOP -.-> BOTTOM
  BOTTOM -.-> LEFT

  %% Styling for a larger, bold look
  classDef topStyle fill:#e8f4ff,stroke:#0366d6,stroke-width:2px,rx:6,ry:6;
  classDef rightStyle fill:#fff8e6,stroke:#d97706,stroke-width:1.5px,rx:6,ry:6;
  classDef bottomStyle fill:#ecfff2,stroke:#059669,stroke-width:1.5px,rx:6,ry:6;
  classDef leftStyle fill:#fff0f6,stroke:#be185d,stroke-width:1.5px,rx:6,ry:6;
  class TOP topStyle;
  class RIGHT rightStyle;
  class BOTTOM bottomStyle;
  class LEFT leftStyle;

  %% Make nodes larger by grouping and multi-line labels (increases rendered box size)
  class LJS,VCTK,Libri,HiFi,CV topStyle;
  class P1,P2,P3,P4,P5,P6,P7,P8 rightStyle;
  class MTrain,MEval,USingle,UMulti,UExpress bottomStyle;
  class F1,F2,F3,F4,F5 leftStyle;
```

Notes:
- This layout intentionally places nodes on four sides to form a rectangular / square visual. Multi-line labels enlarge nodes and the overall diagram.
- If you want the rectangle to be even bigger, we can add invisible spacer nodes to increase spacing, or split pipeline steps into grouped subgraphs (I can do that if desired).
- If you want exact styling to match architecture.md, paste that mermaid block or allow me to fetch it and I'll match fonts/colors precisely.

If you want, I can:
- Add spacer nodes to make the rectangle physically larger on render.
- Produce a second diagram that isolates Voice Quality Factors in a separate large panel.
