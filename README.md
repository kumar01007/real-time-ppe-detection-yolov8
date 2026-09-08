
# Real-Time PPE Detection Using YOLOv8

A computer vision project for detecting personal protective equipment (PPE) and safety-related objects in construction-site images using YOLOv8.

## Project Overview

Construction sites require workers to follow safety regulations such as wearing hardhats, masks, and safety vests. Manual monitoring can be difficult at scale.

This project develops an object detection system using **YOLOv8s** to identify PPE-related objects and other safety-relevant objects from construction-site images.

The trained model is evaluated on a held-out test set and exported to **ONNX** for deployment-oriented inference.

---

## Objectives

- Detect PPE and safety-related objects automatically.
- Train a YOLOv8 object detection model on construction-site imagery.
- Evaluate model performance using Precision, Recall, mAP@50, and mAP@50–95.
- Analyze class-wise detection performance.
- Measure inference speed.
- Export the trained model to ONNX format.

---

## Dataset

The project uses the **Construction Site Safety Image Dataset Roboflow**.

- **Images:** 2,801
- **Format:** YOLO
- **Classes:** 10
- **Train:** 2,605 images
- **Validation:** 114 images
- **Test:** 82 images
- **License:** CC BY 4.0

### Dataset Source

[Kaggle - Construction Site Safety Image Dataset Roboflow](https://www.kaggle.com/datasets/snehilsanyal/construction-site-safety-image-dataset-roboflow)

The dataset is **not included in this repository** due to its size.

See [`dataset_info`](dataset_info) for dataset details and the download link.

### Classes

1. Hardhat
2. Mask
3. NO-Hardhat
4. NO-Mask
5. NO-Safety Vest
6. Person
7. Safety Cone
8. Safety Vest
9. machinery
10. vehicle

---

## Tech Stack

- Python
- PyTorch
- Ultralytics YOLOv8
- OpenCV
- NumPy
- Pandas
- Matplotlib
- ONNX

---

## Project Workflow

```text
Dataset
   ↓
Dataset Verification
   ↓
Exploratory Data Analysis
   ↓
Annotation Visualization
   ↓
YOLOv8s Model Training
   ↓
Validation
   ↓
Held-Out Test Evaluation
   ↓
Error Analysis
   ↓
Inference Speed Evaluation
   ↓
ONNX Export
````

---

## Model

The project uses **YOLOv8s**, a lightweight YOLO architecture suitable for object detection applications where a balance between accuracy and inference speed is required.

### Training Configuration

* Model: YOLOv8s
* Image size: 640 × 640
* Epochs: 50
* Batch size: 8
* Optimizer: AdamW
* Pretrained weights: Yes
* Number of classes: 10

---

## Results

The final model was evaluated on the **82-image held-out test set containing 760 annotated instances**.

| Metric         |  Test Performance |
| -------------- | ----------------: |
| Precision      |        **86.72%** |
| Recall         |        **56.32%** |
| mAP@50         |        **59.34%** |
| mAP@50–95      |        **37.25%** |
| Inference Time | **27.1 ms/image** |

### Class-wise Performance

| Class          | Precision | Recall | mAP@50 |
| -------------- | --------: | -----: | -----: |
| Hardhat        |     96.9% |  57.2% |  61.0% |
| Mask           |     96.2% |  60.7% |  60.5% |
| NO-Hardhat     |     81.9% |  48.8% |  48.3% |
| NO-Mask        |     92.4% |  46.1% |  50.0% |
| NO-Safety Vest |     90.4% |  62.6% |  66.3% |
| Person         |     84.9% |  59.8% |  64.5% |
| Safety Cone    |     67.8% |  23.9% |  25.1% |
| Safety Vest    |    100.0% |  59.0% |  62.1% |
| machinery      |     82.0% |  84.1% |  88.8% |
| vehicle        |     74.8% |  61.0% |  66.8% |

### Error Analysis

The model achieves relatively high precision but lower recall, indicating that its detections are generally reliable when an object is detected, while some objects are missed.

**Safety Cone** is the most challenging class, with a recall of **23.9%** and mAP@50 of **25.1%**.

This highlights an important limitation of the current model and provides a direction for future improvement.

---

## Deployment

The trained YOLOv8s model was exported to **ONNX** format.

```text
best.onnx
Size: 42.69 MB
```

The ONNX model can be used for deployment-oriented inference in environments supporting ONNX Runtime.

---

## Repository Structure

```text
real-time-ppe-detection-yolov8/
│
├── dataset_info/
│   └── README.md
│
├── notebooks/
│   └── PPE_Detection_YOLOv8.ipynb
│
├── results/
│   └── ...
│
├── detects/
│   └── ...
│
├── models/
│   ├── best.pt
│   └── best.onnx
│
├── requirements.txt
├── .gitignore
└── README.md
```

The original dataset is excluded from the repository.

---

## How to Run

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/real-time-ppe-detection-yolov8.git
cd real-time-ppe-detection-yolov8
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Download the dataset

Download the dataset from the Kaggle source mentioned above and place it in:

```text
dataset/
```

### 4. Open the notebook

```text
notebooks/PPE_Detection_YOLOv8.ipynb
```

Run the notebook to reproduce the dataset analysis, model evaluation, and inference workflow.

---

## Future Improvements

* Improve recall through additional training and hyperparameter tuning.
* Address difficult classes such as Safety Cone and NO-Mask.
* Experiment with data augmentation and class balancing.
* Evaluate larger YOLO architectures.
* Develop real-time webcam/video inference.
* Deploy the ONNX model using ONNX Runtime.

---

## Author

**Bobbadi Kumar**

Computer Science / Data Science | Machine Learning | Deep Learning | Computer Vision

```
Also, **don't claim "real-time safety monitoring" as a completed feature**—your current project demonstrates fast object detection and ONNX export, but not a completed webcam/video monitoring application. This README keeps that distinction clear.
```
