# 🏥 Clinical Text Classifier — DistilBERT on MedNLI

Fine-tuning **DistilBERT** for Medical Natural Language Inference — classifying whether a clinical hypothesis is *entailed*, *neutral*, or *contradicted* by a clinical premise.

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/clinical-text-classifier/blob/main/clinical_text_classifier.ipynb)
[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://python.org)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-orange.svg)](https://pytorch.org)
[![HuggingFace](https://img.shields.io/badge/🤗-Transformers-yellow.svg)](https://huggingface.co)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

---

## 🚀 Run in Your Browser — No Installation Required

> **Everything runs free in Google Colab. No Python, no Jupyter, no setup.**

**→ [Open Notebook in Google Colab](https://colab.research.google.com/github/YOUR_USERNAME/clinical-text-classifier/blob/main/clinical_text_classifier.ipynb)**

Once open:
1. **Runtime → Change runtime type → T4 GPU** (free, ~4× faster)
2. **Runtime → Run all**
3. Done — the full pipeline runs in ~2 minutes

---

## 🎯 Task

**Medical NLI** determines the logical relationship between two clinical sentences:

| Label | Description | Example |
|---|---|---|
| ✅ **Entailment** | Hypothesis follows from premise | *"BP: 165/100"* → *"Patient has hypertension"* |
| ➖ **Neutral** | No logical connection | *"BP: 165/100"* → *"Patient was discharged today"* |
| ❌ **Contradiction** | Hypothesis contradicts premise | *"BP: 165/100"* → *"BP is completely normal"* |

Real-world use: EHR consistency checking, clinical decision support, automated note review.

---

## 🧠 Model

- **Base**: [`distilbert-base-uncased`](https://huggingface.co/distilbert-base-uncased) — 66M params, 40% smaller & 60% faster than BERT
- **Architecture**: DistilBERT encoder + linear classification head (3 outputs)
- **Input format**: `[CLS] premise tokens [SEP] hypothesis tokens [SEP]`

---

## 📦 Dataset

**MedNLI** — clinical NLI benchmark from MIMIC-III de-identified ICU notes.

- **Source**: [BigBIO on HuggingFace](https://huggingface.co/datasets/bigbio/mednli)
- **License**: Requires [PhysioNet](https://physionet.org/content/mednli/) registration (free)
- **Fallback**: Built-in synthetic clinical dataset — **no login required**, runs immediately

The notebook defaults to the synthetic dataset so everything works out of the box. Swap in real MedNLI by uncommenting two lines.

---

## 📂 Repository Structure

```
clinical-text-classifier/
├── clinical_text_classifier.ipynb   # Full pipeline notebook
├── requirements.txt                 # Dependencies (for local use)
└── README.md
```

---

## 🏋️ Training Config

| Hyperparameter | Value |
|---|---|
| Base model | `distilbert-base-uncased` |
| Max sequence length | 256 tokens |
| Batch size | 16 |
| Learning rate | 2e-5 |
| Epochs | 3 |
| Optimizer | AdamW |
| LR scheduler | Cosine + 10% warmup |
| Mixed precision | fp16 (auto on GPU) |
| Training time | ~2 min (T4 GPU) / ~5 min (CPU) |

---

## 📓 Notebook Steps

| Step | What Happens |
|---|---|
| 1 | GPU check + package install |
| 2 | Imports & hyperparameter config |
| 3 | Load clinical dataset (MedNLI or built-in) |
| 4 | Exploratory data analysis & label distribution |
| 5 | Tokenization as sentence pairs |
| 6 | Load DistilBERT with 3-class head |
| 7 | Define accuracy + macro F1 metrics |
| 8 | Fine-tune with HuggingFace Trainer |
| 9 | Evaluate — accuracy, F1, confusion matrix |
| 10 | Inference on custom clinical sentences |
| 11 | Save model + download from Colab |

---

## 🔬 Next Steps

- Use [`microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract`](https://huggingface.co/microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract) for higher biomedical accuracy
- Push fine-tuned model to HuggingFace Hub (one cell, uncomment & run)
- Build a [Gradio](https://gradio.app) demo and host free on [HuggingFace Spaces](https://huggingface.co/spaces)
- Extend to ICD-10 coding, clinical NER, de-identification

---

## 📄 License

MIT — see [LICENSE](LICENSE)

---

*Built with PyTorch & HuggingFace Transformers · Runs free on Google Colab*
