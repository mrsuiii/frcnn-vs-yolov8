# Failure Analysis Report

## Experiment Info
- **Nama**: Emery Fathan Zwageri
- **NIM**: 13522079
- **Date**: 2026-02-06 12:50:39

---

## 1. Overall Failure Statistics

### Images with No Matched Detections (IoU = 0)
| Model | Count | Percentage |
|-------|-------|------------|
| Faster R-CNN | 482 | 48.20% |
| YOLOv8 | 513 | 51.30% |

### Images with High False Negative Rate (missed more than half)
| Model | Count | Percentage |
|-------|-------|------------|
| Faster R-CNN | 825 | 82.50% |
| YOLOv8 | 837 | 83.70% |

---

## 2. Worst IoU Images (Faster R-CNN)

These images have the lowest bounding box precision:

| Rank | Image ID | Num GT | Detections | Avg IoU | TP | FP | FN |
|------|----------|--------|------------|---------|----|----|-----|
| 1 | 0 | 20 | 24 | 0.0000 | 0 | 24 | 20 |
| 2 | 2 | 18 | 38 | 0.0000 | 0 | 38 | 18 |
| 3 | 3 | 4 | 6 | 0.0000 | 0 | 6 | 4 |
| 4 | 5 | 2 | 2 | 0.0000 | 0 | 2 | 2 |
| 5 | 6 | 2 | 3 | 0.0000 | 0 | 3 | 2 |
| 6 | 7 | 4 | 4 | 0.0000 | 0 | 4 | 4 |
| 7 | 9 | 17 | 21 | 0.0000 | 0 | 21 | 17 |
| 8 | 10 | 11 | 10 | 0.0000 | 0 | 10 | 11 |
| 9 | 14 | 2 | 2 | 0.0000 | 0 | 2 | 2 |
| 10 | 16 | 8 | 10 | 0.0000 | 0 | 10 | 8 |


## 3. Worst IoU Images (YOLOv8)

| Rank | Image ID | Num GT | Detections | Avg IoU | TP | FP | FN |
|------|----------|--------|------------|---------|----|----|-----|
| 1 | 0 | 20 | 13 | 0.0000 | 0 | 13 | 20 |
| 2 | 2 | 18 | 5 | 0.0000 | 0 | 5 | 18 |
| 3 | 3 | 4 | 2 | 0.0000 | 0 | 2 | 4 |
| 4 | 5 | 2 | 2 | 0.0000 | 0 | 2 | 2 |
| 5 | 6 | 2 | 2 | 0.0000 | 0 | 2 | 2 |
| 6 | 8 | 9 | 6 | 0.0000 | 0 | 6 | 9 |
| 7 | 9 | 17 | 13 | 0.0000 | 0 | 13 | 17 |
| 8 | 10 | 11 | 7 | 0.0000 | 0 | 7 | 11 |
| 9 | 12 | 7 | 3 | 0.0000 | 0 | 3 | 7 |
| 10 | 13 | 2 | 2 | 0.0000 | 0 | 2 | 2 |


---

## 4. Images with Most False Positives (Over-detection)

### Faster R-CNN
| Image ID | Num GT | Detections | False Positives | Avg IoU |
|----------|--------|------------|-----------------|---------|
| 27 | 23 | 50 | 50 | 0.0000 |
| 233 | 28 | 50 | 50 | 0.0000 |
| 333 | 52 | 50 | 50 | 0.0000 |
| 354 | 30 | 50 | 50 | 0.0000 |
| 527 | 29 | 50 | 50 | 0.0000 |
| 644 | 26 | 50 | 50 | 0.0000 |
| 287 | 21 | 50 | 49 | 0.6835 |
| 289 | 53 | 50 | 49 | 0.5006 |
| 460 | 17 | 50 | 49 | 0.7068 |
| 123 | 29 | 48 | 48 | 0.0000 |


### YOLOv8
| Image ID | Num GT | Detections | False Positives | Avg IoU |
|----------|--------|------------|-----------------|---------|
| 181 | 54 | 32 | 30 | 0.5535 |
| 289 | 53 | 29 | 27 | 0.5253 |
| 957 | 33 | 24 | 23 | 0.6343 |
| 190 | 28 | 22 | 22 | 0.0000 |
| 517 | 26 | 22 | 22 | 0.0000 |
| 93 | 24 | 21 | 20 | 0.5644 |
| 392 | 25 | 20 | 20 | 0.0000 |
| 527 | 29 | 20 | 20 | 0.0000 |
| 560 | 23 | 20 | 20 | 0.0000 |
| 711 | 27 | 20 | 20 | 0.0000 |


---

## 5. Images with Most False Negatives (Missed Detections)

### Faster R-CNN
| Image ID | Num GT | Detections | False Negatives | Recall |
|----------|--------|------------|-----------------|--------|
| 181 | 54 | 50 | 52 | 0.0370 |
| 289 | 53 | 50 | 52 | 0.0189 |
| 333 | 52 | 50 | 52 | 0.0000 |
| 565 | 39 | 42 | 38 | 0.0256 |
| 589 | 37 | 29 | 37 | 0.0000 |
| 357 | 36 | 24 | 36 | 0.0000 |
| 775 | 37 | 46 | 36 | 0.0270 |
| 761 | 38 | 33 | 35 | 0.0789 |
| 502 | 33 | 45 | 33 | 0.0000 |
| 701 | 32 | 39 | 32 | 0.0000 |


### YOLOv8
| Image ID | Num GT | Detections | False Negatives | Recall |
|----------|--------|------------|-----------------|--------|
| 181 | 54 | 32 | 52 | 0.0370 |
| 333 | 52 | 15 | 52 | 0.0000 |
| 289 | 53 | 29 | 51 | 0.0377 |
| 565 | 39 | 15 | 38 | 0.0256 |
| 589 | 37 | 14 | 37 | 0.0000 |
| 357 | 36 | 15 | 36 | 0.0000 |
| 775 | 37 | 14 | 36 | 0.0270 |
| 761 | 38 | 18 | 34 | 0.1053 |
| 502 | 33 | 5 | 33 | 0.0000 |
| 701 | 32 | 7 | 32 | 0.0000 |


---

## 6. Common Failure Images (Difficult for Both Models)

Number of images in worst-10 for both models: **7**

Image IDs: [0, 2, 3, 5, 6, 9, 10]

These images likely contain:
- Highly occluded objects
- Small or distant objects
- Unusual viewpoints or lighting
- Objects at image boundaries


---

## 7. Failure Pattern Analysis

### Most Common Failure Scenarios:

1. **Small Objects**: Both models struggle with objects < 32×32 pixels
   - FRCNN small object IoU: 0.6543
   - YOLO small object IoU: 0.8529

2. **Crowded Scenes**: More objects = more occlusion and NMS challenges
   - FRCNN crowded scene IoU: 0.3356
   - YOLO crowded scene IoU: 0.3158

3. **Under Perturbations**: Model degradation under image corruptions
   - FRCNN worst perturbation: motion_blur (severity 3)
   - YOLO worst perturbation: jpeg_compression (severity 3)

---

## 8. Recommendations

Based on the failure analysis:

1. **For small object detection**: Consider using higher resolution inputs or specialized small object detectors
2. **For crowded scenes**: Tune NMS threshold or use soft-NMS
3. **For robustness**: Apply data augmentation matching the expected perturbations

---

*Generated automatically by the evaluation notebook*
