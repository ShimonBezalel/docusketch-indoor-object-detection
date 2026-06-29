# AI-assisted workflow

AI agents were used as engineering accelerators for implementation scaffolding, repeatable checks, artifact handling, and review. They helped make the work more reproducible and easier to audit; they did not replace human evaluation judgment.

## What AI helped with

- Dataset inspection: archive checksums, image/annotation counts, dlib XML parsing, and class-map verification.
- Annotation-conversion checks: boundary-box clipping policy, YOLO normalized label conversion, and overlay sanity checks.
- Split-candidate analysis: comparing split strategies and surfacing leakage risks.
- Colab execution: running one reproducible YOLO11s baseline, preserving logs/artifacts, and recording environment details.
- Notebook QA: checking that the final Colab is readable, rerunnable, and free of private paths or heavyweight artifacts.

## What I manually reviewed

- Dataset overlays and converted-label overlays.
- Split candidates and leakage visualizations.
- Validation metric tables and support counts.
- Good and bad validation examples.
- Final notebook readability and assignment coverage.

## Human-owned evaluation decisions

The most important split decision was human-reviewed. A contiguous chunk-based split initially looked attractive numerically because it was closer to an exact 80/10/10 distribution and had stronger rare-class test support. Visual review exposed semantic leakage across split boundaries: adjacent frames still showed the same physical objects and contexts on both sides of the split.

I rejected that split and switched to strict whole-sequence splitting. The final split is slightly approximate at 81.744 / 9.806 / 8.450, but it protects validation integrity and keeps all seven classes in train, validation, and test.

## Reproducibility and audit gates

The final metrics and claims come from a hash-verified, reproducible Colab run. The notebook records the split hash, class-map hash, checkpoint hash, bundle hash, evaluator settings, and training configuration. Weak classes and limitations are reported directly rather than hidden: chair recall is the main weakness, and screen has sparse validation support.
