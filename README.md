# celtic-llm
A research project investigating whether large language models can learn and separate closely related Celtic languages through LoRA fine-tuning, and whether these languages form structured clusters in embedding spac

# Celtic LLM Fine-Tuning Project 🌍🧠

This project explores whether a single multilingual language model can learn and separate closely related Celtic languages through parameter-efficient fine-tuning.

We fine-tune a pre-trained LLM using LoRA/QLoRA on Irish, Breton, and Welsh datasets to study:
- cross-lingual transfer
- language clustering in embedding space
- translation performance on low-resource languages

---

## 🎯 Project Goals

- Fine-tune a pretrained LLM on Celtic languages
- Evaluate translation quality (Irish, Breton, Welsh ↔ English)
- Test zero-shot cross-Celtic translation (e.g., Irish → Breton)
- Visualize language clustering using t-SNE / UMAP
- Study whether Celtic languages form structured clusters in embedding space

---

## 🧠 Model

We use a parameter-efficient fine-tuning approach:

- Base model: **Gemma 4 E2B / Mistral 7B**
- Method: **LoRA / QLoRA (PEFT)**
- Frameworks: Hugging Face Transformers + TRL + Unsloth
- Precision: 4-bit quantization for low VRAM training

---

## 🌍 Languages

- Irish (Gaeilge)
- Breton (Brezhoneg)
- Welsh (Cymraeg)
- English (pivot language)

---

## 📊 Data Sources

- OPUS parallel corpora (https://opus.nlpl.eu/)
- Tatoeba sentence database (https://tatoeba.org/)
- Wikimedia dumps (https://dumps.wikimedia.org/)

All datasets are cleaned, language-tagged, and formatted into instruction-style training samples.

---

## 🏗️ Training Setup

### Example hyperparameters:
- LoRA rank: 16
- Batch size: 1–2
- Gradient accumulation: 8–16
- Epochs: 1–3
- Learning rate: 2e-4 (adjusted during experiments)
- Max sequence length: 512–1024

---

## 📈 Evaluation

We evaluate using:

### Translation metrics
- BLEU
- chrF

### Behavioral tests
- Language leakage detection
- Instruction adherence (correct language output)
- Zero-shot Celtic-to-Celtic translation

### Embedding analysis
- t-SNE / UMAP clustering
- cosine similarity between translation pairs
- language identity separability tests

---

## 🔬 Key Experiments

### 1. Language clustering in embedding space
We visualize sentence embeddings before and after fine-tuning to see whether languages form distinct clusters.

### 2. Cross-lingual transfer
We test whether the model can translate between Celtic languages it was not explicitly trained on.

### 3. Representation alignment
We measure whether translation pairs become closer in embedding space after fine-tuning.

---

## 📊 Example Results (placeholder)

| Language Pair | BLEU | chrF |
|--------------|------|------|
| Irish → English | XX.X | XX.X |
| Breton → English | XX.X | XX.X |
| Welsh → English | XX.X | XX.X |

---

## 🧪 Visualizations

We generate:
- t-SNE plots of sentence embeddings
- UMAP clustering of languages
- before/after fine-tuning comparisons

---

## 🚀 How to Run

### 1. Install dependencies
```bash
pip install -r requirements.txt
