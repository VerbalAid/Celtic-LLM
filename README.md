# 🌿 Celtic LLM: Multilingual Fine-Tuning for Celtic Languages

![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red.svg)
![Transformers](https://img.shields.io/badge/HuggingFace-Transformers-yellow.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Research](https://img.shields.io/badge/type-research-purple.svg)

---

## 🧠 Overview

This project explores whether a pretrained language model can learn and structure **all surviving Celtic languages** through efficient fine-tuning.

We fine-tune a multilingual LLM using **LoRA / QLoRA** on:

- Irish (Gaeilge)
- Scottish Gaelic (Gàidhlig)
- Manx (Gaelg)
- Welsh (Cymraeg)
- Breton (Brezhoneg)
- Cornish (Kernewek)

English is used as a pivot language for alignment and evaluation.

The goal is not only translation, but to study:

> **Whether neural models reconstruct linguistic family structure inside embedding space.**

---

## 🎯 Objectives

- Fine-tune a multilingual LLM on all surviving Celtic languages
- Build reliable Celtic ↔ English translation systems
- Test zero-shot Celtic ↔ Celtic translation
- Analyse whether Celtic languages cluster in embedding space
- Study low-resource language transfer effects

---

## 🧠 Model

We use parameter-efficient fine-tuning:

### Base Models

- 🟢 **Gemma 4 E2B** (recommended)
- 🔵 Mistral 7B (alternative)

### Fine-Tuning Method

- LoRA / QLoRA (4-bit quantisation)
- Hugging Face Transformers + PEFT
- Optional: Unsloth acceleration

---

## 🌍 Languages Covered

| Language | Code |
|---|---|
| Irish | `ga` |
| Scottish Gaelic | `gd` |
| Manx | `gv` |
| Welsh | `cy` |
| Breton | `br` |
| Cornish | `kw` |
| English | `en` |

---

## 📚 Data Sources

We use structured linguistic corpora only:

### 🌐 OPUS
https://opus.nlpl.eu/

- Parallel sentence datasets
- Celtic ↔ English translations

### 🧾 Tatoeba
https://tatoeba.org/

- Clean sentence-level translations
- Small but high-quality dataset

### 📖 Wikimedia Dumps
https://dumps.wikimedia.org/

- Monolingual Celtic text
- Used for language modelling

---

## 🏗️ Pipeline Overview

```text
Data Collection → Cleaning → Formatting → Training → Evaluation → Embedding Analysis
```

---

## 🧹 Data Format

All samples are converted into instruction-style JSONL:

```json
{
  "messages": [
    {
      "role": "system",
      "content": "You are a multilingual Celtic language model. Always obey the requested language exactly."
    },
    {
      "role": "user",
      "content": "Translate to English: <lang=ga> Dia duit, conas atá tú?"
    },
    {
      "role": "assistant",
      "content": "Hello, how are you?"
    }
  ]
}
```

---

## ⚙️ Training Setup

### LoRA Configuration

- Rank: 16
- Alpha: 32
- Dropout: 0.05
- Target modules: `q_proj`, `v_proj`

### Training Hyperparameters

| Parameter | Value |
|---|---|
| Sequence length | 512–1024 |
| Batch size | 1–2 |
| Gradient accumulation | 8–16 |
| Learning rate | 2e-4 |
| Epochs | 1–3 |

---

## 🔁 Training Strategy

Training is carried out in stages:

1. Irish ↔ English
2. Add Scottish Gaelic
3. Add Welsh + Breton
4. Add Manx + Cornish
5. Full Celtic multilingual mix

Each stage is evaluated before proceeding.

---

## 📊 Evaluation

We evaluate using:

### Translation Metrics

- BLEU
- chrF (particularly important for morphologically rich languages)

### Behavioural Tests

- Language correctness (no mixing)
- Instruction adherence
- Zero-shot Celtic ↔ Celtic translation

### Embedding Analysis

- t-SNE visualisation
- UMAP projection
- Cosine similarity between translations
- Language clustering metrics

---

## 🧪 Key Experiments

### 1. Language Clustering

Do Celtic languages form structured clusters in embedding space?

### 2. Cross-Language Transfer

Can the model translate between Celtic languages without direct training?

### 3. Representation Alignment

Do translation pairs move closer in embedding space after fine-tuning?

---

## 🧬 Hypothesis

We expect a structured Celtic embedding space:

```text
Irish ↔ Scottish Gaelic ↔ Manx
           |
   Welsh ↔ Breton ↔ Cornish
```

---

## 📁 Repository Structure

```text
celtic-llm/
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── splits/
│
├── scripts/
│   ├── download_data.py
│   ├── preprocess_data.py
│   ├── train_lora.py
│   ├── evaluate.py
│   └── embed_analysis.py
│
├── models/
├── results/
│   ├── plots/
│   └── metrics.json
│
└── README.md
```

---

## 🚀 How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Download datasets

```bash
python scripts/download_data.py
```

### 3. Preprocess data

```bash
python scripts/preprocess_data.py
```

### 4. Train model

```bash
python scripts/train_lora.py
```

### 5. Evaluate model

```bash
python scripts/evaluate.py
```

### 6. Visualise embeddings

```bash
python scripts/embed_analysis.py
```

---

## 🖥 Hardware Requirements

- NVIDIA GPU (8 GB+ VRAM minimum)
- Recommended: RTX 3070 / 3080 / 3090
- QLoRA enables training on consumer-grade GPUs

---

## 📅 One-Week Plan

| Day | Task |
|---|---|
| 1 | Download datasets |
| 2 | Clean & normalise data |
| 3 | Format JSONL dataset |
| 4 | Run initial training |
| 5 | Evaluate results |
| 6 | Retrain + improve |
| 7 | Embedding analysis + visualisation |

---

## 📌 Success Criteria

The project is considered successful if:

- Celtic languages remain clearly separated
- Translation quality improves over the baseline model
- Low-resource languages (Manx, Cornish) are usable
- Embedding space shows structured Celtic clustering
- Zero-shot Celtic ↔ Celtic transfer is at least partially achievable

---

## 🔬 Why This Matters

This project explores:

> Whether neural language models can recover linguistic family structure purely from data.

It connects:

- low-resource NLP
- multilingual representation learning
- historical linguistics
- embedding geometry

---

## 📜 Licence

MIT Licence — for research and educational use.

---

## ⭐ Acknowledgements

- Hugging Face Transformers
- Google Gemma
- OPUS Corpus Project
- Tatoeba Project
