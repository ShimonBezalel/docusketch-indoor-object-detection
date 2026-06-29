# Indoor Object Detection — YOLO11 Baseline

**Primary submission:** open the notebook in Google Colab:
<https://colab.research.google.com/github/ShimonBezalel/docusketch-indoor-object-detection/blob/main/Indoor_Object_Detection_YOLO11_Baseline.ipynb>

**Static report:** <https://shimonbezalel.github.io/docusketch-indoor-object-detection/site/>

This repository contains a lean public submission for the DocuSketch Indoor Object Detection assignment. The primary deliverable is a Colab notebook that downloads and verifies the official Indoor Object Detection Dataset, parses dlib XML annotations, builds a strict sequence-aware split, trains/evaluates a YOLO11s baseline, and reports validation metrics plus good and bad validation examples.

## Result summary

| Item | Value |
|---|---|
| Model | YOLO11s (`yolo11s.pt`) |
| Split | strict sequence-aware split |
| Validation mAP@0.5 | 0.9142 |
| Validation mAP@0.5:0.95 | 0.6797 |
| Validation split | sequence 2, 217 images, 346 boxes |

## Split strategy

The dataset is built from six source video sequences, so random image-level splitting can leak adjacent or near-duplicate frames across train/validation/test. I used a strict whole-sequence split to protect validation integrity while preserving all seven classes in every subset:

| Split | Source sequences | Images | Percentage |
|---|---|---:|---:|
| train | 1, 3, 4, 5 | 1,809 | 81.744% |
| validation | 2 | 217 | 9.806% |
| test | 6 | 187 | 8.450% |

This is approximate rather than exact 80/10/10 because sequence-disjoint validation is more reliable than a numerically exact but leaky split.

## Included

- `Indoor_Object_Detection_YOLO11_Baseline.ipynb` — primary Colab notebook with saved outputs.
- `assets/` — lightweight figures, validation examples, and precomputed summary JSON.
- `site/index.html` — static report supplement.
- `requirements.txt` — package references for reproduction.
- `AI_ASSISTED_WORKFLOW.md` and `ai_workflow/skills_used.md` — concise AI-use disclosure and workflow table.

## Intentionally not included

- Raw dataset archive or extracted images.
- Converted full YOLO dataset.
- Model weights or checkpoints.
- Training bundles, runtime logs, or private work artifacts.

## Reproduce

Open the Colab notebook above. By default:

```python
RUN_TRAINING = False
USE_PRECOMPUTED_RESULTS = True
```

This shows the accepted run without starting a training job. To retrain from scratch, switch `RUN_TRAINING=True` in a Colab GPU runtime.

## Dataset attribution

Dataset: [Indoor Object Detection Dataset](https://zenodo.org/records/2654485), Zenodo DOI [10.5281/zenodo.2654485](https://doi.org/10.5281/zenodo.2654485), licensed CC BY 4.0.
Related paper: *Faster Bounding Box Annotation for Object Detection in Indoor Scenes*, DOI [10.1109/EUVIP.2018.8611732](https://doi.org/10.1109/EUVIP.2018.8611732).

## AI-assisted workflow

I used AI agents as implementation and review accelerators for dataset auditing, split validation, Colab execution, artifact handling, and final notebook QA. The key ML/evaluation decisions were manually reviewed. In particular, I rejected an initially attractive chunk-based split after visual inspection showed semantic leakage, and switched to a strict sequence split for validation integrity.

See [`AI_ASSISTED_WORKFLOW.md`](AI_ASSISTED_WORKFLOW.md) for details.
