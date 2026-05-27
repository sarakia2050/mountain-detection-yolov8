# Mountain Detection with YOLOv8

This project is a practical Computer Vision experiment for detecting mountains using YOLOv8.

I started with a very small manually labeled dataset. I collected a few mountain images, annotated them with bounding boxes in CVAT, exported the annotations in YOLO format, and trained a first YOLO model.

As expected, the first result was not very accurate because the dataset was too small. However, this step was valuable as hands-on experience with CVAT, image annotation, YOLO-format export, and the basic training workflow.

After that, I moved to a larger annotated dataset from Roboflow Universe. The dataset I used was the **"Mountain detector"** dataset by **Snow sense**, with **2,083 mountain images** in **YOLOv8 format**.

This helped me understand the full object detection workflow:

**image collection → manual annotation → dataset preparation → training → testing → improvement**

---

## Tools Used

- Python
- YOLOv8
- Ultralytics
- CVAT
- Roboflow Universe
- PyTorch
- Conda
- PowerShell

---

## Project Workflow

1. Collected a few mountain images manually
2. Labeled mountain objects with bounding boxes in CVAT
3. Exported annotations in YOLO format
4. Trained a first YOLO model
5. Tested the model on a new mountain image
6. Improved the project using a larger Roboflow dataset
7. Trained YOLOv8 again
8. Compared the prediction confidence before and after improvement

---

## Dataset

The initial dataset was a very small manually labeled dataset that I created myself using CVAT.

For the improved model, I used a larger annotated dataset  from" Roboflow Universe ".

Dataset details:

- Source: Roboflow Universe
- Dataset name: Mountain detector
- Provider: Snow sense
- Version: v1
- Format: YOLOv8
- Number of images: 2,083
- Class: Mountain
- Dataset link: https://universe.roboflow.com/snow-sense/mountain-detector-m5f6f

The full dataset is not included in this repository due to size and licensing considerations.

---

## Manual Annotation Example

This image shows one of my first manually labeled mountain examples using a bounding box in CVAT.

![Manual Annotation in CVAT](images/manual_annotation_cvat.jpg)

---

## Training

The improved model was trained using YOLOv8n with the larger annotated mountain dataset.

Training command:

```bash
yolo detect train model=yolov8n.pt data=data.yaml epochs=10 imgsz=640
```

In my local Windows environment, I used the YOLO executable from my Conda environment directly because the global `yolo` command was pointing to the wrong Anaconda environment.

Example local command:

```bash
C:\Users\reza\anaconda3\envs\yolo-cv\Scripts\yolo.exe detect train model=yolov8n.pt data=data.yaml epochs=10 imgsz=640
```

---

## Prediction

The trained model was tested on a new mountain image.

Prediction command:

```bash
yolo detect predict model="runs/detect/train-3/weights/best.pt" source="mountain_01.jpeg" conf=0.25
```

Example local command:

```bash
C:\Users\reza\anaconda3\envs\yolo-cv\Scripts\yolo.exe detect predict model="runs\detect\train-3\weights\best.pt" source="mountain_01.jpeg" conf=0.25
```

---

## Results

The first model was trained on a very small manually labeled dataset. It detected the mountain, but only with about **25% confidence**.

After training with the larger Roboflow dataset, the confidence improved to **88%** on a new mountain image.

This improvement showed the importance of:

- dataset size
- data diversity
- annotation quality
- iterative training and testing

---

## Improved YOLOv8 Prediction

After training with the larger dataset, the model detected a mountain in a new image with **88% confidence**.

![YOLOv8 Prediction Result](images/prediction_88_confidence.jpg)

---

## What I Learned

This project helped me understand that object detection is not only about running a model.

The quality and diversity of the dataset are very important. A model trained on only a few images cannot learn enough visual variety. Using a larger and more diverse dataset helped the model make a much more confident prediction.

I also practiced the complete Computer Vision workflow:

- manual annotation
- YOLO dataset format
- model training
- prediction
- result comparison
- debugging Conda, PyTorch, and Ultralytics environment issues

---

## Troubleshooting Note

During the project, I had an environment issue where the `yolo` command was executed from the base Anaconda environment instead of the dedicated `yolo-cv` environment.

The error was related to PyTorch DLL loading in the wrong environment.

The solution was to run YOLO directly from the correct Conda environment path:

```bash
C:\Users\reza\anaconda3\envs\yolo-cv\Scripts\yolo.exe
```

After using the correct environment, training and prediction worked successfully.

---

## Repository Structure

```text
mountain-detection-yolov8/
│
├── README.md
├── requirements.txt
├── commands.txt
│
├── images/
│   ├── manual_annotation_cvat.jpg
│   └── prediction_88_confidence.jpg
```

---

## Requirements

The main Python packages used in this project are:

```text
ultralytics
torch
torchvision
opencv-python
numpy
matplotlib
pyyaml
```

---

## Next Steps

- Train the model for more epochs
- Test the model on more mountain images
- Compare YOLOv8n with larger YOLO models
- Add a small Python inference script
- Improve the documentation with more examples

---

## Summary

This project started with a small manually labeled dataset and a weak first result.

By improving the dataset and training the model again, the prediction confidence improved from about **25%** to **88%**.

For me, this was an important practical step in building my Computer Vision portfolio and understanding how real object detection projects improve step by step.