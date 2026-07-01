# Real-Time Hand Gesture Recognition ✋🤖

A real-time hand gesture recognition system that uses **MediaPipe** for hand landmark detection and a **machine learning classifier** to recognize hand gestures (e.g., alphabet signs) via webcam.

## 🎯 Overview

This project captures hand landmarks from a webcam feed using MediaPipe, then feeds the normalized landmark coordinates into a trained classifier to predict and display the corresponding gesture/letter in real time.

## 📁 Project Structure

```
Real-Time-Hand-Gesture-Recognition/
│
├── collect_imgs.py          # Step 1: Collect hand gesture images via webcam
├── create_dataset.py        # Step 2: Extract landmarks and build dataset
├── train_classifier.py      # Step 3: Train the ML model
├── inference_classifier.py  # Step 4: Run real-time recognition
├── requirements.txt         # Python dependencies
└── README.md
```

> **Note:** Script names above are placeholders for the data collection, dataset creation, and training steps. Update these to match your actual filenames if different.

## ⚠️ Before Running This Project

This repo does **not** include the dataset, `data.pickle`, or `model.p` — they are excluded to keep the repository lightweight and avoid uploading large or binary files (pickle files can also pose a security risk when shared directly).

To run this project, you need to **generate them yourself** by following the steps below.

## 🚀 Setup & Usage

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/Real-Time-Hand-Gesture-Recognition.git
cd Real-Time-Hand-Gesture-Recognition
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Collect the dataset
Run the data collection script to capture hand gesture images via webcam:
```bash
python collect_imgs.py
```
This creates a `data/` folder with images organized by class label.

### 4. Create the dataset file (`data.pickle`)
Extract hand landmarks from the collected images:
```bash
python create_dataset.py
```
This generates `data.pickle`, containing the processed landmark data used for training.

### 5. Train the model (`model.p`)
Train the classifier on the processed dataset:
```bash
python train_classifier.py
```
This produces `model.p`, the trained model used for predictions.

### 6. Run real-time gesture recognition
Once `model.p` exists, launch the main script:
```bash
python inference_classifier.py
```
Press **Esc** to exit the webcam window.

## 🧠 How It Works

1. **Capture** – Webcam frames are captured using OpenCV.
2. **Detect** – MediaPipe Hands detects hand landmarks (21 key points) in each frame.
3. **Normalize** – Landmark coordinates are normalized relative to the hand's bounding box.
4. **Predict** – The normalized landmarks are passed to the trained classifier, which predicts the corresponding letter/gesture.
5. **Display** – The predicted gesture is drawn on the video frame in real time.

## 📦 Requirements

- Python 3.x
- opencv-python
- mediapipe
- numpy
- scikit-learn

Install all at once with:
```bash
pip install -r requirements.txt
```

## 📝 Notes

- Use webcam index `0` or `1` in `cv2.VideoCapture()` depending on your system if the default camera doesn't work.
- The current label map supports the alphabet (A–Z) plus a SPACE gesture — update `labels_dict` in `inference_classifier.py` if your dataset uses different classes.
- For best results, collect a diverse dataset (different lighting, hand angles, and backgrounds) when running `collect_imgs.py`.

