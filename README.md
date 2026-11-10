# Faster R-CNN vs YOLOv8 — Object Detection Comparison

**Emery Fathan Zwageri — 13522079**

Evaluation of a two-stage detector (Faster R-CNN, `fasterrcnn_resnet50_fpn_v2`) against a one-stage detector (YOLOv8m) on a 1000-image COCO subset: baseline accuracy and speed, IoU precision, robustness to image perturbations, edge cases and failure modes.

## Structure

| Path | Contents |
|------|----------|
| `frcnn.ipynb` | Full experiment notebook (inference, evaluation, plots) |
| `day1/` | Baseline results: `baseline/metrics.json`, `baseline/results.csv`, experiment `log.md` |
| `day2/` | Robustness CSVs (`robustness/`), edge-case analysis, `failure_analysis.md` |
| `visualization/` | Main figures (robustness curves, 9-panel analysis) |
| `figures/` | Additional figures (detection comparisons, failure cases, heatmaps, IoU distribution) |
| `results/` | Aggregated JSON results |
| `report/` | Technical report (`technical_report.tex` / `.pdf`) |
| `notes/` | Earlier drafts and notes |

## Running

Install dependencies with `pip install -r requirements.txt`, then open `frcnn.ipynb` (Jupyter or Colab) and run all cells. YOLOv8 weights (`yolov8m.pt`) are not tracked in git; `ultralytics` downloads them automatically on first use.

To rebuild the report:

```bash
cd report && pdflatex technical_report.tex
```
