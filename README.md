## Hi, I'm RUMPELL

I work on **medical AI and reproducible machine-learning systems**, with a focus on
Korean–English clinical language, structured clinical prediction, and privacy-aware
system design for environments where sending data to an external API is not an option.

My interests:

- **Korean–English medical NLP and retrieval** — domain embeddings, dense retrieval, code-switched clinical text
- **Clinical prediction from free-text and tabular data** — multi-label coding, outcome modelling
- **Reproducible evaluation** — frozen protocols, confidence intervals, significance testing, honest limitations
- **On-premise / privacy-aware design** — local models, local indexes, no required inference-time API

---

## Featured Projects

| Project | What it is | Status |
|---|---|---|
| **[K-BMEM](https://github.com/RUMPELL/K-BMEM)** | Korean–English medical embedding and dense-retrieval prototype for on-premise use. Bilingual docs, model/data cards, packaged CLI, CI on Python 3.10–3.12. | Research prototype — public code, evaluation-complete |
| **Clinical_AIS_prediction** *(private)* | Multi-label AIS injury-code prediction from trauma CT report text, using a Qwen3-8B sequence classifier with LoRA and an MLP head. | Private research repository — dataset and code access restricted by project governance |
| **[emergency_call_stt](https://github.com/RUMPELL/emergency_call_stt)** | Batch speech-to-text pipeline for prehospital emergency-call audio, built on NAVER Cloud CLOVA Speech. Resumable, CLI-driven, no bundled audio. | Small production-style utility |
| **[RSNA2024_LSDC_kaggle](https://github.com/RUMPELL/RSNA2024_LSDC_kaggle)** | Two-stage lumbar-spine MRI pipeline (detection → severity classification) from the RSNA 2024 Kaggle competition. | Work in progress — pipeline skeleton, not an end-to-end system |
| **[Sarcopenia_XGboost](https://github.com/RUMPELL/Sarcopenia_XGboost)** | Sarcopenia severity classification from protein-expression features with XGBoost and feature selection under LOOCV. | Thesis work — code public, dataset not distributed |

**K-BMEM** is the project I'd point at first: it carries the most complete documentation,
the clearest evaluation protocol, and a stated account of what its numbers do and do not show.

---

## Technology

Python · PyTorch · Hugging Face Transformers · PEFT / LoRA · sentence-transformers ·
scikit-learn · XGBoost · pandas / NumPy · YAML-configured CLIs · unittest · GitHub Actions

---

## A note on data and reproducibility

Public repositories here contain **code, configuration, and documentation only**.

- Forked repositories on this account are unmodified copies of other authors' projects; I claim no contribution to them.

- Clinical datasets used in this work are governed by institutional and IRB restrictions and are **not distributed**.
- No patient records, protected health information, model weights, or credentials are published.
- Repositories document the expected data schema so the pipelines can be re-run on your own data.

Reported results describe the specific datasets and protocols documented in each repository.
Where an evaluation has known limitations, those limitations are stated in the repository rather
than omitted. Nothing here is a medical device or a clinical decision-support system.
