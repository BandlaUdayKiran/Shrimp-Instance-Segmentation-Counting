# 🦐 Shrimp Instance Segmentation & Counting

## 📌 Project Title
**Instance Segmentation of Shrimp for Detection and Counting**

---

## 🎯 Objective
Develop an end-to-end deep learning pipeline that can:
- Segment individual shrimps from images using instance segmentation
- Count the number of shrimps present in each image

---

## 📂 Dataset Description
- Images captured in controlled environments with multiple shrimps per image
- Each shrimp is annotated using **LabelMe JSON** format with 3 parts:
  - `Shrimp Shrimp` (main body)
  - `Shrimp length` (length line)
  - `Pancreas` (internal region)
- Polygons for each shrimp are **merged into a single mask**
- All data is converted into **COCO format**, and then to **YOLOv8 segmentation format**

---

## 🧠 Approach Overview

### ✅ Step 1: Data Preprocessing
- Merged the 3 parts into a **unified instance mask** per shrimp
- Converted all annotations to **COCO format** with one category: `"shrimp"`
- Converted COCO → YOLOv8 segmentation format
- Split data into **80% Train / 10% Val / 10% Test**

### ✅ Step 2: Model Training
- Used `YOLOv8-seg` for fast and efficient instance segmentation
- Applied basic augmentations: **flip**, **rotation**, **brightness**
- Tracked metrics: `mAP`, `IoU`, and shrimp count accuracy

### ✅ Step 3: Inference
- Performed inference on test images
- Saved annotated images with **bounding boxes** and **segmentation masks**
- Counted number of shrimps per image
- Exported results to CSV

---

## 🤖 Model
- **Model Used**: `YOLOv8n-seg` (Ultralytics)
- **Pretrained** on COCO, then fine-tuned on custom shrimp dataset
- Final weights: `runs/segment/shrimp_seg_model2/weights/best.pt`

---

## 📈 Metrics Tracked
- **mAP** (Mean Average Precision)
- **IoU** (Intersection over Union)
- **Shrimp Count Accuracy**

---

## 📦 Final Outputs

| Output Type | Location |
|-------------|----------|
| Annotated Images | `inference_outputs/preds/` |
| Shrimp Count CSV | `inference_outputs/shrimp_counts.csv` |
| Trained Model | `runs/segment/shrimp_seg_model2/weights/best.pt` |

---

## 📊 Example CSV Output

```csv
image_name,shrimp_count
image_001.jpg,4
image_002.jpg,2
image_003.jpg,5
...

