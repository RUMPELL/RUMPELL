# Jinsu Park

**Medical AI Researcher / ML Engineer**
Clinical NLP · Medical Retrieval & Embeddings · Medical Imaging · Privacy-aware ML systems

I build machine-learning systems for clinical settings where the data cannot leave the
institution — and the evaluation discipline that makes them defensible: frozen protocols,
confidence intervals, recorded negative results, and no required inference-time API.

## At a glance

| Area | Project | Key idea | Status |
|---|---|---|---|
| Medical retrieval | [K-BMEM](https://github.com/RUMPELL/K-BMEM) | Korean–English medical embeddings for on-premise retrieval, with published training and statistical-evaluation pipelines | Public · MIT · CI · **flagship** |
| Clinical NLP / LLM | Clinical AIS prediction | Qwen3-8B + LoRA multi-label injury coding from CT reports | Private (governance) |
| Medical imaging | [RSNA 2024 lumbar MRI](https://github.com/RUMPELL/RSNA2024_LSDC_kaggle) | DICOM → YOLOv8 localisation → 2.5D EfficientNet severity | Public · MIT · CI · partial |
| AI engineering | [emergency_call_stt](https://github.com/RUMPELL/emergency_call_stt) | Resumable, fully mocked-tested emergency-call STT CLI | Public · MIT · CI |
| Tabular ML | [Sarcopenia_XGboost](https://github.com/RUMPELL/Sarcopenia_XGboost) | XGBoost + feature selection under LOOCV with per-fold preprocessing; thesis work | Public · CI |

---

## Featured projects

### [K-BMEM](https://github.com/RUMPELL/K-BMEM) — Korean–English medical embeddings for on-premise retrieval  · *flagship*

**Problem.** Korean clinical text mixes Korean descriptions with English disease, drug, and
lab terminology; general-purpose embeddings blur these distinctions, and external embedding
APIs are unsuitable for hospital data.
**What I built.** A local-first dense-retrieval prototype: collision-safe contrastive batches
with false-negative controls, deterministic fine-tuning with checkpoint identity, and an
evaluation harness with paired-bootstrap CIs and exact McNemar tests against sparse, dense,
and commercial-API references. Negative results (DAPT, reranker distillation, hybrid
retrieval, source ablations) are recorded as first-class evidence. Model card, data card,
security policy, citation metadata, packaged CLI. The public release includes the original
batch-construction, fine-tuning, and statistical evaluation pipelines (4 scripts, ~4.3k LOC)
with 308 synthetic-data unit tests and a claim-to-code map.
**Status.** Public, MIT, CI on Python 3.10–3.12. Aggregate benchmark only; weights and
source datasets are not distributed, and the evaluation splits had prior exposure — stated
in the repository.

### Clinical AIS-code prediction from trauma CT reports  · *private repository*

**Problem.** Assigning AIS injury codes to free-text CT reports is manual, expert-driven
multi-label coding.
**What I built.** A Qwen3-8B sequence classifier with LoRA adapters and an MLP head
(weighted BCE); stratified multilabel splitting; date-scrubbing text pipeline; threshold +
top-k decoding; YAML-driven train/eval/external-inference CLIs; 85 standard-library unit
tests with a torch-free CI.
**Status.** Private — the multi-hospital dataset, weights, results, and code are restricted
by project governance. No performance figures are published.

### [RSNA 2024 Lumbar Spine Degenerative Classification](https://github.com/RUMPELL/RSNA2024_LSDC_kaggle) — two-stage MRI pipeline

**Problem.** Grade spinal-canal, foraminal, and subarticular stenosis severity per disc
level from multi-sequence lumbar MRI (Kaggle competition).
**What I built.** DICOM preprocessing (VOI LUT, MONOCHROME1 correction, percentile
clipping), a 2.5D three-slice crop exporter, YOLOv8 disc localisation with left/right
post-processing, and an EfficientNet severity classifier with study-level GroupKFold,
class-weighted loss, AMP, and early stopping. 50 synthetic-input unit tests cover the
DICOM, crop, split-leakage, and post-processing logic in CI.
**Status.** Public, MIT. Preprocessing and training stages run; the YOLO training-set
exporter and end-to-end submission orchestration are unfinished. No competition score is
claimed.

### [emergency_call_stt](https://github.com/RUMPELL/emergency_call_stt) — batch speech-to-text for prehospital call audio  · *engineering utility*

**Problem.** Turn folders of emergency-call recordings into transcripts for downstream
research without ever committing audio, transcripts, or credentials.
**What I built.** A resumable CLI over NAVER CLOVA Speech: recursive discovery, skip-existing
resume, per-file error records that don't poison retries, fail-closed credential loading,
secret redaction, deterministic file handling.
**Status.** Public, MIT. 67 unit tests with every network call mocked; CI on Python 3.9–3.12.

### [Sarcopenia_XGboost](https://github.com/RUMPELL/Sarcopenia_XGboost) — severity classification from protein expression  · *thesis*

**Problem.** Three-class sarcopenia severity from 5,420 protein-expression features on a
small clinical cohort (n = 72).
**What I built.** XGBoost with ANOVA / χ² / mutual-information feature selection under
LOOCV, with scaling and selection fitted inside each fold, per-fold artifacts for
raw-data inference, and a soft-voting ensemble. 17 synthetic unit tests in CI.
**Results (thesis).** A 35-biomarker signature reached AUROC 0.930; on an independent
cohort sharing 13 biomarkers, accuracy was 78.6 %. SHAP analysis highlighted SERTAD2,
HOXD8, IFTAP, and PTPRA.

---

## How these fit together

Clinical prediction work (AIS coding, sarcopenia) kept running into the same two
constraints: Korean–English mixed text, and data that cannot leave the hospital. K-BMEM is
the direct response — domain embeddings, air-gapped design, and an evaluation harness whose
standards (CIs, significance tests, negative results on record) now apply across the
imaging and speech projects too.

## Technology

Python · PyTorch · Hugging Face Transformers · PEFT / LoRA · sentence-transformers ·
timm / EfficientNet · Ultralytics YOLOv8 · pydicom / OpenCV · scikit-learn · XGBoost ·
pandas / NumPy · YAML-configured CLIs · `unittest` · GitHub Actions

## Provenance and data

- The repositories above are my own work. Forked repositories on this account
  (`Pre_hospital_mortality`, `In_hospital_mortality`, and the biosignal repositories) are
  unmodified copies of other authors' projects kept for reference; I claim no contribution
  to them.
- Public repositories contain code, configuration, and documentation only. Clinical datasets
  are governed by institutional and IRB restrictions and are not distributed. No patient
  records, protected health information, model weights, or credentials are published.
- Reported results describe the datasets and protocols documented in each repository, with
  their limitations stated there. Nothing here is a medical device or clinical
  decision-support system.
