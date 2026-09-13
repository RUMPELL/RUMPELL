# Jinsu Park

**Medical AI Researcher / ML Engineer**
Clinical NLP · Medical Retrieval & Embeddings · Medical Imaging · Privacy-aware ML systems

I build machine-learning systems for clinical settings where the data cannot leave the
institution. My work runs from structured clinical prediction and Korean–English medical
text, through domain embeddings for retrieval, to the evaluation discipline and on-premise
design that make such systems defensible: frozen protocols, confidence intervals, recorded
negative results, and no required inference-time API.

---

## Featured projects

### [K-BMEM](https://github.com/RUMPELL/K-BMEM) — Korean–English medical embeddings for on-premise retrieval  · *flagship*

**Problem.** Korean clinical text mixes Korean descriptions with English disease, drug, and
lab terminology; general-purpose embeddings blur these distinctions, and external embedding
APIs are unsuitable for hospital data.
**What I built.** A local-first dense-retrieval prototype: collision-safe contrastive batches
with false-negative controls, deterministic fine-tuning with checkpoint identity, and an
evaluation harness with paired-bootstrap CIs and exact McNemar tests against sparse, dense,
and commercial-API references.
**Technical character.** Model-agnostic Python package + CLI; negative results (DAPT,
reranker distillation, hybrid retrieval, source ablations) recorded as first-class evidence;
model card, data card, security policy, citation metadata.
**Status.** Public code, MIT, CI on Python 3.10–3.12. Aggregate benchmark only; weights and
source datasets are not distributed. Evaluation splits had prior exposure and are documented
as such.

### Clinical AIS-code prediction from trauma CT reports  · *private repository*

**Problem.** Assigning AIS injury codes to free-text CT reports is manual, expert-driven
multi-label coding.
**What I built.** A Qwen3-8B sequence classifier with LoRA adapters and an MLP head trained
with weighted BCE; stratified multilabel splitting; date-scrubbing text pipeline;
threshold + top-k decoding; YAML-driven train/eval/external-inference CLIs; 85
standard-library unit tests and a torch-free CI.
**Status.** Private — the multi-hospital dataset, weights, and results are restricted by
project governance, and the code is not public at this time. No performance figures are
published.

### [RSNA 2024 Lumbar Spine Degenerative Classification](https://github.com/RUMPELL/RSNA2024_LSDC_kaggle) — two-stage MRI pipeline

**Problem.** Grade spinal-canal, foraminal, and subarticular stenosis severity per disc
level from multi-sequence lumbar MRI (Kaggle competition).
**What I built.** DICOM preprocessing (VOI LUT, MONOCHROME1 correction, percentile
clipping), a 2.5D three-slice PNG crop exporter, YOLOv8 disc localisation inference with
left/right post-processing, and an EfficientNet severity classifier with study-level
GroupKFold, class-weighted loss, AMP, and early stopping.
**Status.** Public, MIT. Training and preprocessing stages run; the YOLO training-set
exporter and the end-to-end submission orchestration are not finished, and no competition
score is claimed.

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
LOOCV, with scaling and selection fitted inside each fold, and a soft-voting ensemble.
**Results (thesis).** A 35-biomarker signature reached AUROC 0.930; on an independent
cohort sharing 13 biomarkers, accuracy was 78.6 %. SHAP analysis highlighted SERTAD2,
HOXD8, IFTAP, and PTPRA.

---

## How these fit together

Structured clinical prediction (AIS coding, sarcopenia) exposed two recurring constraints:
the text is Korean–English mixed, and the data cannot leave the hospital. K-BMEM addresses
the first with domain embeddings and the second with an air-gapped design, and its
evaluation harness — bootstrap CIs, significance testing, negative results kept on record —
is the standard I now apply across projects. The imaging and speech projects extend the
same discipline to DICOM and audio pipelines.

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
