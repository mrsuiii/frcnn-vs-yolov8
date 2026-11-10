# Generate Final Report answering the research questions
speed_ratio = frcnn_speed['avg_inference_ms'] / yolo_speed['avg_inference_ms']
accuracy_diff = frcnn_metrics['f1_score'] - yolo_metrics['f1_score']
iou_diff = frcnn_iou_analysis['mean_iou'] - yolo_iou_analysis['mean_iou']  # per-image

# Helper function to convert numpy types to native Python types for JSON serialization
def convert_to_native(obj):
    """Recursively convert numpy types to native Python types"""
    if isinstance(obj, dict):
        return {k: convert_to_native(v) for k, v in obj.items()}
    elif isinstance(obj, list):
        return [convert_to_native(item) for item in obj]
    elif isinstance(obj, np.integer):
        return int(obj)
    elif isinstance(obj, np.floating):
        return float(obj)
    elif isinstance(obj, np.ndarray):
        return obj.tolist()
    else:
        return obj

# Save all results to JSON
final_results = {
    'experiment_info': {
        'nama': 'Emery Fathan Zwageri',
        'nim': '13522079',
        'dataset': DATASET_NAME,
        'num_images': len(coco_list),
        'confidence_threshold': CONFIDENCE_THRESHOLD,
        'date': datetime.now().strftime('%Y-%m-%d %H:%M:%S')
    },
    'faster_rcnn': {
        'model': 'fasterrcnn_resnet50_fpn_v2',
        'paradigm': 'two-stage',
        'metrics': frcnn_metrics,
        'speed': frcnn_speed,
        'iou_analysis': frcnn_iou_analysis
    },
    'yolov8': {
        'model': 'yolov8m',
        'paradigm': 'single-stage',
        'metrics': yolo_metrics,
        'speed': yolo_speed,
        'iou_analysis': yolo_iou_analysis
    },
    'comparison': {
        'speed_ratio': float(speed_ratio),
        'accuracy_diff_f1': float(accuracy_diff),
        'iou_diff_per_image': float(iou_diff)
    }
}

# Convert all numpy types to native Python types before saving
final_results = convert_to_native(final_results)

with open('final_comparison_results.json', 'w') as f:
    json.dump(final_results, f, indent=2)

print("=" * 80)
print("FINAL REPORT: Two-Stage (Faster R-CNN) vs Single-Stage (YOLO) Comparison")
print("=" * 80)
print(f"\nNama: Emery Fathan Zwageri")
print(f"NIM: 13522079")
print(f"Dataset: {DATASET_NAME} ({len(coco_list)} images)")
print(f"Date: {datetime.now().strftime('%Y-%m-%d')}")

print("\n" + "=" * 80)
print("JAWABAN PERTANYAAN PENELITIAN")
print("=" * 80)

# Q1: Berapa besar peningkatan akurasi dengan two-stage?
print(f"""
📌 Q1: Berapa besar peningkatan akurasi dengan two-stage detector?

   Faster R-CNN (Two-Stage):
   - Precision: {frcnn_metrics['precision']:.4f}
   - Recall: {frcnn_metrics['recall']:.4f}
   - F1-Score: {frcnn_metrics['f1_score']:.4f}
   
   YOLOv8 (Single-Stage):
   - Precision: {yolo_metrics['precision']:.4f}
   - Recall: {yolo_metrics['recall']:.4f}
   - F1-Score: {yolo_metrics['f1_score']:.4f}
   
   ➡️ Perbedaan F1-Score: {accuracy_diff:+.4f} ({'Faster R-CNN lebih baik' if accuracy_diff > 0 else 'YOLOv8 lebih baik'})
""")

# Q2: Apakah peningkatan akurasi worth dengan lebih lambat?
print(f"""
📌 Q2: Apakah peningkatan akurasi worth dengan inference yang lebih lambat?

   Speed Comparison:
   - Faster R-CNN: {frcnn_speed['avg_inference_ms']:.1f} ms/image ({frcnn_speed['fps']:.1f} FPS)
   - YOLOv8: {yolo_speed['avg_inference_ms']:.1f} ms/image ({yolo_speed['fps']:.1f} FPS)
   - Ratio: Faster R-CNN {speed_ratio:.1f}x lebih lambat dari YOLO
   
   Trade-off Analysis:
   - Gain akurasi (F1): {abs(accuracy_diff):.4f}
   - Cost speed: {speed_ratio:.1f}x slower
   - Gain IoU (per-image): {abs(iou_diff):.4f}
   
   ➡️ Worth it jika: Akurasi/presisi lebih penting dari real-time processing
   ➡️ Tidak worth jika: Aplikasi membutuhkan real-time detection (>30 FPS)
""")

# Q3: Pada kesulitan apa two-stage lebih baik?
print(f"""
📌 Q3: Pada kesulitan apa two-stage detector lebih baik?

   By Scene Complexity (Mean IoU per-image):
   - Simple scenes (1-3 objects): 
     FRCNN: {frcnn_by_complexity['Simple (1-3 obj)']['avg_iou']:.4f}, YOLO: {yolo_by_complexity['Simple (1-3 obj)']['avg_iou']:.4f}
     Winner: {'FRCNN' if frcnn_by_complexity['Simple (1-3 obj)']['avg_iou'] > yolo_by_complexity['Simple (1-3 obj)']['avg_iou'] else 'YOLO'}
   
   - Medium scenes (4-7 objects):
     FRCNN: {frcnn_by_complexity['Medium (4-7 obj)']['avg_iou']:.4f}, YOLO: {yolo_by_complexity['Medium (4-7 obj)']['avg_iou']:.4f}
     Winner: {'FRCNN' if frcnn_by_complexity['Medium (4-7 obj)']['avg_iou'] > yolo_by_complexity['Medium (4-7 obj)']['avg_iou'] else 'YOLO'}
   
   - Complex scenes (8+ objects):
     FRCNN: {frcnn_by_complexity['Complex (8+ obj)']['avg_iou']:.4f}, YOLO: {yolo_by_complexity['Complex (8+ obj)']['avg_iou']:.4f}
     Winner: {'FRCNN' if frcnn_by_complexity['Complex (8+ obj)']['avg_iou'] > yolo_by_complexity['Complex (8+ obj)']['avg_iou'] else 'YOLO'}
   
   By Object Size (Mean IoU per-detection):
   - Small objects: FRCNN {np.mean(frcnn_ious_by_size['small']) if frcnn_ious_by_size['small'] else 0:.4f}, YOLO {np.mean(yolo_ious_by_size['small']) if yolo_ious_by_size['small'] else 0:.4f}
   - Medium objects: FRCNN {np.mean(frcnn_ious_by_size['medium']) if frcnn_ious_by_size['medium'] else 0:.4f}, YOLO {np.mean(yolo_ious_by_size['medium']) if yolo_ious_by_size['medium'] else 0:.4f}
   - Large objects: FRCNN {np.mean(frcnn_ious_by_size['large']) if frcnn_ious_by_size['large'] else 0:.4f}, YOLO {np.mean(yolo_ious_by_size['large']) if yolo_ious_by_size['large'] else 0:.4f}
""")

# Q4: Bagaimana precision bounding box (IoU) antara kedua paradigma?
print(f"""
📌 Q4: Bagaimana precision bounding box (IoU) antara kedua paradigma?

   IoU Distribution Analysis (Per-Image - Fair Comparison):
   
   Faster R-CNN (Two-Stage):
   - Mean IoU (per-image): {frcnn_iou_analysis['mean_iou']:.4f}
   - Median IoU (per-image): {frcnn_iou_analysis['median_iou']:.4f}
   - Detections dengan IoU > 0.5: {frcnn_iou_analysis['iou_gt_0.5']:.1f}%
   - Detections dengan IoU > 0.7: {frcnn_iou_analysis['iou_gt_0.7']:.1f}%
   - Detections dengan IoU > 0.9: {frcnn_iou_analysis['iou_gt_0.9']:.1f}%
   
   YOLOv8 (Single-Stage):
   - Mean IoU (per-image): {yolo_iou_analysis['mean_iou']:.4f}
   - Median IoU (per-image): {yolo_iou_analysis['median_iou']:.4f}
   - Detections dengan IoU > 0.5: {yolo_iou_analysis['iou_gt_0.5']:.1f}%
   - Detections dengan IoU > 0.7: {yolo_iou_analysis['iou_gt_0.7']:.1f}%
   - Detections dengan IoU > 0.9: {yolo_iou_analysis['iou_gt_0.9']:.1f}%
   
   ➡️ Winner: {'Faster R-CNN (Two-Stage)' if iou_diff > 0 else 'YOLOv8 (Single-Stage)'}
   ➡️ Perbedaan Mean IoU: {iou_diff:+.4f}
""")

print("=" * 80)
print("KESIMPULAN")
print("=" * 80)

# Determine winners for each aspect
iou_winner = 'Faster R-CNN' if iou_diff > 0 else 'YOLOv8'
f1_winner = 'Faster R-CNN' if accuracy_diff > 0 else 'YOLOv8'

print(f"""
1. Detection Accuracy (F1-Score):
   - Faster R-CNN: {frcnn_metrics['f1_score']:.4f}
   - YOLOv8: {yolo_metrics['f1_score']:.4f}
   - Winner: {f1_winner} (perbedaan: {abs(accuracy_diff):.4f})

2. Speed Trade-off:
   - Faster R-CNN {speed_ratio:.1f}x lebih lambat ({frcnn_speed['avg_inference_ms']:.0f}ms vs {yolo_speed['avg_inference_ms']:.0f}ms)
   - Cocok untuk: Offline processing, high-accuracy requirements
   - Tidak cocok untuk: Real-time applications, embedded systems

3. Bounding Box Precision (IoU per-image):
   - Faster R-CNN: {frcnn_iou_analysis['mean_iou']:.4f}
   - YOLOv8: {yolo_iou_analysis['mean_iou']:.4f}
   - Winner: {iou_winner} (perbedaan: {abs(iou_diff):.4f})
   
4. Insight:
   {'✅ Two-stage detector (Faster R-CNN) memberikan bounding box lebih presisi' if iou_diff > 0 else '⚠️ Berlawanan dengan ekspektasi teoritis, YOLOv8 memberikan IoU lebih tinggi'}
   {'   Hal ini sesuai dengan teori karena two-stage melakukan refinement 2x' if iou_diff > 0 else '   YOLOv8 menggunakan CIoU loss yang langsung mengoptimasi IoU'}
""")

print("\n✅ Results saved to 'final_comparison_results.json'")
print("✅ Visualizations saved to PNG files")