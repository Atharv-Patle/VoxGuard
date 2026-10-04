# 🛡️ VoxGuard — AI Voice Deepfake & Fraud Detection System

> **From trusting a voice → to verifying the voice.**

VoxGuard is an **AI-powered voice fraud detection system** designed to identify whether an audio recording is **genuine human speech or AI-generated / manipulated speech**.

The project addresses the growing threat of **voice cloning, AI-generated voices, impersonation scams, and audio-based social engineering attacks**. By combining deep learning, audio signal processing, and an easy-to-use web interface, VoxGuard provides a practical approach for detecting suspicious voice recordings before they can be used for fraud.

---

## 🚨 Problem Statement

Voice-based fraud is becoming increasingly sophisticated with the rapid development of generative AI and voice-cloning technologies.

Attackers can now generate highly realistic voices that can imitate:

- 👤 Family members
- 🏦 Bank representatives
- 👨‍💼 Company executives
- 📞 Customer-care agents
- 🧑‍⚕️ Professionals
- 🎙️ Public personalities

Traditional fraud detection systems primarily focus on **text, transaction patterns, phone numbers, or URLs** and may fail when the primary attack vector is the **voice itself**.

### Our Solution

**VoxGuard analyzes the acoustic characteristics of an audio recording and predicts whether the voice is authentic or potentially AI-generated/manipulated.**

The system can act as an additional **verification layer** for voice-based communication.

---

# 💡 Our Solution

VoxGuard follows a deep-learning pipeline:

```text
Audio Input
     ↓
Audio Preprocessing
     ↓
Mel-Spectrogram Generation
     ↓
Data Normalization & Masking
     ↓
ResNet18 Feature Extraction
     ↓
Bi-GRU Temporal Analysis
     ↓
Fraud / Genuine Classification
     ↓
Confidence Score
     ↓
User-Friendly Result
```

The combination of **CNN-based spatial feature extraction** and **Bi-GRU-based temporal modeling** enables the system to analyze both the spectral characteristics and temporal patterns present in speech.

---

# 🧠 Key Features

### 🎙️ AI Voice Fraud Detection
Detects suspicious AI-generated or manipulated speech using deep learning.

### 🔬 Mel-Spectrogram Analysis
Converts raw audio into a visual time-frequency representation that allows the neural network to identify acoustic patterns.

### 🧠 ResNet18 Feature Extraction
A pretrained ResNet18 network extracts high-level acoustic features from the spectrogram representation.

### 🔄 Bi-GRU Temporal Modeling
A Bidirectional GRU analyzes temporal dependencies in the extracted audio features.

### 🛡️ Audio Augmentation
The training pipeline uses multiple augmentation techniques to improve robustness:

- Time shifting
- Noise injection
- Pitch shifting
- Gain adjustment
- Spectrogram masking

### 📊 Confidence-Based Prediction
The system provides a classification result along with a confidence/probability score.

### 🌐 Streamlit Interface
A simple web interface allows users to upload an audio recording and obtain a prediction without interacting directly with the ML pipeline.

### 🐳 Docker Support
The application can be containerized for easier deployment and reproducibility.

---

# 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │     Audio Input      │
                    │  WAV / MP3 / Audio   │
                    └──────────┬───────────┘
                               ↓
                    ┌──────────────────────┐
                    │ Audio Preprocessing  │
                    │ Resampling / Cleaning │
                    └──────────┬───────────┘
                               ↓
                    ┌──────────────────────┐
                    │   Mel-Spectrogram    │
                    │ Feature Extraction   │
                    └──────────┬───────────┘
                               ↓
                    ┌──────────────────────┐
                    │      ResNet18        │
                    │ Acoustic Features    │
                    └──────────┬───────────┘
                               ↓
                    ┌──────────────────────┐
                    │       Bi-GRU         │
                    │ Temporal Features    │
                    └──────────┬───────────┘
                               ↓
                    ┌──────────────────────┐
                    │ Classification Layer │
                    └──────────┬───────────┘
                               ↓
               ┌───────────────┴───────────────┐
               ↓                               ↓
        🟢 GENUINE AUDIO                🔴 AI / FRAUD
```

---

# 🧪 Machine Learning Pipeline

## 1. Audio Preprocessing

The input audio is standardized before being passed to the model.

Typical preprocessing includes:

- Audio loading
- Sampling-rate normalization
- Channel normalization
- Audio segmentation
- Signal normalization

This ensures that recordings from different sources can be processed consistently.

---

## 2. Mel-Spectrogram

The processed waveform is transformed into a **Mel-spectrogram**.

Instead of directly feeding the raw waveform into the model, the spectrogram represents how the frequency content of the voice changes over time.

This helps expose acoustic characteristics associated with:

- Artificial voice generation
- Voice conversion
- Synthetic speech
- Recording artifacts
- Abnormal frequency patterns

---

## 3. ResNet18

**ResNet18** is used as the primary feature extractor.

The CNN learns spatial patterns from the Mel-spectrogram and extracts meaningful acoustic representations from the input audio.

ResNet's residual architecture also makes deeper feature learning more stable.

---

## 4. Bi-GRU

The extracted features are passed to a **Bidirectional GRU**.

The Bi-GRU analyzes the sequence in both forward and backward directions, allowing the system to capture temporal dependencies within speech.

This is useful because synthetic speech may contain subtle inconsistencies across time that cannot always be identified from individual frames.

---

## 5. Classification

The final feature representation is passed through the classification layer.

The system produces a prediction such as:

```text
Prediction: AI / FRAUDULENT
Confidence: 94.7%
```

or

```text
Prediction: GENUINE
Confidence: 96.2%
```

The confidence score is intended as a model output rather than a guarantee of authenticity.

---

# 📚 Dataset

The project uses a combination of genuine and spoofed audio samples for training and evaluation.

### Primary Sources

- **ASVspoof 2019**
- **Generated / synthetic speech samples**
- Additional augmented training samples

The dataset contains examples representing both genuine human speech and spoofed/synthetic audio.

### Data Augmentation

To improve model robustness, training samples can undergo:

```text
Original Audio
      │
      ├── Time Shift
      ├── Noise Addition
      ├── Pitch Shift
      ├── Gain Adjustment
      └── Spectrogram Masking
```

This helps the model handle variations in recording conditions rather than memorizing a specific dataset pattern.

---

# 📈 Model Performance

The proof-of-concept implementation demonstrates approximately:

| Metric | Performance |
|---|---:|
| Precision | ~95–97% |
| Recall | ~95–97% |
| Classification | Genuine vs AI/Spoof |
| Input | Audio Recording |
| Output | Prediction + Confidence |

> **Note:** Performance can vary depending on the dataset split, audio quality, attack type, recording environment, and evaluation methodology. Real-world deployment should therefore include additional validation on unseen datasets and real-world recordings.

---

# 🎯 Use Cases

## 🏦 Banking & Finance

Detect suspicious voice recordings used for:

- Executive impersonation
- Banking scams
- Account takeover attempts
- Social engineering

## 📞 Customer Support

Help identify potentially synthetic voices interacting with automated or human support systems.

## 📡 Telecommunications

Provide an additional layer of protection against AI-assisted voice impersonation.

## 🏥 Healthcare

Help verify suspicious voice-based requests involving sensitive information or authorization.

## 🏢 Corporate Security

Protect organizations against CEO/executive voice-cloning attacks.

## 👨‍👩‍👧 Personal Safety

Potentially assist users in identifying suspicious cloned-voice recordings used in emergency or family impersonation scams.

---

# 🌍 Impact

VoxGuard aims to shift voice communication from:

> **“I recognize the voice, so I trust it.”**

to:

> **“The voice has been verified, so I can trust it with greater confidence.”**

### Expected Benefits

- 🔴 Early identification of AI-generated voice fraud
- 🛡️ Additional security layer for voice communication
- ⚡ Fast automated audio analysis
- 📊 Explainable prediction through confidence scoring
- 🌐 Easy deployment through a web interface
- 🚀 Potential integration with larger fraud detection systems

---

# 🛠️ Technology Stack

| Technology | Purpose |
|---|---|
| **Python** | Core development |
| **PyTorch** | Deep learning framework |
| **TorchAudio** | Audio processing |
| **TorchVision** | Computer vision / ResNet support |
| **Librosa** | Audio feature extraction |
| **ResNet18** | Acoustic feature extraction |
| **Bi-GRU** | Temporal sequence modeling |
| **Mel-Spectrogram** | Audio representation |
| **Streamlit** | Web application |
| **SoundFile** | Audio I/O |
| **Docker** | Containerized deployment |
| **uv** | Python dependency management |

---

# 🖥️ Application Workflow

```text
        USER
         │
         ▼
 ┌─────────────────┐
 │ Upload Audio    │
 └────────┬────────┘
          ▼
 ┌─────────────────┐
 │ Preprocessing   │
 └────────┬────────┘
          ▼
 ┌─────────────────┐
 │ Mel-Spectrogram │
 └────────┬────────┘
          ▼
 ┌─────────────────┐
 │ ResNet18        │
 └────────┬────────┘
          ▼
 ┌─────────────────┐
 │ Bi-GRU          │
 └────────┬────────┘
          ▼
 ┌─────────────────┐
 │ AI Classifier   │
 └────────┬────────┘
          ▼
 ┌─────────────────────────┐
 │ Result + Confidence     │
 └─────────────────────────┘
```

---

# 📂 Project Structure

```text
fraud-audio-detection/
│
├── data/
│   └──                  # Dataset and processed audio
│
├── models/
│   └──                  # Trained model weights
│
├── notebooks/
│   └──                  # Experiments and analysis
│
├── src/
│   ├── main.py          # Streamlit application
│   ├── model/           # Deep learning architecture
│   ├── preprocessing/   # Audio preprocessing
│   └── utils/           # Utility functions
│
├── tests/
│   └──                  # Testing
│
├── Dockerfile
├── Makefile
├── pyproject.toml
└── README.md
```

---

# ⚙️ Installation

## Prerequisites

- Python **3.11+**
- [uv](https://github.com/astral-sh/uv)
- Docker *(optional)*
- Make *(optional)*

---

## 🚀 Local Setup

Clone the repository:

```bash
git clone https://github.com/mlvanguards/fraud-audio-detection.git

cd fraud-audio-detection
```

Install dependencies:

```bash
uv sync
```

Activate the virtual environment:

### Linux / macOS

```bash
source .venv/bin/activate
```

### Windows

```bash
.venv\Scripts\activate
```

---

# ▶️ Running the Application

Start the Streamlit application:

```bash
streamlit run src/main.py
```

The application will be available at:

```text
http://localhost:8501
```

Upload an audio file through the interface and the system will analyze it and return the predicted class with its confidence score.

---

# 🐳 Docker Deployment

Build the Docker image:

```bash
docker build -t voxguard .
```

Run the container:

```bash
docker run -p 8501:8501 --rm voxguard
```

Open:

```text
http://localhost:8501
```

---

# 🔮 Future Scope

VoxGuard is designed as a proof-of-concept that can be extended into a larger real-world fraud prevention platform.

### Future enhancements include:

- 📱 Mobile application integration
- 📞 Real-time call analysis
- 🎧 Live microphone monitoring
- 🌐 Browser/VoIP integration
- 🧠 Transformer-based audio models
- 🔍 Explainable AI for suspicious audio regions
- 🗃️ Larger multilingual datasets
- 🌎 Support for Indian regional languages
- ⚡ Real-time inference optimization
- 🔐 Integration with banking and telecom security systems
- 🔗 API-based integration with existing fraud detection platforms

---

# 🇮🇳 Hackathon Vision

The long-term vision of **VoxGuard** is to create a scalable AI-based security layer capable of protecting users and organizations against the rapidly growing threat of **AI-powered voice impersonation**.

The system can serve as one component of a broader fraud detection ecosystem combining:

```text
Voice Intelligence
       +
AI Deepfake Detection
       +
Fraud Risk Analysis
       +
Identity Verification
       +
Real-Time Alerts
       ↓
Stronger Digital Security
```

---

# ⚠️ Limitations

No audio deepfake detector can guarantee perfect detection.

Performance may be affected by:

- Very low-quality recordings
- Background noise
- Unseen voice-cloning techniques
- Compression artifacts
- Languages not represented in training data
- Adversarial manipulation
- New generative-AI models

Therefore, VoxGuard should be considered a **decision-support and risk-detection system**, not the sole basis for high-stakes identity verification.

---

# 👥 Team

**Team:** ML Vanguards

**Project:** VoxGuard — AI Voice Deepfake & Fraud Detection

**Hackathon:** Smart India Hackathon

---

# 📜 License

This project is intended for educational, research, and hackathon purposes.

See the repository license for details.

---

## 🛡️ VoxGuard

### **Hear the voice. Verify the source. Stop the fraud.**