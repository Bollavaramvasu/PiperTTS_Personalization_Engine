#  Piper TTS Personalization Diagrams

##  Architecture Diagram
See ARCHITECTURE.md

---

##  Data Flow Diagram (Level 0 - Context)

```mermaid
flowchart LR
  U[User<br/>(Audio Input)] -->|2.8s Processing| P[Personalization Engine]
  P --> O[Output<br/>(Personalized Speech)]
  P --> J[JSON Profile<br/>2.5KB Storage]
```

---

##  Component Interaction

```mermaid
flowchart TD
  A[Preprocess<br/>22kHz Mono] --> B[Feature Analysis<br/>Pauses / Energy]
  B --> C[Profile Manager<br/>JSON Export]

  A -.->|Shared Data| D[Piper TTS + Adapter]
  B -.->|Shared Data| D
  C -.->|Profile Import| D
```

---

##  Sequence Flow

```mermaid
sequenceDiagram
  participant User
  participant Engine
  participant Profile
  participant Piper

  User ->> Engine: Upload Audio File
  Engine ->> Profile: Preprocess & Extract Features
  Profile ->> Profile: Store Profile (profile.json)
  User ->> Piper: Text Input ("Hello World")
  Piper ->> Profile: Load Voice Profile
  Piper ->> User: Return Personalized WAV Output
```
