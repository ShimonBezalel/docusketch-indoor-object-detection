# AI workflow capabilities used

| Skill / capability | Purpose in this assignment | Evidence or output | Human review gate | Included in public notebook? |
|---|---|---|---|---|
| Dataset audit | Parse and verify images, annotations, classes, and boundary boxes. | Dataset counts, class map, checksum evidence, clipping policy. | Counts and visual overlays reviewed. | Yes, summarized in dataset and annotation sections. |
| Annotation conversion review | Convert dlib XML boxes into YOLO normalized labels and test reprojection. | Conversion summary, clipped-box count, overlay sanity gallery. | Label overlays inspected before training. | Yes. |
| Split integrity review | Compare split strategies and leakage risk. | Strict sequence split selected. | Human visual review rejected a leaky chunk split. | Yes, summarized in split section. |
| Colab training execution | Run one reproducible YOLO11s baseline. | Training configuration, metrics, environment, checkpoint hash. | Metrics and artifacts verified before packaging. | Yes. |
| Artifact persistence | Preserve run identity and hashes. | Split, class-map, checkpoint, and bundle hashes. | Checkpoint reload and bundle integrity verified. | Yes, in reproducibility appendix. |
| Final notebook QA | Check standalone readability and assignment compliance. | Reviewer-facing notebook, saved outputs, static assets. | Human review before public packaging. | Yes. |

No private instructions, logs, or internal work traces are included in this public repository.
