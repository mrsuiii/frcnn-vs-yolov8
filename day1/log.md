# Experiment Log - Faster R-CNN vs YOLOv8 Comparison

## Experiment Info
- **Nama**: Emery Fathan Zwageri
- **NIM**: 13522079
- **Date**: 2026-02-06 12:50:39
- **Dataset**: COCO-1000 (1000 images)
- **Confidence Threshold**: 0.5

## Models Evaluated
1. **Faster R-CNN** (fasterrcnn_resnet50_fpn_v2)
   - Paradigm: Two-stage detector
   - Parameters: 41.3M
   
2. **YOLOv8** (yolov8m)
   - Paradigm: Single-stage detector

## Day 1: Baseline Evaluation

### Detection Accuracy (IoU threshold = 0.5)

| Metric | Faster R-CNN | YOLOv8 | Winner |
|--------|--------------|--------|--------|
| Precision | 0.0749 | 0.1409 | YOLO |
| Recall | 0.0981 | 0.0867 | FRCNN |
| F1-Score | 0.0849 | 0.1074 | YOLO |

### Bounding Box Precision (IoU Analysis)

| Metric | Faster R-CNN | YOLOv8 | Winner |
|--------|--------------|--------|--------|
| Mean IoU (per-image) | 0.3519 | 0.3378 | FRCNN |
| IoU > 0.5 (%) | 100.0% | 100.0% | YOLO |
| IoU > 0.7 (%) | 38.6% | 41.3% | YOLO |
| IoU > 0.9 (%) | 8.4% | 12.2% | YOLO |

### Speed Comparison

| Metric | Faster R-CNN | YOLOv8 | Ratio |
|--------|--------------|--------|-------|
| Avg Inference (ms) | 152.2 | 22.8 | 6.7x |
| FPS | 6.6 | 43.9 | - |

### Performance by Object Size

| Size | FRCNN IoU | YOLO IoU | FRCNN Detections | YOLO Detections |
|------|-----------|----------|------------------|-----------------|
| Small (<32²px) | 0.6543 | 0.8529 | 3 | 1 |
| Medium (32²-96²px) | 0.6707 | 0.6994 | 25 | 18 |
| Large (>96²px) | 0.6759 | 0.6905 | 685 | 611 |

## Key Findings (Day 1)

1. **Detection Accuracy**: YOLOv8 achieves better F1-score (difference: 0.0224)
2. **Bounding Box Precision**: Faster R-CNN provides more precise bounding boxes (IoU difference: 0.0141)
3. **Speed Trade-off**: Faster R-CNN is 6.7x slower than YOLOv8

---
*Generated automatically by the evaluation notebook*
