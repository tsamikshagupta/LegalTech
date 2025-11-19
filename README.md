# ⚖️ Court-MOE  
### *Mixture of Experts for Indian Legal Intelligence*

Court-MOE is a research-driven attempt to bring **clarity, structure, and specialization** into the processing of Indian legal documents.  
Instead of relying on one generic transformer to understand every court, Court-MOE mirrors the real judicial system —  
**different courts speak differently, so different experts should interpret them.**

This project embraces that philosophy.

---

## 🌟 What Is Court-MOE?

Court-MOE is a **Mixture-of-Experts (MoE)** architecture built for analyzing and classifying Indian court judgments and orders.  
It combines:

- A **custom legal tokenizer**  
- A **fine-tuned LegalBERT encoder**  
- A lightweight **Router network**  
- Five specialized **Expert models**, one for each court type:

| Court Type | Expert Model |
|-----------|---------------|
| 🏛️ Supreme Court | Supreme Court Expert |
| 🏛️ High Court | High Court Expert |
| 🏛️ District Court | District Court Expert |
| ⚖️ Tribunals | Tribunal Expert |
| 📜 Daily Orders | Daily Orders Expert |

Each expert is trained exclusively on its court’s data, giving it a deeper understanding of domain-specific patterns.

---

## 🧠 Why This Project?

Indian judgments are rich, diverse, and often wildly different across court types:

- **Supreme Court** → lengthy reasoning, precedent-based analysis  
- **High Courts** → appeals, detailed legal interpretation  
- **District Courts** → factual narratives and everyday disputes  
- **Tribunals** → technical and procedure-centric  
- **Daily Orders** → abrupt, short, noisy, administrative text  

A single model cannot represent all of this equally well.  
So Court-MOE routes each case to the expert that understands it best.

**One case → One expert → One specialized prediction.**  
Hard routing. No blending. No ambiguity.

---

## 🧬 Core Components

### 🔡 Custom Tokenizer  
A domain-trained BPE tokenizer that handles the unique vocabulary of Indian judgments — citations, act names, Latin terms, multilingual noise, procedural markers, etc.

### 🧩 LegalBERT Encoder  
A fine-tuned LegalBERT model adapted to Indian legal data.  
It generates robust embeddings that reflect the structure and semantics of court documents.

### 🧭 Router Network  
A 4-layer SE-Residual MLP that predicts the appropriate court type.  
Supports metadata-augmented routing for improved accuracy on District & Daily Orders.

### 👩‍⚖️ Expert Models  
Five experts, one per court. Each expert is trained using:

- 3-Fold Stratified K-Fold  
- AMP (mixed precision)  
- SWA (generalization)  
- EMA (stability)  
- MixUp (robustness)  
- Asymmetric Focal Loss (imbalance handling)

Each model learns the writing style, complexity, and reasoning pattern of its court.

---

## 🚀 Running Inference

Run the interactive CLI:

```bash
python prediction.py
```

You’ll be prompted with:

```bash
📂 Enter path to case file:
⚖️  Enter court type (press Enter to auto-detect):
```

Two Modes
1. Auto Mode (recommended)

Leave court type blank → Router selects the expert → Expert produces final prediction.

2. Manual Mode

Provide any one of:

```bash
supreme
high
district
tribunal
daily
```
The system will bypass routing and directly use that expert.

📊 Performance Summary

🧭 Router

  ~62.7% accuracy

  ~0.75 macro F1 (metadata-augmented)

  Particularly strong improvements for District and Daily Orders

👩‍⚖️ Experts

  Supreme, High, Tribunal → consistently strong

  District & Daily Orders → highest gains after metadata augmentation

  Each expert comes with detailed confusion matrices + summary reports

🎯 Vision & Roadmap

Court-MOE is built around one principle:

Legal AI should respect the structural diversity of courts.

Upcoming modules:

  🌐 MERN-based public demo
  
  🐳 Docker support for easier deployments
  
  🔍 Explainability layer (token-level and section-level insights)
  
  🤝 Ensemble inference across K-Fold splits
  
  📡 REST API for integration into legal-tech platforms
  

