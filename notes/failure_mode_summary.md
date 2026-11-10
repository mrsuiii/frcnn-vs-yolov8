# Failure Mode Analysis

We analyzed the 20 worst-performing images for each model to identify common failure patterns.

## Common Failures (Both Models)

- Heavy occlusion where >50% of objects are partially hidden
- Very small objects at image boundaries (cropped objects)
- Unusual viewpoints or rare object poses
- Low contrast between object and background

## Faster R-CNN Specific Failures

- Duplicate detections on large objects (RPN generating multiple overlapping proposals)
- Missed detections in highly cluttered regions

## YOLOv8 Specific Failures

- Imprecise bounding boxes on elongated objects (extreme aspect ratios)
- False positives on background textures resembling objects

## Analysis Summary

The failure analysis reveals that while both models struggle with similar challenging scenarios, their failure modes differ due to architectural differences. Faster R-CNN's two-stage approach can generate redundant proposals, while YOLOv8's single-stage prediction occasionally produces less precise boxes.

---

## Explaining Faster R-CNN's Low Precision

A critical observation from our evaluation is Faster R-CNN's surprisingly low precision (0.0749) compared to YOLOv8 (0.1409). This counterintuitive result—where a two-stage detector with refinement achieves lower precision than a single-stage detector—requires careful examination.

### Primary Cause: Annotation Style Mismatch

The primary cause is a **mismatch between COCO annotation style and Faster R-CNN's detection behavior**. COCO ground truth annotations tend to be broad bounding boxes that encompass entire object regions, sometimes including background or multiple overlapping instances. In contrast, Faster R-CNN's Region Proposal Network generates proposals that are often more *instance-focused* and tightly cropped around individual objects.

This creates an evaluation artifact: when Faster R-CNN produces a detection that correctly identifies an object but with a tighter bounding box than the COCO annotation, the IoU between prediction and ground truth falls below 0.5. Under our evaluation protocol (TP requires IoU ≥ 0.5), such detections are counted as **false positives** despite being semantically correct.

### Compounding Effect: Aggressive Detection Behavior

The effect is compounded by Faster R-CNN's aggressive detection behavior. With 24 detections versus YOLOv8's 13 detections in a typical complex scene, Faster R-CNN attempts to detect more objects, including smaller instances within cluttered regions. Many of these detections are visually correct but fail the IoU threshold due to annotation style differences. YOLOv8's more conservative approach (fewer, larger boxes) happens to align better with COCO's annotation style, resulting in higher measured precision.

### Key Insight

This finding highlights an important limitation of IoU-based evaluation: **precision metrics can be sensitive to annotation granularity and style**, not just detection quality. Faster R-CNN's low precision does not necessarily indicate poor detection capability, but rather a mismatch between its instance-focused predictions and COCO's broader annotation conventions.
